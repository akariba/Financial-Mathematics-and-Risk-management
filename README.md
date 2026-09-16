CCRIG — Immediate Improvements Prompt
VS Code Agent Execution
No external dependencies — everything uses existing infrastructure
MANDATORY FIRST STEP — READ BEFORE TOUCHING ANYTHING
Read these files before writing a single line of code:
1. backend/app/core/data.py
2. backend/app/core/coreai.py
3. backend/app/core/enrichment.py
4. backend/app/core/scoring.py
5. backend/app/api/routes/distance_map.py
6. frontend/src/pages/DistanceMap.tsx
7. frontend/src/pages/GraphExplorer.tsx (or wherever /graph is rendered)
8. frontend/src/pages/CamResearch.tsx (or equivalent)
9. README.md

Do not assume function names, file locations, or data shapes. Read first. Then build. All five tasks are additive — nothing existing is removed or rewritten.

TASK 1 — Extend Price History from 14 to 40+ Entities
What exists

The tool already fetches Yahoo Finance OHLC for 14 entities. Find where this is implemented — likely in enrichment.py or a dedicated prices.py. The function probably looks like fetch_price_history(ticker, period).

What to add

Run the existing price fetcher for all tickers in this list. Do NOT modify the fetcher function itself — just pass more tickers to it.

python
# Add these tickers to whatever list/dict drives the price fetch
# Listed equities — Yahoo Finance will return data
ADDITIONAL_TICKERS = {
    # Hyperscalers
    "GOOGL": "Alphabet Inc.",
    "AMZN": "Amazon.com Inc.",
    "META": "Meta Platforms Inc.",
    "IBM": "IBM Corporation",

    # Semiconductors / AI hardware
    "AVGO": "Broadcom Inc.",
    "QCOM": "Qualcomm Inc.",
    "ARM":  "ARM Holdings plc",
    "MU":   "Micron Technology Inc.",
    "AMAT": "Applied Materials Inc.",
    "INTC": "Intel Corporation",

    # Memory
    "005930.KS": "Samsung Electronics Co., Ltd.",

    # Financial investors (publicly listed)
    "BX":   "Blackstone Inc.",
    "CG":   "Carlyle Group Inc.",
    "JPM":  "JPMorgan Chase & Co.",
    "C":    "Citigroup Inc.",
    "GS":   "The Goldman Sachs Group Inc.",
    "MS":   "Morgan Stanley",

    # Competing infrastructure / HPC
    "CORZ": "Core Scientific Inc.",

    # Defence / industrial (in AI theme)
    "RTX":  "RTX Corporation",
    "LMT":  "Lockheed Martin Corporation",
    "NOC":  "Northrop Grumman Corporation",
    "GD":   "General Dynamics Corporation",
    "BA":   "The Boeing Company",

    # Energy (in AI power theme)
    "XOM":  "ExxonMobil Corporation",
    "SHEL": "Shell plc",
    "BP":   "BP p.l.c.",
    "CVX":  "Chevron Corporation",

    # Materials (critical minerals)
    "RIO":  "Rio Tinto plc",
    "FCX":  "Freeport-McMoRan Inc.",

    # Shipping / logistics
    "MAERSK-B.CO": "A.P. Møller-Maersk A/S",

    # Already have but verify coverage
    "NVDA": "NVIDIA Corporation",
    "TSM":  "Taiwan Semiconductor Manufacturing Co.",
    "ASML": "ASML Holding N.V.",
    "AMD":  "Advanced Micro Devices Inc.",
    "INTC": "Intel Corporation",
    "SKHY": "SK Hynix Inc.",
    "MSFT": "Microsoft Corporation",
    "AAPL": "Apple Inc.",
}

# These are private — explicitly mark, do not attempt to fetch
PRIVATE_NO_PRICE_HISTORY = {
    "COREWEAVE":  "CoreWeave Inc.",
    "ANTHROPIC":  "Anthropic PBC",
    "OPENAI":     "OpenAI",
    "MISTRAL":    "Mistral AI",
    "LAMBDA":     "Lambda Inc.",
    "REPLICATE":  "Replicate",
    "CHAI":       "Chai Discovery",
}
Implementation rules
For private companies: store {"ticker": null, "price_history": null, "private": true, "note": "Private — no public price history"} in the enrichment cache. Display this note in Entity 360 where price history would appear.
For failed fetches (ticker not found, network error): store {"ticker": ticker, "price_history": null, "error": "fetch_failed"} — never crash, always degrade gracefully.
Cache all results in .enrichment_cache/prices/{ticker}.json — do not re-fetch on every startup.
Add a cache TTL check: if cached file is older than 24 hours, re-fetch on next enrichment run.
After fetching, update the Data & Provenance Explorer count: "X/Y issuers with market data" should reflect the new total.
Verify
# After running, check:
grep -r "price_history" .enrichment_cache/prices/ | wc -l
# Should be 40+

# Check a specific ticker
cat .enrichment_cache/prices/META.json | python3 -m json.tool | head -20
TASK 2 — Activate Stylus for Real SEC Content in CAM Research
What exists

The CAM Research page already has a "Run SEC + Web Assessment" button and "Stylus diagnostics" link. Find the frontend component and the backend handler for this button. Read the current implementation — it probably calls something like /api/cam-research/stylus or similar.

What the button currently does

From Image 4, when clicked it attempts a Stylus assessment but the note says: "R2D2 auth does not activate Stylus." This means Stylus needs a separate credential from R2D2.

What to implement

Step A — Find the Stylus credential pattern

Search the codebase for "STYLUS" or "stylus":

bash
grep -r "STYLUS\|stylus\|STYL" backend/ --include="*.py" | grep -v ".pyc"
grep -r "STYLUS\|stylus" frontend/src/ --include="*.tsx" --include="*.ts"

Find what environment variable Stylus expects. Add to .env.example:

STYLUS_API_KEY=your_stylus_key_here
STYLUS_BASE_URL=https://stylus-endpoint-from-team

Step B — Backend Stylus handler

Find the existing Stylus handler. If it exists but is returning an auth error, check:

Is STYLUS_API_KEY set in the environment?
Is the Stylus endpoint URL correct?
Is the auth header pattern correct?

The typical Citi internal API auth pattern:

python
headers = {
    "Authorization": f"Bearer {STYLUS_API_KEY}",
    "Content-Type": "application/json",
}

If the handler does not exist yet, create it following the exact same pattern as the R2D2 handler in coreai.py.

Step C — What Stylus should return per company

python
# Target output shape from Stylus SEC + web assessment
{
    "company_name": str,
    "cagid": str,
    "sec_filings": [
        {
            "form_type": str,      # "10-K", "S-1", "20-F", "10-Q"
            "filing_date": str,    # YYYY-MM-DD
            "accession_number": str,
            "sec_url": str,
            "business_excerpt": str,   # max 200 words from Item 1
            "risk_factors": [str],     # key risk factor mentions, max 3
            "concentration_mentions": [str],  # any mentions of customer/supplier concentration
        }
    ],
    "web_assessment": {
        "recent_headlines": [
            {
                "headline": str,
                "date": str,
                "source": str,
                "url": str,
            }
        ],
        "credit_relevant_developments": str,  # 2-3 sentence summary
    },
    "source": "STYLUS",
    "is_synthetic": False,
    "fetched_at": str,
}

Step D — Display in CAM Research

When Stylus returns results, display them in the STYLUS SEC + WEB ASSESSMENT section that already exists in the CAM Research page. Replace any "not connected" or error message with the real content.

Step E — Graceful fallback

If Stylus is not yet credentialed:

Keep the button visible
Show: "Stylus not yet configured — add STYLUS_API_KEY to environment"
Do not crash, do not hide the button
Log the missing credential clearly
TASK 3 — Join OSUC Exposure to Distance Map Issuer Rows
What this does

Currently the Distance Map shows ρ (inferred correlation) for each issuer. The Masterfile has real OSUC PSLE figures for some of those same companies. This task joins them so the analyst sees both in one row:

Issuer          ρ      Channel      OSUC Exposure
CoreWeave       0.95   Ownership    $193,323,429  ← real figure
NVIDIA          0.78   Supply       —  (not a direct obligor)
Microsoft       0.70   Historical   —
ServerFarm      0.81   Hidden       —
Backend change — distance.py

In the IssuerDistance dataclass, add one field:

python
@dataclass
class IssuerDistance:
    # ... existing fields ...

    # NEW — OSUC exposure if this issuer is also a Masterfile obligor
    osuc_psle_net: float | None = None       # real figure or None
    osuc_match_status: str | None = None     # "MATCHED" | "NOT_IN_POPULATION" | None
    osuc_match_name: str | None = None       # matched Masterfile name
    osuc_snapshot: str | None = None         # "Jul'26" etc.

In compute_counterparty_distances(), after building the results dict, do a single batch OSUC lookup for all issuer names:

python
# After STEP 4 (sort and filter), add:

# Batch OSUC lookup for all issuers in results
from backend.app.core.coreai import get_exposure_for_entity

for issuer_dist in ranked:
    try:
        osuc = get_exposure_for_entity(issuer_dist.issuer_id)
        if osuc and osuc.get("match_status") == "MATCHED":
            issuer_dist.osuc_psle_net = osuc.get("osuc_psle_net")
            issuer_dist.osuc_match_status = "MATCHED"
            issuer_dist.osuc_match_name = osuc.get("matched_name")
            issuer_dist.osuc_snapshot = osuc.get("snapshot_period", "Jul'26")
        else:
            issuer_dist.osuc_match_status = "NOT_IN_POPULATION"
    except Exception:
        pass  # graceful — OSUC context is supplementary
API change — add field to IssuerDistanceOut
python
class IssuerDistanceOut(BaseModel):
    # ... existing fields ...
    osuc_psle_net: float | None = None
    osuc_match_status: str | None = None
    osuc_match_name: str | None = None
    osuc_snapshot: str | None = None
Frontend change — DistanceMap.tsx

In the IssuerDistance TypeScript interface, add:

tsx
osuc_psle_net: number | null;
osuc_match_status: string | null;
osuc_match_name: string | null;
osuc_snapshot: string | null;

In the IssuerRow component header (dm-ir-head grid), add an OSUC column:

tsx
{/* After the correlation bar */}
<div className="dm-osuc">
  {issuer.osuc_match_status === "MATCHED" && issuer.osuc_psle_net ? (
    <span className="dm-osuc-value">
      ${(issuer.osuc_psle_net / 1_000_000).toFixed(1)}M
      <span className="dm-osuc-label">OSUC</span>
    </span>
  ) : (
    <span className="dm-osuc-none">—</span>
  )}
</div>

Add CSS:

css
.dm-ir-head {
  /* Update grid to add OSUC column */
  grid-template-columns: 30px 1fr auto auto auto auto;
}
.dm-osuc { width: 80px; text-align: right; }
.dm-osuc-value {
  font-size: 12px; font-weight: 600;
  color: #12233f; font-variant-numeric: tabular-nums;
}
.dm-osuc-label {
  font-size: 9px; color: #8a97a5;
  display: block; letter-spacing: .4px;
  text-transform: uppercase;
}
.dm-osuc-none { font-size: 12px; color: #c0c8d0; }

Also add in the expanded detail panel (inside dm-ir-body) when OSUC is matched:

tsx
{issuer.osuc_match_status === "MATCHED" && (
  <div className="dm-osuc-detail">
    <span className="dm-osuc-detail-label">OSUC PSLE Net</span>
    <span className="dm-osuc-detail-value">
      ${issuer.osuc_psle_net?.toLocaleString()}
    </span>
    <span className="dm-osuc-detail-meta">
      {issuer.osuc_snapshot} · Real Masterfile figure ·
      Separate from inferred ρ
    </span>
  </div>
)}
Important rule

Never mathematically combine OSUC and ρ. They are different units and different concepts. Display them side by side, clearly labelled separately. The methodology note must say: "OSUC PSLE and ρ are independent measures — OSUC is a real exposure figure; ρ is an inferred structural correlation proxy. They must never be summed or multiplied."

TASK 4 — Add Crusoe Inc and OpenAI CAMs to the Relationship Matrix
What exists

The CAM relationship matrix currently has 3 hub facilities: BX Matrix II, CoreWeave, Anthropic — producing 104 bidirectional records.

What to add

Two new hub facilities using the same extraction pipeline:

Crusoe Inc — CAGID 1040287325, TFA ~$739M (largest in CoreAI book) OpenAI OPCO LLC — CAGID 9008833883, TFA ~$519M (second largest)

How to add them

Step A — Find the CAM data extraction pipeline

Search for where the existing 3 CAMs were processed:

bash
grep -r "BX_MATRIX\|COREWEAVE\|ANTHROPIC" backend/ --include="*.py" -l
grep -r "cam_relationship\|cam_data\|relationship_html" backend/ --include="*.py" -l

Find the function that ingests CAM relationship records. It probably reads from a JSON/CSV fixture or from the Masterfile CAM Data tab.

Step B — Extract relationships for Crusoe and OpenAI

From the Masterfile CAM Data tab and Core AI - Raw data tab, extract relationship records for these two companies.

Known relationships to add for Crusoe Inc (from public sources):

python
CRUSOE_RELATIONSHIPS = [
    {
        "company_a": "Crusoe Inc",
        "company_b": "NVIDIA Corporation",
        "type": "Supplier / Customer",
        "kind": "normal",
        "relationship": "NVIDIA supplies GPUs for Crusoe's flared gas compute infrastructure; NVIDIA is also an equity investor in Crusoe.",
        "amount": "Not disclosed",
        "source": "Masterfile; Public reporting",
        "confidence": "High",
        "hub": "Crusoe",
    },
    {
        "company_a": "Crusoe Inc",
        "company_b": "Stripe",
        "type": "Select Customer",
        "kind": "normal",
        "relationship": "Stripe is a contracted customer of Crusoe's cloud compute services.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "Medium",
        "hub": "Crusoe",
    },
    {
        "company_a": "Crusoe Inc",
        "company_b": "Andreessen Horowitz",
        "type": "Equity Investor",
        "kind": "normal",
        "relationship": "Andreessen Horowitz led Crusoe's Series C funding round.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "High",
        "hub": "Crusoe",
    },
]

Known relationships to add for OpenAI (from public sources):

python
OPENAI_RELATIONSHIPS = [
    {
        "company_a": "OpenAI",
        "company_b": "Microsoft",
        "type": "Strategic Investor / Partner",
        "kind": "normal",
        "relationship": "Microsoft has invested $13Bn+ in OpenAI and is the exclusive cloud partner. Azure hosts OpenAI's compute infrastructure.",
        "amount": "$13Bn+ cumulative",
        "source": "Public reporting; SEC filings",
        "confidence": "Very High",
        "hub": "OpenAI",
    },
    {
        "company_a": "OpenAI",
        "company_b": "CoreWeave Inc",
        "type": "Customer + Equity Holder",
        "kind": "normal",
        "relationship": "OpenAI is a major CoreWeave GPU compute customer with cumulative $22.4Bn in contracts across 3 tranches; OpenAI holds $350M equity stake in CoreWeave.",
        "amount": "Cumulative $22.4Bn contracts; $350M equity",
        "source": "BX Matrix II CAM; CoreWeave QR CAM; SEC; News",
        "confidence": "Very High",
        "hub": "OpenAI",
    },
    {
        "company_a": "OpenAI",
        "company_b": "NVIDIA Corporation",
        "type": "Supplier / Strategic Partner",
        "kind": "normal",
        "relationship": "NVIDIA is OpenAI's primary GPU supplier; NVIDIA and OpenAI have deep strategic partnership on AI model training infrastructure.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "High",
        "hub": "OpenAI",
    },
    {
        "company_a": "OpenAI",
        "company_b": "SoftBank",
        "type": "Equity Investor",
        "kind": "normal",
        "relationship": "SoftBank committed $15Bn to OpenAI as part of the Stargate initiative.",
        "amount": "$15Bn committed",
        "source": "Public reporting",
        "confidence": "High",
        "hub": "OpenAI",
    },
    {
        "company_a": "OpenAI",
        "company_b": "Apple Inc",
        "type": "Enterprise Partner",
        "kind": "normal",
        "relationship": "Apple integrated ChatGPT into iOS 18 via Apple Intelligence; strategic distribution partnership.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "Very High",
        "hub": "OpenAI",
    },
]

Step C — Ingest into the relationship matrix

Add these records to the same data store that holds the BX Matrix II / CoreWeave / Anthropic records. Follow the exact same data shape — do not create a new format.

Generate bidirectional records (A→B and B→A) as the existing pipeline does.

Update the summary counts:

Records: 104 → 104 + (Crusoe records × 2) + (OpenAI records × 2)
Hubs: 3 → 5
Companies: 46 → 46 + new unique companies

Step D — Update CAM Research page

The CAM Research search suggestions currently show: Try: COREWEAVE | OPENAI | ANTHROPIC | NVIDIA | MICROSOFT | TSMC | 1037131233

Add CRUSOE to the suggestion chips.

TASK 5 — Fix Graph Explorer Blank Page
What to do first

Open the browser at http://localhost:5173/graph. Open browser DevTools → Console tab. Copy the exact error message shown.

Then search for that error in the codebase:

bash
# Common graph renderer errors after data changes:
grep -r "GraphExplorer\|graph_explorer\|force.*simulation\|d3\|cytoscape" frontend/src/ --include="*.tsx" --include="*.ts" -l
Most likely causes after the real-data integration

Cause A — Data shape changed The graph endpoint (/api/graph or similar) now returns different fields because entities were added from the real CAM/Masterfile data. The frontend expects fields that no longer exist or are now named differently.

Fix: check what /api/graph returns now vs what GraphExplorer.tsx expects. Add defensive null checks for any field that might be missing.

Cause B — Too many nodes crashing the renderer The real data added significantly more entities. If the graph tries to render all nodes at once without ego-graph bounding, it crashes.

Check: does the graph renderer have a node limit? If not, add one:

typescript
const MAX_NODES = 50; // never render more than this in one ego-graph

Cause C — Canvas/WebGL initialization timing The canvas element is not ready when the graph tries to draw. Add a mount check:

typescript
useEffect(() => {
  if (!canvasRef.current) return; // guard
  // ... rest of graph init
}, [data]); // depend on data, not empty array

Cause D — Missing entity ID format Real entities now have IDs like COREAI_BX_MATRIX_II_FUNDING while the graph renderer expected the old format BX_MATRIX.

Fix: check the entity ID format returned by the graph API against what the renderer uses to look up nodes. Normalize if needed.

After identifying the error

Whatever the specific error is — fix only that error. Do not rewrite the graph renderer. Do not change the visual design. The graph was working before — it needs a targeted fix, not a rebuild.

Verify
Navigate to localhost:5173/graph
Type "TSM" in the search box
Click Go
→ Graph should render with TSM at centre, connected entities around it
→ No blank page, no console errors
VERIFICATION CHECKLIST — run through all five before declaring done
Task 1 — Price History
□ .enrichment_cache/prices/ contains 40+ JSON files
□ Each file has date/close arrays, not empty
□ GOOGL, META, AMZN, AVGO, QCOM, ARM all present
□ CoreWeave.json exists with {"private": true, "price_history": null}
□ Data & Provenance Explorer shows "40+ issuers with market data"
□ No crash on tickers that fail — graceful null stored
Task 2 — Stylus
□ If STYLUS_API_KEY is set: clicking "Run SEC + Web Assessment" 
  returns real content, not an error
□ If not set: button shows "Stylus not yet configured" message,
  does not crash
□ Stylus content displays in the STYLUS SEC + WEB ASSESSMENT 
  section of CAM Research
□ Source tagged "STYLUS" not "SYNTHETIC"
Task 3 — OSUC in Distance Map
□ Select BX Matrix II in Distance Map left panel
□ CoreWeave row shows "$193.3M OSUC" next to ρ 0.95
□ NVIDIA row shows "—" (not a direct obligor)
□ Expanded detail panel shows the full OSUC figure with 
  "Separate from inferred ρ" note
□ No mathematical combination of OSUC and ρ anywhere
□ All existing Distance Map functionality still works
Task 4 — Crusoe + OpenAI CAMs
□ Navigate to CAM Research, search "CRUSOE"
  → returns CRUSOE INC with relationship records
□ Search "OPENAI"
  → returns OpenAI OPCO with 5 relationship records including
     Microsoft, CoreWeave, NVIDIA, SoftBank, Apple
□ Hub count in CAM Research header: 5 (was 3)
□ Record count: higher than 104
□ Bidirectional records exist (A→B and B→A for each relationship)
□ Existing CoreWeave/BX Matrix II/Anthropic records unchanged
Task 5 — Graph Explorer
□ localhost:5173/graph loads without blank page
□ No errors in browser console
□ Type "TSM" → click Go → graph renders
□ Type "NVDA" → click Go → graph renders  
□ Type "COREWEAVE" → click Go → graph renders
□ All existing graph features work (hop selector, 
  fact/derived/exposure toggles, group by)
WHAT NOT TO DO
✗ Do NOT modify scoring.py
✗ Do NOT modify the Distance Map calculation logic
✗ Do NOT remove any existing synthetic data — 
  new real data is additive alongside it
✗ Do NOT combine OSUC figures with ρ values mathematically
✗ Do NOT invent CAM relationship data — 
  only use publicly verifiable facts for Crusoe/OpenAI
✗ Do NOT rewrite the Graph Explorer — fix only the specific error
✗ Do NOT fetch price data at runtime on every page load —
  always use the cache, refresh on explicit enrichment run only
✗ Do NOT expose raw CAGIDs in any user-facing output
✗ Do NOT break any existing passing tests
PRIORITY ORDER

If short on time, do in this order:

Task 5 first (Graph Explorer fix) — it is broken, everything else works
Task 3 (OSUC in Distance Map) — highest demo value, closes the MJ question
Task 1 (price history) — improves correlation quality silently
Task 4 (Crusoe + OpenAI) — expands the relationship matrix
Task 2 (Stylus) — depends on having the credential
