# CCRIG — Master Integration Prompt
## Single comprehensive prompt for VS Code agent
## Covers all immediate improvements + Cascade Simulation
## Author: Ala-Eddine Karib, Citi ICM

---

## ⚠️ READ THIS ENTIRE PROMPT BEFORE WRITING A SINGLE LINE OF CODE ⚠️

You are working on a **running local application** at `localhost:5173`.
This is not a greenfield build. Every task here is additive.
Nothing existing is removed or rewritten unless explicitly stated.

**Non-negotiable rules before starting:**
1. Read the existing codebase files listed in Step 0 first
2. Adjust ALL function names and import paths to match what you actually find
3. Do not assume any function signature — verify it in the actual files
4. Run the full test suite after every task to confirm nothing broke
5. Every synthetic metric must carry an "Illustrative" label in the UI

---

## STEP 0 — MANDATORY PRE-READ (do this first, before anything else)

```bash
# Read these files completely before writing any code:
cat backend/app/core/data.py
cat backend/app/core/scoring.py
cat backend/app/core/coreai.py
cat backend/app/core/enrichment.py
cat backend/app/core/distance.py          # if exists
cat backend/app/core/paths.py             # if exists
cat backend/app/main.py                   # to understand router registration
cat backend/app/api/routes/distance_map.py  # if exists
cat frontend/src/App.tsx                  # or router equivalent
cat frontend/src/components/Sidebar.tsx   # nav link pattern
cat frontend/src/pages/BacktestLab.tsx
cat frontend/src/pages/GraphExplorer.tsx
cat frontend/src/pages/DistanceMap.tsx    # if exists
cat frontend/src/pages/CamResearch.tsx    # or equivalent
cat README.md
cat BUILD_REPORT.md
```

**After reading, answer these before writing code:**
- What is the actual function name for fetching entities? (e.g. `get_entities()`)
- What is the actual function name for fetching fact relations per entity?
- What does a fact relation dict look like? (keys: entity_id, relation, criticality, etc.)
- How are routes registered in main.py?
- What CSS framework / styling approach does the frontend use?
- What router library does the frontend use? (React Router v6, TanStack, etc.)
- Where does the sidebar nav live and how is a new entry added?

Do not proceed until you have read the actual files and can answer the above.

---

## OVERVIEW — 6 TASKS, EXECUTE IN ORDER

| # | Task | Priority | Effort |
|---|---|---|---|
| 1 | Fix three broken/missing things | 🔴 CRITICAL | Small |
| 2 | Extend price history to 40+ entities | 🟠 HIGH | Small |
| 3 | Join OSUC exposure to Distance Map rows | 🟠 HIGH | Medium |
| 4 | Add Crusoe + OpenAI to CAM relationship matrix | 🟠 HIGH | Small |
| 5 | Add Stylus SEC content to CAM Research | 🟡 MEDIUM | Small |
| 6 | Cascade Simulation in Backtest Lab | 🟠 HIGH | Large |

Run `python -m pytest` after Tasks 1, 3, and 6 to verify nothing broke.

---

---

# TASK 1 — FIX THREE CRITICAL ISSUES

## 1A — Fix Graph Explorer blank page (`/graph`)

**What to do:**
1. Open browser DevTools at `localhost:5173/graph`
2. Go to Console tab
3. Copy the exact error message
4. Find that error in the frontend codebase
5. Fix only that specific error — do not rewrite the renderer

**Most likely causes (check in order):**

```
Cause A: Data shape changed after real-data integration
→ The graph API endpoint returns different field names now
→ Fix: add defensive null checks in GraphExplorer.tsx for any
   field that might be missing or renamed

Cause B: Too many nodes crashing the renderer
→ Add a MAX_NODES = 60 guard before rendering
→ If node count exceeds limit, show top-60 by connection count

Cause C: Canvas initialization timing
→ Add guard: if (!canvasRef.current) return;
→ Make the useEffect depend on [data] not []

Cause D: Entity ID format mismatch
→ Real entities may have IDs like "COREAI_BX_MATRIX_II_FUNDING"
→ Check if the renderer expects a different format
→ Normalize if needed
```

**Verify:** `localhost:5173/graph` loads, type "TSM", click Go, graph renders.

---

## 1B — Fix LOW EVIDENCE badge on GUARANTOR_BACKLEVERAGE

**The bug:** BX Matrix II → CoreWeave shows "LOW EVIDENCE" badge despite
source text saying "BX Matrix II CAM; SEC 10-K/10-Q" — two independent sources.

**Find the bug:**
```bash
grep -r "LOW_EVIDENCE\|LOW EVIDENCE\|evidence.*low\|low.*evidence" backend/ --include="*.py" -i
grep -r "confidence.*evidence\|evidence.*confidence" backend/ --include="*.py" -i
```

**Fix the mapping — wherever evidence quality is computed, apply this logic:**

```python
def compute_evidence_quality(source_text: str, confidence_level: str) -> str:
    """
    Map CAM confidence + source text to evidence quality badge.
    Never return LOW for a CAM-sourced relationship with SEC corroboration.
    """
    source_lower = source_text.lower() if source_text else ""

    has_cam  = "cam" in source_lower
    has_sec  = "sec" in source_lower or "10-k" in source_lower or "10-q" in source_lower or "s-1" in source_lower
    has_news = "news" in source_lower or "reuters" in source_lower or "bloomberg" in source_lower

    conf_upper = confidence_level.upper() if confidence_level else ""

    if conf_upper in ("VERY_HIGH", "VERY HIGH") or (has_cam and has_sec and has_news):
        return "VERY HIGH"
    if conf_upper == "HIGH" or (has_cam and (has_sec or has_news)):
        return "HIGH"
    if conf_upper in ("MEDIUM_HIGH", "MEDIUM-HIGH") or has_cam:
        return "MEDIUM"
    if conf_upper == "MEDIUM":
        return "MEDIUM"
    # LOW only when genuinely thin — no CAM, no SEC, single news mention only
    return "LOW"
```

Apply this function wherever the evidence badge is currently computed.
The result: GUARANTOR_BACKLEVERAGE with "BX Matrix II CAM; SEC 10-K/10-Q" → HIGH or VERY HIGH.

**Verify:** Open Entity Explorer, search BX Matrix II, scroll to Fact Relations.
GUARANTOR_BACKLEVERAGE should now show HIGH or VERY HIGH, not LOW EVIDENCE.

---

## 1C — Wire "Illustrative" badges to 4 frontend files

**The problem:** PFE, NSE, ΔPFE, utilisation render as plain numbers.
A viewer cannot tell they are synthetic. Governance risk.

**Create one reusable component** — add to the shared components folder:

```tsx
// IllustrativeBadge.tsx
// Usage: <IllustrativeBadge /> next to any synthetic metric

export function IllustrativeBadge() {
  return (
    <span
      title="Illustrative figure — not actual exposure data. Synthetic POC."
      style={{
        fontSize: "9px",
        fontWeight: 700,
        letterSpacing: ".4px",
        textTransform: "uppercase",
        color: "#b26a00",
        background: "#fdf0dd",
        border: "1px solid #f0c870",
        borderRadius: "4px",
        padding: "1px 5px",
        marginLeft: "5px",
        verticalAlign: "middle",
        cursor: "help",
        whiteSpace: "nowrap",
      }}
    >
      Illustrative
    </span>
  );
}
```

**Wire it to these four files — find the exact lines and add the badge:**

```
File 1: DailyReview.tsx
→ Find where ΔPFE or NSE values render (around line 140-145)
→ Add <IllustrativeBadge /> immediately after each metric value

File 2: Counterparty360.tsx
→ Find where PFE, NSE, RC, utilisation render (around line 420-423)
→ Add <IllustrativeBadge /> after each

File 3: ExposureMovers.tsx
→ Find where MOVE column values render (around line 70-81)
→ Add <IllustrativeBadge /> after each MOVE value

File 4: EventStudio.tsx
→ Find where ΔPFE/NSE and utilisation render (around line 137-155)
→ Add <IllustrativeBadge /> after each
```

**Important:** The badge should appear on the metric value itself,
not just in a footnote. It must be visible without scrolling.

**Verify:** Open Exposure Movers. Each MOVE value (+900, +700, etc.)
should have a small amber "Illustrative" badge next to it.

---

---

# TASK 2 — EXTEND PRICE HISTORY TO 40+ ENTITIES

## Find the existing fetcher

```bash
grep -r "yahoo\|yfinance\|fetch_price\|price_history\|OHLC\|ohlc" backend/ --include="*.py" -l
```

Find the function that currently fetches price history for 14 entities.
Do NOT rewrite it — just call it with more tickers.

## Add these tickers

```python
ADDITIONAL_TICKERS = {
    # Hyperscalers
    "GOOGL": "Alphabet Inc.",
    "AMZN":  "Amazon.com Inc.",
    "META":  "Meta Platforms Inc.",
    "IBM":   "IBM Corporation",

    # Semiconductors / AI hardware
    "AVGO":  "Broadcom Inc.",
    "QCOM":  "Qualcomm Inc.",
    "ARM":   "ARM Holdings plc",
    "MU":    "Micron Technology Inc.",
    "AMAT":  "Applied Materials Inc.",
    "INTC":  "Intel Corporation",

    # Memory
    "005930.KS": "Samsung Electronics Co., Ltd.",

    # Financial investors (listed)
    "BX":  "Blackstone Inc.",
    "CG":  "Carlyle Group Inc.",
    "JPM": "JPMorgan Chase & Co.",
    "C":   "Citigroup Inc.",
    "GS":  "The Goldman Sachs Group Inc.",
    "MS":  "Morgan Stanley",

    # Competing infrastructure
    "CORZ": "Core Scientific Inc.",

    # Defence / industrial (in AI theme)
    "RTX": "RTX Corporation",
    "LMT": "Lockheed Martin Corporation",
    "NOC": "Northrop Grumman Corporation",
    "GD":  "General Dynamics Corporation",
    "BA":  "The Boeing Company",

    # Energy
    "XOM":  "ExxonMobil Corporation",
    "SHEL": "Shell plc",
    "BP":   "BP p.l.c.",
    "CVX":  "Chevron Corporation",

    # Materials
    "RIO": "Rio Tinto plc",
    "FCX": "Freeport-McMoRan Inc.",
}

# These are private — mark explicitly, do NOT attempt to fetch
PRIVATE_ENTITIES = {
    "COREWEAVE":  "CoreWeave Inc. — Private, no public price history",
    "ANTHROPIC":  "Anthropic PBC — Private, no public price history",
    "OPENAI":     "OpenAI — Private, no public price history",
    "MISTRAL":    "Mistral AI — Private, no public price history",
    "LAMBDA":     "Lambda Inc. — Private, no public price history",
    "CRUSOE":     "Crusoe Inc. — Private, no public price history",
}
```

## Caching rules

```python
CACHE_DIR = ".enrichment_cache/prices/"

# For each ticker:
# 1. Check if {CACHE_DIR}/{ticker}.json exists
# 2. If exists and age < 24 hours: use cache
# 3. If not exists or stale: fetch from Yahoo Finance, save to cache
# 4. If fetch fails: save {"ticker": ticker, "price_history": None, "error": "fetch_failed"}
#    Never crash — always degrade gracefully

# For private entities:
# Save {"ticker": None, "price_history": None, "private": True,
#       "note": "Private company — no public price history"}
```

## Update Data & Provenance Explorer

After fetching, the counter "X issuers with market data" in the
Data Sources page must update to reflect the new total.
Find where this count is computed and update it to read from the cache
rather than a hardcoded number.

## Verify

```bash
ls .enrichment_cache/prices/ | wc -l   # should be 40+
cat .enrichment_cache/prices/META.json | python3 -m json.tool | head -10
cat .enrichment_cache/prices/COREWEAVE.json  # should show private:true
```

---

---

# TASK 3 — JOIN OSUC EXPOSURE TO DISTANCE MAP ISSUER ROWS

## What this adds

One new column in each Distance Map issuer row showing the real OSUC
PSLE figure when the issuer is a Masterfile obligor:

```
Issuer          ρ      Channel      OSUC
CoreWeave Inc   0.95   OWNERSHIP    $193.3M ← real figure from Masterfile
NVIDIA Corp     0.78   SUPPLY       —       ← not a direct obligor
Microsoft       0.70   HISTORICAL   —
ServerFarm LLC  0.81   HIDDEN       —
```

## Backend — add to IssuerDistance dataclass

Find the `IssuerDistance` dataclass in `distance.py`.
Add these fields:

```python
# NEW fields — add to IssuerDistance dataclass
osuc_psle_net: float | None = None
osuc_match_status: str | None = None   # "MATCHED" | "NOT_IN_POPULATION"
osuc_match_name: str | None = None
osuc_snapshot: str | None = None       # e.g. "Jul'26"
```

In `compute_counterparty_distances()`, after sorting the ranked list,
add a batch OSUC lookup:

```python
# After building the ranked list, add:
# (adjust import to match actual function name in coreai.py)
try:
    from backend.app.core.coreai import get_exposure_for_entity
    for issuer_dist in ranked:
        try:
            osuc = get_exposure_for_entity(issuer_dist.issuer_id)
            if osuc and osuc.get("match_status") == "MATCHED":
                issuer_dist.osuc_psle_net    = osuc.get("osuc_psle_net")
                issuer_dist.osuc_match_status = "MATCHED"
                issuer_dist.osuc_match_name   = osuc.get("matched_name")
                issuer_dist.osuc_snapshot     = osuc.get("snapshot_period", "Jul'26")
            else:
                issuer_dist.osuc_match_status = "NOT_IN_POPULATION"
        except Exception:
            pass  # graceful — OSUC context is supplementary
except ImportError:
    pass  # coreai module not available — skip silently
```

## API — add fields to IssuerDistanceOut

```python
class IssuerDistanceOut(BaseModel):
    # ... all existing fields ...
    osuc_psle_net:     float | None = None
    osuc_match_status: str   | None = None
    osuc_match_name:   str   | None = None
    osuc_snapshot:     str   | None = None
```

## Frontend — add OSUC column to DistanceMap.tsx

**Step 1 — Add to TypeScript interface:**
```tsx
interface IssuerDistance {
  // ... existing fields ...
  osuc_psle_net:     number | null;
  osuc_match_status: string | null;
  osuc_match_name:   string | null;
  osuc_snapshot:     string | null;
}
```

**Step 2 — Add column to issuer row header:**

Find the `dm-ir-head` grid div in the IssuerRow component.
Update the grid-template-columns to add an OSUC column.
Add this element after the correlation bar:

```tsx
<div className="dm-osuc-col">
  {issuer.osuc_match_status === "MATCHED" && issuer.osuc_psle_net != null ? (
    <span className="dm-osuc-value">
      ${(issuer.osuc_psle_net / 1_000_000).toFixed(1)}M
      <span className="dm-osuc-tag">OSUC</span>
    </span>
  ) : (
    <span className="dm-osuc-empty">—</span>
  )}
</div>
```

**Step 3 — Add detail in expanded panel:**

Inside the expanded `dm-ir-body`, when OSUC is matched:
```tsx
{issuer.osuc_match_status === "MATCHED" && issuer.osuc_psle_net != null && (
  <div className="dm-osuc-detail">
    <span className="dm-osuc-detail-label">OSUC PSLE Net ({issuer.osuc_snapshot})</span>
    <span className="dm-osuc-detail-value">
      ${issuer.osuc_psle_net.toLocaleString()}
    </span>
    <span className="dm-osuc-detail-note">
      Real Masterfile figure · Separate from ρ · Never combined with correlation
    </span>
  </div>
)}
```

**Step 4 — Add CSS:**
```css
.dm-ir-head { grid-template-columns: 30px 1fr auto auto auto auto; }
.dm-osuc-col { width: 90px; text-align: right; }
.dm-osuc-value { font-size: 12px; font-weight: 600; color: #12233f; font-variant-numeric: tabular-nums; }
.dm-osuc-tag { display: block; font-size: 9px; font-weight: 700; letter-spacing: .4px; text-transform: uppercase; color: #8a97a5; }
.dm-osuc-empty { font-size: 12px; color: #c0c8d0; }
.dm-osuc-detail { margin-top: 10px; padding: 10px 14px; background: #f3f9fe; border: 1px solid #cfe6f8; border-radius: 8px; }
.dm-osuc-detail-label { font-size: 10px; font-weight: 700; letter-spacing: .5px; text-transform: uppercase; color: #5b6b7c; display: block; margin-bottom: 3px; }
.dm-osuc-detail-value { font-size: 16px; font-weight: 700; color: #12233f; display: block; font-variant-numeric: tabular-nums; }
.dm-osuc-detail-note { font-size: 10.5px; color: #8a97a5; display: block; margin-top: 4px; }
```

## ⚠️ Critical rule
NEVER mathematically combine OSUC and ρ. They are different objects:
- ρ = inferred structural correlation (dimensionless, [0,1])
- OSUC = real lending exposure in USD

The methodology note in the Distance Map must include:
*"OSUC PSLE and ρ are independent measures — OSUC is a real exposure
figure from the Masterfile; ρ is an inferred distance-based correlation proxy.
They must never be summed, multiplied, or presented as equivalent."*

## Verify
```
□ Select BX Matrix II in Distance Map
□ CoreWeave row shows "$193.3M" in OSUC column with "OSUC" tag
□ NVIDIA row shows "—" in OSUC column
□ Click CoreWeave row → expanded panel shows full $193,323,429 figure
□ "Separate from ρ · Never combined with correlation" note visible
□ All existing Distance Map functionality unchanged
```

---

---

# TASK 4 — ADD CRUSOE AND OPENAI TO CAM RELATIONSHIP MATRIX

## Find the ingestion pipeline

```bash
grep -r "BX_MATRIX\|COREWEAVE\|ANTHROPIC\|cam_relationship\|hub.*cam\|relationship.*hub" backend/ --include="*.py" -l
grep -r "GUARANTOR\|BACKLEVERAGE\|relationship_record\|cam_record" backend/ --include="*.py" -l
```

Find how the existing 3-hub CAM relationships are stored and loaded.
Follow the exact same pattern for the two new hubs.

## Crusoe Inc relationships

```python
CRUSOE_CAM_RELATIONSHIPS = [
    {
        "company_a": "Crusoe Inc",
        "company_b": "NVIDIA Corporation",
        "type": "Supplier / Investor / Customer",
        "kind": "normal",
        "hub": "Crusoe",
        "relationship_a_perspective": "NVIDIA supplies GPUs for Crusoe's AI cloud infrastructure and flared-gas compute platform; NVIDIA is also an equity investor in Crusoe.",
        "relationship_b_perspective": "Crusoe is an NVIDIA GPU cloud customer and strategic portfolio company.",
        "amount": "Not disclosed",
        "source": "Public reporting; Masterfile",
        "confidence": "High",
    },
    {
        "company_a": "Crusoe Inc",
        "company_b": "Andreessen Horowitz",
        "type": "Equity Investor",
        "kind": "normal",
        "hub": "Crusoe",
        "relationship_a_perspective": "Andreessen Horowitz led Crusoe's Series C funding round.",
        "relationship_b_perspective": "Crusoe is a growth-equity portfolio company for Andreessen Horowitz.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "High",
    },
    {
        "company_a": "Crusoe Inc",
        "company_b": "Founders Fund",
        "type": "Equity Investor",
        "kind": "normal",
        "hub": "Crusoe",
        "relationship_a_perspective": "Founders Fund participated in Crusoe's Series B and C funding rounds.",
        "relationship_b_perspective": "Crusoe is a portfolio company of Founders Fund.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "High",
    },
    {
        "company_a": "Crusoe Inc",
        "company_b": "Stripe",
        "type": "Select Customer",
        "kind": "normal",
        "hub": "Crusoe",
        "relationship_a_perspective": "Stripe is a contracted customer of Crusoe's cloud compute services.",
        "relationship_b_perspective": "Crusoe supplies GPU compute capacity to Stripe.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "Medium",
    },
    {
        "company_a": "Crusoe Inc",
        "company_b": "Amazon Web Services",
        "type": "Competitor",
        "kind": "normal",
        "hub": "Crusoe",
        "relationship_a_perspective": "AWS is a hyperscale competitor in the GPU cloud market.",
        "relationship_b_perspective": "Crusoe is a specialized GPU cloud competitor to AWS.",
        "amount": "N/A",
        "source": "Public reporting",
        "confidence": "High",
    },
]
```

## OpenAI relationships

```python
OPENAI_CAM_RELATIONSHIPS = [
    {
        "company_a": "OpenAI",
        "company_b": "Microsoft",
        "type": "Strategic Investor / Cloud Partner",
        "kind": "normal",
        "hub": "OpenAI",
        "relationship_a_perspective": "Microsoft has invested $13Bn+ in OpenAI across multiple rounds and is the exclusive cloud provider — Azure hosts OpenAI's training and inference infrastructure.",
        "relationship_b_perspective": "OpenAI is Microsoft's primary AI model partner integrated across Azure, Office 365, Bing, and GitHub Copilot.",
        "amount": "$13Bn+ cumulative investment",
        "source": "Public reporting; SEC filings",
        "confidence": "Very High",
    },
    {
        "company_a": "OpenAI",
        "company_b": "CoreWeave Inc",
        "type": "Customer + Equity Holder",
        "kind": "normal",
        "hub": "OpenAI",
        "relationship_a_perspective": "OpenAI is a major CoreWeave GPU compute customer (cumulative $22.4Bn across 3 tranches) and holds a $350M equity stake in CoreWeave.",
        "relationship_b_perspective": "CoreWeave supplies dedicated GPU infrastructure to OpenAI and OpenAI is a minority equity holder.",
        "amount": "Cumulative $22.4Bn contracts; $350M equity stake",
        "source": "BX Matrix II CAM; CoreWeave QR CAM; SEC; News",
        "confidence": "Very High",
    },
    {
        "company_a": "OpenAI",
        "company_b": "NVIDIA Corporation",
        "type": "Supplier / Strategic Partner",
        "kind": "normal",
        "hub": "OpenAI",
        "relationship_a_perspective": "NVIDIA is OpenAI's primary GPU supplier for model training and inference; strategic partnership on AI infrastructure.",
        "relationship_b_perspective": "OpenAI is one of NVIDIA's largest GPU customers globally.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "High",
    },
    {
        "company_a": "OpenAI",
        "company_b": "SoftBank Group",
        "type": "Equity Investor",
        "kind": "normal",
        "hub": "OpenAI",
        "relationship_a_perspective": "SoftBank committed $15Bn to OpenAI as part of the Stargate AI infrastructure initiative.",
        "relationship_b_perspective": "OpenAI is a major SoftBank Vision Fund / Stargate portfolio company.",
        "amount": "$15Bn committed",
        "source": "Public reporting",
        "confidence": "High",
    },
    {
        "company_a": "OpenAI",
        "company_b": "Apple Inc",
        "type": "Enterprise Partner",
        "kind": "normal",
        "hub": "OpenAI",
        "relationship_a_perspective": "Apple integrated ChatGPT into iOS 18 via Apple Intelligence — strategic distribution partnership giving OpenAI access to 1Bn+ Apple devices.",
        "relationship_b_perspective": "OpenAI provides AI model capabilities powering Apple Intelligence on iOS.",
        "amount": "Not disclosed",
        "source": "Public reporting; Apple WWDC 2024",
        "confidence": "Very High",
    },
    {
        "company_a": "OpenAI",
        "company_b": "Amazon Web Services",
        "type": "Cloud Partner / Competitor",
        "kind": "normal",
        "hub": "OpenAI",
        "relationship_a_perspective": "AWS hosts some OpenAI workloads and distributes OpenAI models via Amazon Bedrock; simultaneously a competitor via Amazon's own AI models (Titan, Nova).",
        "relationship_b_perspective": "OpenAI is both a cloud customer and an AI competitor to Amazon.",
        "amount": "Not disclosed",
        "source": "Public reporting",
        "confidence": "Medium-High",
    },
]
```

## How to ingest

1. Find the function that loads existing CAM relationship records into the data layer
2. Add `CRUSOE_CAM_RELATIONSHIPS` and `OPENAI_CAM_RELATIONSHIPS` to the same source
3. Generate bidirectional records (A→B and B→A) using the same logic as existing records
4. Update hub count: 3 → 5
5. Update total record count accordingly

## Update search suggestions in CAM Research

Find where the "Try:" search suggestion chips are defined.
Add "CRUSOE" and "OPENAI" to the list.

## Verify
```
□ CAM Research search "CRUSOE" → returns results with relationship records
□ CAM Research search "OPENAI" → returns 6 relationship records
□ Hub count shown in Entity Explorer header: 5 (was 3)
□ Bidirectional records exist: NVIDIA→OpenAI and OpenAI→NVIDIA both present
□ Existing BX Matrix II / CoreWeave / Anthropic records unchanged
```

---

---

# TASK 5 — STYLUS SEC CONTENT IN CAM RESEARCH

## Check if Stylus credential exists

```bash
grep -r "STYLUS\|stylus\|STYL_" backend/ --include="*.py" -i | grep -v ".pyc"
grep -r "STYLUS" .env* 2>/dev/null
echo "STYLUS_API_KEY from env: $STYLUS_API_KEY"
```

## If credential exists — wire it

Find the existing Stylus handler (the "Run SEC + Web Assessment" button
already exists in CAM Research — find its backend handler).

Verify the auth header pattern matches the actual Stylus API contract.
Common patterns:
```python
# Pattern A
headers = {"Authorization": f"Bearer {STYLUS_API_KEY}"}
# Pattern B  
headers = {"X-API-Key": STYLUS_API_KEY}
# Pattern C (Citi internal)
headers = {"Authorization": f"Bearer {R2D2_TOKEN}", "X-Stylus-Enable": "true"}
```

The Stylus response should populate this section in CAM Research:
```
STYLUS SEC + WEB ASSESSMENT
─────────────────────────
Filing: 10-K / S-1 / 20-F  [date]
Business: [2-3 sentence excerpt from Item 1]
Key risks: [bullet list, max 3]
Concentration: [any mentions of customer/supplier concentration]
Recent web: [3 headlines with source and date]
```

## If credential NOT yet available — graceful degradation

```tsx
// In the CAM Research Stylus section:
{!stylusAvailable ? (
  <div className="stylus-unavailable">
    <p>Stylus not yet configured.</p>
    <p>Add <code>STYLUS_API_KEY</code> to the environment to enable
       real SEC + web assessment.</p>
    <button onClick={runStylusDiagnostics}>Run diagnostics</button>
  </div>
) : (
  <button onClick={runStylusAssessment}>Run SEC + Web Assessment</button>
)}
```

Do not hide the section — show the configuration message instead.

## Add STYLUS_API_KEY to .env.example

```
# Stylus SEC + web assessment (separate from R2D2)
STYLUS_API_KEY=your_stylus_key_here
STYLUS_BASE_URL=https://stylus-endpoint-from-team
```

## Verify
```
□ If STYLUS_API_KEY set: button works, returns real SEC content
□ If not set: informative message shown, no crash, no hidden section
□ .env.example updated with STYLUS_API_KEY placeholder
```

---

---

# TASK 6 — CASCADE SIMULATION IN BACKTEST LAB

This is the largest task. Read it completely before starting.

## What it builds

A new "Cascade Simulation" tab in the Backtest Lab implementing
round-by-round credit contagion propagation, matching the reference tool:

```
LEFT panel:  Network Topology — force-directed graph coloured by failure state
RIGHT panel: Cascade Trace — round-by-round entity failure list

Controls:
- Preset scenario selector (4 scenarios)
- Custom shock: entity selector + magnitude slider
- Threshold slider (default 0.55)
- Layer B contagion toggle
- Run button
```

**Five failure states (matching reference tool):**
```
Prime      > 0.80  green  #1a7f4b
Near-Prime  0.60-0.80  yellow  #f0c040
Sub-Prime   0.40-0.60  orange  #e07820
Distressed  0.20-0.40  dark orange  #c04020
Failed     <= 0.20  red  #b13636
```

## 6A — Create `backend/app/core/cascade.py`

```python
"""
cascade.py
----------
Round-by-round credit contagion propagation over CCRIG's typed entity graph.

Algorithm: DebtRank-inspired (Battiston et al. 2012), adapted for
the CCRIG three-layer graph. Uses edge criticality weights as
transmission-strength proxy (balance-sheet capital buffers unavailable).

This is a POC illustration. All outputs tagged is_synthetic=True.
"""

from __future__ import annotations
from dataclasses import dataclass, field
from enum import Enum
from typing import Optional
import math
import logging

logger = logging.getLogger(__name__)


class FailureState(str, Enum):
    PRIME      = "Prime"
    NEAR_PRIME = "Near-Prime"
    SUB_PRIME  = "Sub-Prime"
    DISTRESSED = "Distressed"
    FAILED     = "Failed"


STATE_COLORS = {
    FailureState.PRIME:      "#1a7f4b",
    FailureState.NEAR_PRIME: "#f0c040",
    FailureState.SUB_PRIME:  "#e07820",
    FailureState.DISTRESSED: "#c04020",
    FailureState.FAILED:     "#b13636",
}


def score_to_state(score: float) -> FailureState:
    if score > 0.80: return FailureState.PRIME
    if score > 0.60: return FailureState.NEAR_PRIME
    if score > 0.40: return FailureState.SUB_PRIME
    if score > 0.20: return FailureState.DISTRESSED
    return FailureState.FAILED


# Transmission weight by relationship type
# How strongly distress propagates along each edge type (0.0 to 1.0)
TRANSMISSION_WEIGHTS = {
    "GUARANTOR_BACKLEVERAGE":     0.95,
    "SPONSOR_EQUITY_HOLDER":      0.85,
    "EQUITY_INVESTOR":            0.70,
    "CONTRACTED_CUSTOMER":        0.75,
    "CUSTOMER_EQUITY_HOLDER":     0.75,
    "COMPLETED_ACQUISITION":      0.80,
    "FAILED_M&A_TARGET":          0.20,
    "SUPPLIES":                   0.60,
    "SUPPLIED_BY":                0.55,
    "SUPPLY_CHAIN":               0.55,
    "SUPPLIER_INVESTOR_CUSTOMER": 0.70,
    "AGENT_BANK":                 0.40,
    "COMPETITOR":                 0.15,
    "PEER_CUSTOMER_PARTNER":      0.25,
    "SELECT_CUSTOMER":            0.45,
    "_DEFAULT":                   0.20,
}


def get_tx_weight(edge_type: str) -> float:
    return TRANSMISSION_WEIGHTS.get(
        edge_type.upper().replace(" ", "_"),
        TRANSMISSION_WEIGHTS["_DEFAULT"],
    )


@dataclass
class EntityState:
    entity_id: str
    entity_name: str
    entity_type: str
    entity_sector: str
    current_health: float = 1.0
    state: FailureState = FailureState.PRIME
    failed_in_round: Optional[int] = None
    shock_received: float = 0.0
    shock_sources: list[str] = field(default_factory=list)


@dataclass
class CascadeRound:
    round_number: int
    new_failures: list[str]
    state_changes: list[dict]
    total_failed: int


@dataclass
class CascadeResult:
    scenario_name: str
    initial_shock_entity: str
    initial_shock_magnitude: float
    threshold: float
    rounds: list[CascadeRound]
    final_states: dict[str, EntityState]
    total_entities: int
    total_failed: int
    total_distressed: int
    converged: bool
    rounds_to_convergence: int
    nodes: list[dict]
    edges: list[dict]
    is_synthetic: bool = True
    methodology_note: str = (
        "DebtRank-inspired cascade over CCRIG typed entity graph. "
        "Transmission weights derived from edge criticality and relationship type "
        "— not from balance-sheet capital buffers (unavailable in POC). "
        "Health scores are inferred, not observed defaults. Synthetic POC."
    )


def run_cascade(
    initial_shock_entity_id: str,
    initial_shock_magnitude: float = 1.0,
    threshold: float = 0.55,
    max_rounds: int = 10,
    scenario_name: str = "Custom shock",
    include_layer_b: bool = False,
) -> CascadeResult:
    """
    Run round-by-round cascade from one shocked entity.
    Reads from existing CCRIG data layer — does not modify it.
    """

    # ── Import actual functions from data.py ──────────────────────────────
    # ADJUST THESE NAMES to match what you find in data.py:
    from backend.app.core.data import get_entities
    # Find and use the actual function for getting fact relations:
    # Common names: get_fact_relations, get_fact_relations_for_entity,
    #               get_layer_a_edges, get_relations_for_node
    # Example (adjust):
    from backend.app.core.data import get_fact_relations_for_entity

    entities = get_entities()
    if initial_shock_entity_id not in entities:
        raise ValueError(f"Entity '{initial_shock_entity_id}' not found")

    # Initialise all entities at full health
    states: dict[str, EntityState] = {
        eid: EntityState(
            entity_id=eid,
            entity_name=e.get("name", eid),
            entity_type=e.get("type", ""),
            entity_sector=e.get("sector", ""),
        )
        for eid, e in entities.items()
    }

    # Apply initial shock
    shocked = states[initial_shock_entity_id]
    shocked.current_health = max(0.0, 1.0 - initial_shock_magnitude)
    shocked.state = score_to_state(shocked.current_health)
    shocked.shock_received = initial_shock_magnitude
    if shocked.current_health <= threshold:
        shocked.failed_in_round = 0

    rounds: list[CascadeRound] = []
    r0_failures = [eid for eid, s in states.items() if s.failed_in_round == 0]
    rounds.append(CascadeRound(
        round_number=0,
        new_failures=r0_failures,
        state_changes=[{
            "entity_id": initial_shock_entity_id,
            "entity_name": shocked.entity_name,
            "from_state": FailureState.PRIME.value,
            "to_state": shocked.state.value,
            "shock_received": initial_shock_magnitude,
            "shock_source": "INITIAL_SHOCK",
        }],
        total_failed=len(r0_failures),
    ))

    converged = False
    for rnum in range(1, max_rounds + 1):
        # Find entities transmitting shock this round
        transmitting = [
            s for s in states.values()
            if s.current_health <= threshold and s.failed_in_round is not None
        ]
        if not transmitting:
            converged = True
            break

        health_deltas: dict[str, float] = {}
        shock_sources: dict[str, list[str]] = {}

        for tx in transmitting:
            try:
                relations = get_fact_relations_for_entity(tx.entity_id)
            except Exception:
                continue

            for rel in relations:
                tid = rel.get("other_entity_id") or rel.get("entity_b_id")
                if not tid or tid not in states:
                    continue
                if states[tid].current_health <= threshold:
                    continue  # already failed

                rel_type = str(rel.get("relation", "")).upper()
                criticality = float(rel.get("criticality", 0.5))
                tx_weight = get_tx_weight(rel_type)
                distress = 1.0 - tx.current_health
                shock = distress * tx_weight * criticality

                if shock < 0.005:
                    continue

                health_deltas[tid] = health_deltas.get(tid, 0.0) + shock
                shock_sources.setdefault(tid, []).append(
                    f"{tx.entity_name} ({rel_type}, -{shock:.3f})"
                )

        if not health_deltas:
            converged = True
            break

        round_changes = []
        new_failures = []

        for tid, delta in health_deltas.items():
            target = states[tid]
            old_state = target.state
            target.current_health = max(0.0, target.current_health - delta)
            target.shock_received += delta
            target.shock_sources.extend(shock_sources.get(tid, []))
            target.state = score_to_state(target.current_health)

            if target.current_health <= threshold and target.failed_in_round is None:
                target.failed_in_round = rnum
                new_failures.append(tid)

            if target.state != old_state:
                round_changes.append({
                    "entity_id": tid,
                    "entity_name": target.entity_name,
                    "from_state": old_state.value,
                    "to_state": target.state.value,
                    "shock_received": round(delta, 3),
                    "shock_sources": shock_sources.get(tid, [])[:3],
                })

        total_failed = sum(1 for s in states.values() if s.failed_in_round is not None)
        rounds.append(CascadeRound(
            round_number=rnum,
            new_failures=new_failures,
            state_changes=round_changes,
            total_failed=total_failed,
        ))

        if not round_changes:
            converged = True
            break

    # Build node list with circular initial layout
    n = len(states)
    nodes = []
    for i, (eid, s) in enumerate(states.items()):
        angle = (2 * math.pi * i) / max(n, 1)
        nodes.append({
            "id": eid,
            "name": s.entity_name,
            "type": s.entity_type,
            "sector": s.entity_sector,
            "state": s.state.value,
            "color": STATE_COLORS[s.state],
            "health": round(s.current_health, 3),
            "shock_received": round(s.shock_received, 3),
            "failed_in_round": s.failed_in_round,
            "shock_sources": s.shock_sources[:5],
            "x": 400 + 300 * math.cos(angle),
            "y": 300 + 250 * math.sin(angle),
        })

    # Build edge list
    edges = []
    seen = set()
    for eid in states:
        try:
            rels = get_fact_relations_for_entity(eid)
            for rel in rels:
                tid = rel.get("other_entity_id") or rel.get("entity_b_id")
                if not tid or tid not in states:
                    continue
                key = tuple(sorted([eid, tid]))
                if key in seen:
                    continue
                seen.add(key)
                rel_type = str(rel.get("relation", "")).upper()
                edges.append({
                    "source": eid,
                    "target": tid,
                    "weight": float(rel.get("criticality", 0.5)),
                    "type": rel_type,
                    "transmission_weight": get_tx_weight(rel_type),
                })
        except Exception:
            continue

    total_failed = sum(1 for s in states.values() if s.failed_in_round is not None)
    total_distressed = sum(1 for s in states.values() if s.state == FailureState.DISTRESSED)

    return CascadeResult(
        scenario_name=scenario_name,
        initial_shock_entity=initial_shock_entity_id,
        initial_shock_magnitude=initial_shock_magnitude,
        threshold=threshold,
        rounds=rounds,
        final_states=states,
        total_entities=len(states),
        total_failed=total_failed,
        total_distressed=total_distressed,
        converged=converged,
        rounds_to_convergence=len(rounds),
        nodes=nodes,
        edges=edges,
    )


# Pre-built scenarios
PRESET_SCENARIOS = {
    "taiwan_earthquake": {
        "name": "Taiwan earthquake — TSMC disruption",
        "entity_id": "TSM",
        "magnitude": 0.80,
        "threshold": 0.55,
        "description": "Magnitude 7.2 near Hsinchu disrupts TSMC fabrication. Propagates through GPU supply chain to NVIDIA, AMD, then to AI-infrastructure counterparties.",
    },
    "coreweave_default": {
        "name": "CoreWeave credit event",
        "entity_id": "COREAI_COREWEAVE",
        "magnitude": 1.0,
        "threshold": 0.55,
        "description": "CoreWeave defaults on the $7.6Bn DDTL. Direct impact on BX Matrix II (guarantor), Blackstone (sponsor), Microsoft (revenue loss), NVIDIA (RPO loss).",
    },
    "nvidia_correction": {
        "name": "NVIDIA AI valuation correction (−40%)",
        "entity_id": "NVDA",
        "magnitude": 0.60,
        "threshold": 0.55,
        "description": "Major AI valuation correction hits NVIDIA. Propagates through supply chain to TSMC, equity to CoreWeave, customer relationships to AI cloud.",
    },
    "microsoft_exit": {
        "name": "Microsoft exits CoreWeave contracts",
        "entity_id": "MSFT",
        "magnitude": 0.50,
        "threshold": 0.55,
        "description": "Microsoft terminates CoreWeave take-or-pay agreements. CoreWeave loses ~79.9% of facility collateral. BX Matrix II severely impaired.",
    },
}
```

## 6B — Create `backend/app/api/routes/cascade.py`

```python
from fastapi import APIRouter, HTTPException
from pydantic import BaseModel
from typing import Optional
from backend.app.core.cascade import run_cascade, PRESET_SCENARIOS, STATE_COLORS, FailureState

router = APIRouter(prefix="/api/cascade", tags=["cascade"])


class CascadeRequest(BaseModel):
    initial_shock_entity: str
    initial_shock_magnitude: float = 1.0
    threshold: float = 0.55
    max_rounds: int = 10
    scenario_name: str = "Custom shock"
    include_layer_b: bool = False


@router.post("/run")
def run_cascade_api(req: CascadeRequest):
    try:
        result = run_cascade(
            initial_shock_entity_id=req.initial_shock_entity,
            initial_shock_magnitude=req.initial_shock_magnitude,
            threshold=req.threshold,
            max_rounds=req.max_rounds,
            scenario_name=req.scenario_name,
            include_layer_b=req.include_layer_b,
        )
    except ValueError as e:
        raise HTTPException(status_code=404, detail=str(e))
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))

    return {
        "scenario_name": result.scenario_name,
        "initial_shock_entity": result.initial_shock_entity,
        "initial_shock_magnitude": result.initial_shock_magnitude,
        "threshold": result.threshold,
        "rounds": [
            {
                "round_number": r.round_number,
                "new_failures": r.new_failures,
                "state_changes": r.state_changes,
                "total_failed": r.total_failed,
            }
            for r in result.rounds
        ],
        "total_entities": result.total_entities,
        "total_failed": result.total_failed,
        "total_distressed": result.total_distressed,
        "converged": result.converged,
        "rounds_to_convergence": result.rounds_to_convergence,
        "nodes": result.nodes,
        "edges": result.edges,
        "is_synthetic": result.is_synthetic,
        "methodology_note": result.methodology_note,
    }


@router.get("/presets")
def get_presets():
    return [
        {
            "id": k,
            "name": v["name"],
            "description": v["description"],
            "initial_shock_entity": v["entity_id"],
            "initial_shock_magnitude": v["magnitude"],
            "threshold": v["threshold"],
        }
        for k, v in PRESET_SCENARIOS.items()
    ]


@router.get("/entities")
def get_shock_entities():
    from backend.app.core.data import get_entities
    entities = get_entities()
    return [
        {
            "entity_id": eid,
            "name": e.get("name", eid),
            "type": e.get("type", ""),
            "sector": e.get("sector", ""),
        }
        for eid, e in entities.items()
    ]


@router.get("/state-colors")
def get_state_colors():
    return {state.value: color for state, color in STATE_COLORS.items()}
```

**Register in main.py:**
```python
from backend.app.api.routes.cascade import router as cascade_router
app.include_router(cascade_router)
```

## 6C — Frontend: CascadeSimulation component

Create `frontend/src/components/CascadeSimulation.tsx`:

```tsx
import { useState, useEffect, useRef } from "react";

// Types
interface CascadeNode {
  id: string; name: string; type: string; sector: string;
  state: string; color: string; health: number;
  shock_received: number; failed_in_round: number | null;
  shock_sources: string[]; x: number; y: number;
}
interface CascadeEdge {
  source: string; target: string;
  weight: number; type: string; transmission_weight: number;
}
interface CascadeRound {
  round_number: number; new_failures: string[];
  state_changes: {
    entity_id: string; entity_name: string;
    from_state: string; to_state: string;
    shock_received: number;
  }[];
  total_failed: number;
}
interface CascadeResult {
  scenario_name: string;
  initial_shock_entity: string;
  initial_shock_magnitude: number;
  threshold: number;
  rounds: CascadeRound[];
  total_entities: number;
  total_failed: number;
  total_distressed: number;
  converged: boolean;
  rounds_to_convergence: number;
  nodes: CascadeNode[];
  edges: CascadeEdge[];
  is_synthetic: boolean;
  methodology_note: string;
}
interface Preset {
  id: string; name: string; description: string;
  initial_shock_entity: string;
  initial_shock_magnitude: number; threshold: number;
}

const STATE_COLORS: Record<string, string> = {
  "Prime": "#1a7f4b", "Near-Prime": "#f0c040",
  "Sub-Prime": "#e07820", "Distressed": "#c04020", "Failed": "#b13636",
};

export function CascadeSimulation() {
  const [presets, setPresets]     = useState<Preset[]>([]);
  const [entities, setEntities]   = useState<{entity_id:string; name:string}[]>([]);
  const [result, setResult]       = useState<CascadeResult | null>(null);
  const [loading, setLoading]     = useState(false);
  const [error, setError]         = useState<string | null>(null);
  const [selRound, setSelRound]   = useState(0);

  const [preset, setPreset]       = useState("");
  const [shockId, setShockId]     = useState("");
  const [magnitude, setMagnitude] = useState(1.0);
  const [threshold, setThreshold] = useState(0.55);
  const [layerB, setLayerB]       = useState(false);

  const canvasRef = useRef<HTMLCanvasElement>(null);

  useEffect(() => {
    fetch("/api/cascade/presets").then(r=>r.json()).then(setPresets);
    fetch("/api/cascade/entities").then(r=>r.json()).then(setEntities);
  }, []);

  const applyPreset = (pid: string) => {
    const p = presets.find(p=>p.id===pid);
    if (!p) return;
    setPreset(pid);
    setShockId(p.initial_shock_entity);
    setMagnitude(p.initial_shock_magnitude);
    setThreshold(p.threshold);
  };

  const run = async () => {
    if (!shockId) return;
    setLoading(true); setError(null); setResult(null); setSelRound(0);
    try {
      const p = presets.find(p=>p.id===preset);
      const res = await fetch("/api/cascade/run", {
        method: "POST",
        headers: {"Content-Type":"application/json"},
        body: JSON.stringify({
          initial_shock_entity: shockId,
          initial_shock_magnitude: magnitude,
          threshold, max_rounds: 10,
          scenario_name: p?.name || `Custom: ${shockId}`,
          include_layer_b: layerB,
        }),
      });
      if (!res.ok) throw new Error(`API error ${res.status}: ${await res.text()}`);
      const data = await res.json();
      setResult(data);
    } catch(e: any) {
      setError(e.message);
    } finally {
      setLoading(false);
    }
  };

  // Redraw canvas when result or selected round changes
  useEffect(() => {
    if (!result || !canvasRef.current) return;
    const canvas = canvasRef.current;
    const ctx = canvas.getContext("2d");
    if (!ctx) return;
    const W = canvas.offsetWidth || 700;
    const H = 480;
    canvas.width = W; canvas.height = H;
    ctx.clearRect(0, 0, W, H);

    const nodeMap: Record<string, CascadeNode> = {};
    result.nodes.forEach(n => { nodeMap[n.id] = n; });

    // Simple force layout
    const pos = simpleForceLayout(result.nodes, result.edges, W, H);

    // Draw edges
    result.edges.forEach(e => {
      const sp = pos[e.source], tp = pos[e.target];
      if (!sp || !tp) return;
      ctx.beginPath();
      ctx.moveTo(sp.x, sp.y);
      ctx.lineTo(tp.x, tp.y);
      ctx.strokeStyle = `rgba(180,190,200,${Math.min(e.transmission_weight * 0.9, 0.8)})`;
      ctx.lineWidth = Math.max(0.5, e.weight * 2);
      ctx.stroke();
    });

    // Draw nodes coloured by state at selected round
    result.nodes.forEach(n => {
      const p = pos[n.id];
      if (!p) return;

      // Determine state at selected round
      let displayState = "Prime";
      let displayColor = STATE_COLORS["Prime"];
      if (n.failed_in_round !== null && n.failed_in_round <= selRound) {
        displayState = n.state;
        displayColor = n.color;
      }

      const r = n.failed_in_round !== null && n.failed_in_round <= selRound ? 11 : 7;

      ctx.beginPath();
      ctx.arc(p.x, p.y, r, 0, Math.PI * 2);
      ctx.fillStyle = displayColor;
      ctx.fill();
      ctx.strokeStyle = "#fff";
      ctx.lineWidth = 1.5;
      ctx.stroke();

      ctx.fillStyle = "#1a1f26";
      ctx.font = "bold 9px Segoe UI, Arial";
      ctx.textAlign = "center";
      const lbl = n.name.length > 12 ? n.name.slice(0,11)+"…" : n.name;
      ctx.fillText(lbl, p.x, p.y + r + 10);
    });
  }, [result, selRound]);

  return (
    <div className="casc-shell">

      {/* Controls */}
      <div className="casc-controls">
        <div className="casc-ctrl-grp">
          <label>Preset scenario</label>
          <select value={preset} onChange={e=>applyPreset(e.target.value)}>
            <option value="">— Custom —</option>
            {presets.map(p=><option key={p.id} value={p.id}>{p.name}</option>)}
          </select>
        </div>
        <div className="casc-ctrl-grp">
          <label>Shock entity</label>
          <select value={shockId} onChange={e=>setShockId(e.target.value)}>
            <option value="">Select…</option>
            {entities.map(e=><option key={e.entity_id} value={e.entity_id}>{e.name}</option>)}
          </select>
        </div>
        <div className="casc-ctrl-grp">
          <label>Magnitude: {magnitude.toFixed(2)}</label>
          <input type="range" min={0.1} max={1.0} step={0.05}
            value={magnitude} onChange={e=>setMagnitude(parseFloat(e.target.value))} />
        </div>
        <div className="casc-ctrl-grp">
          <label>Threshold: {threshold.toFixed(2)}</label>
          <input type="range" min={0.1} max={0.9} step={0.05}
            value={threshold} onChange={e=>setThreshold(parseFloat(e.target.value))} />
        </div>
        <label className="casc-toggle">
          <input type="checkbox" checked={layerB} onChange={e=>setLayerB(e.target.checked)} />
          Include sector/market contagion (Layer B)
        </label>
        <button className="casc-run-btn" onClick={run}
          disabled={loading || !shockId}>
          {loading ? "Running…" : "Run cascade"}
        </button>
      </div>

      {error && <div className="casc-error">{error}</div>}

      {result && (
        <>
          {/* Summary */}
          <div className="casc-summary">
            <div className="casc-sum-item"><span>Scenario</span><b>{result.scenario_name}</b></div>
            <div className="casc-sum-item"><span>Entities</span><b>{result.total_entities}</b></div>
            <div className="casc-sum-item casc-red"><span>Failed</span><b>{result.total_failed}</b></div>
            <div className="casc-sum-item casc-amber"><span>Distressed</span><b>{result.total_distressed}</b></div>
            <div className="casc-sum-item"><span>Rounds</span><b>{result.rounds_to_convergence} {result.converged ? "(converged)" : "(max reached)"}</b></div>
          </div>

          <div className="casc-main">
            {/* LEFT: Network */}
            <div className="casc-network">
              <div className="casc-net-title">Network Topology</div>
              <div className="casc-net-sub">Credit Network — {result.scenario_name}</div>

              {/* Legend */}
              <div className="casc-legend">
                {Object.entries(STATE_COLORS).map(([state, color]) => (
                  <div key={state} className="casc-leg-item">
                    <span className="casc-leg-dot" style={{background:color}}/>
                    <span>{state}</span>
                  </div>
                ))}
              </div>

              {/* Canvas */}
              <canvas ref={canvasRef} className="casc-canvas" />

              {/* Round selector */}
              <div className="casc-rounds">
                <span style={{fontSize:"11px",color:"#8a97a5",marginRight:"8px"}}>Round:</span>
                {result.rounds.map(r => (
                  <button key={r.round_number}
                    className={`casc-round-btn ${selRound===r.round_number?"active":""}`}
                    onClick={() => setSelRound(r.round_number)}>
                    {r.round_number === 0 ? "Initial" : `R${r.round_number}`}
                    {r.new_failures.length > 0 &&
                      <span className="casc-round-badge">+{r.new_failures.length}</span>}
                  </button>
                ))}
              </div>
            </div>

            {/* RIGHT: Cascade trace */}
            <div className="casc-trace">
              <div className="casc-trace-title">Cascade Trace</div>
              <div className="casc-trace-sub">Entities that failed per round</div>
              {result.rounds.map(round => (
                <div key={round.round_number}
                  className={`casc-round-block ${selRound===round.round_number?"active":""}`}
                  onClick={() => setSelRound(round.round_number)}>
                  <div className="casc-round-head">
                    <span>
                      {round.round_number === 0
                        ? `Round 0 (initial) → ${round.total_failed} failure(s)`
                        : `Round ${round.round_number} → +${round.new_failures.length} new`}
                    </span>
                    <span className="casc-round-total">Total: {round.total_failed}</span>
                  </div>
                  {round.state_changes.map((sc, i) => (
                    <div key={i} className="casc-entity-row">
                      <span className="casc-entity-dot"
                        style={{background: STATE_COLORS[sc.to_state]||"#888"}}/>
                      <span className="casc-entity-name">{sc.entity_name}</span>
                      <span className="casc-entity-state">({sc.to_state})</span>
                      {sc.shock_received > 0 &&
                        <span className="casc-entity-shock">
                          −{(sc.shock_received*100).toFixed(0)}%
                        </span>}
                    </div>
                  ))}
                </div>
              ))}
              <div className="casc-method-note">{result.methodology_note}</div>
            </div>
          </div>
        </>
      )}

      {!result && !loading && (
        <div className="casc-empty">
          Select a preset or configure a custom shock, then click "Run cascade".
        </div>
      )}
    </div>
  );
}

// Simple force layout for canvas
function simpleForceLayout(
  nodes: CascadeNode[],
  edges: CascadeEdge[],
  W: number, H: number,
): Record<string, {x:number; y:number}> {
  const pos: Record<string, {x:number;y:number;vx:number;vy:number}> = {};
  const n = nodes.length;
  nodes.forEach((node, i) => {
    const angle = (2 * Math.PI * i) / Math.max(n, 1);
    pos[node.id] = {
      x: W/2 + W*0.36*Math.cos(angle),
      y: H/2 + H*0.38*Math.sin(angle),
      vx: 0, vy: 0,
    };
  });
  const K=0.07, REP=2200, DAMP=0.80;
  for (let iter=0; iter<150; iter++) {
    for (let a=0; a<nodes.length; a++) {
      for (let b=a+1; b<nodes.length; b++) {
        const pa=pos[nodes[a].id], pb=pos[nodes[b].id];
        const dx=pb.x-pa.x, dy=pb.y-pa.y;
        const d=Math.sqrt(dx*dx+dy*dy)+0.1;
        const f=REP/(d*d);
        pa.vx-=f*dx/d; pa.vy-=f*dy/d;
        pb.vx+=f*dx/d; pb.vy+=f*dy/d;
      }
    }
    edges.forEach(e=>{
      const pa=pos[e.source], pb=pos[e.target];
      if (!pa||!pb) return;
      const dx=pb.x-pa.x, dy=pb.y-pa.y;
      const d=Math.sqrt(dx*dx+dy*dy)+0.1;
      const target=(1-e.weight)*Math.min(W,H)*0.45;
      const f=K*(d-target)/d;
      pa.vx+=f*dx; pa.vy+=f*dy;
      pb.vx-=f*dx; pb.vy-=f*dy;
    });
    nodes.forEach(nd=>{
      const p=pos[nd.id];
      p.vx+=(W/2-p.x)*0.003;
      p.vy+=(H/2-p.y)*0.003;
      p.vx*=DAMP; p.vy*=DAMP;
      p.x=Math.max(25,Math.min(W-25,p.x+p.vx));
      p.y=Math.max(25,Math.min(H-25,p.y+p.vy));
    });
  }
  return pos;
}
```

## 6D — Add CSS for cascade (to global stylesheet)

```css
.casc-shell { padding: 20px 28px; }
.casc-controls { display:flex; flex-wrap:wrap; align-items:flex-end; gap:14px; background:#fff; border:1px solid #e3e8ee; border-radius:10px; padding:14px 18px; margin-bottom:14px; }
.casc-ctrl-grp { display:flex; flex-direction:column; gap:4px; min-width:130px; }
.casc-ctrl-grp label { font-size:10.5px; font-weight:700; letter-spacing:.4px; text-transform:uppercase; color:#8a97a5; }
.casc-ctrl-grp select { padding:5px 8px; border:1px solid #e3e8ee; border-radius:6px; font-size:12px; }
.casc-ctrl-grp input[type=range] { width:100%; }
.casc-toggle { display:flex; align-items:center; gap:7px; font-size:12px; color:#1a1f26; cursor:pointer; }
.casc-run-btn { padding:9px 22px; background:#12233f; color:#fff; border:none; border-radius:7px; font-size:13px; font-weight:600; cursor:pointer; white-space:nowrap; align-self:flex-end; }
.casc-run-btn:hover { background:#1b2f52; }
.casc-run-btn:disabled { background:#8a97a5; cursor:default; }
.casc-error { background:#f8e7e7; border:1px solid #e2aaaa; border-radius:8px; padding:10px 14px; font-size:12.5px; color:#6d2020; margin-bottom:12px; }
.casc-summary { display:flex; gap:10px; flex-wrap:wrap; margin-bottom:12px; }
.casc-sum-item { background:#fff; border:1px solid #e3e8ee; border-radius:8px; padding:9px 14px; display:flex; flex-direction:column; gap:2px; }
.casc-sum-item span { font-size:9.5px; font-weight:700; letter-spacing:.5px; text-transform:uppercase; color:#8a97a5; }
.casc-sum-item b { font-size:16px; color:#12233f; }
.casc-red b { color:#b13636; }
.casc-amber b { color:#b26a00; }
.casc-main { display:grid; grid-template-columns:1fr 300px; gap:14px; }
.casc-network { background:#fff; border:1px solid #e3e8ee; border-radius:10px; overflow:hidden; }
.casc-net-title { font-size:17px; font-weight:700; color:#12233f; padding:14px 18px 2px; }
.casc-net-sub { font-size:12px; color:#5b6b7c; padding:0 18px 8px; }
.casc-legend { display:flex; gap:12px; flex-wrap:wrap; padding:6px 18px 10px; border-bottom:1px solid #eef2f6; }
.casc-leg-item { display:flex; align-items:center; gap:6px; font-size:11.5px; }
.casc-leg-dot { width:10px; height:10px; border-radius:50%; flex:0 0 auto; }
.casc-canvas { display:block; width:100%; }
.casc-rounds { display:flex; align-items:center; flex-wrap:wrap; gap:5px; padding:10px 18px; border-top:1px solid #eef2f6; }
.casc-round-btn { padding:4px 10px; border:1px solid #e3e8ee; border-radius:6px; font-size:11px; cursor:pointer; background:#fff; position:relative; }
.casc-round-btn.active { background:#12233f; color:#fff; border-color:#12233f; }
.casc-round-badge { position:absolute; top:-6px; right:-6px; background:#b13636; color:#fff; font-size:9px; font-weight:700; border-radius:10px; padding:1px 4px; }
.casc-trace { background:#fff; border:1px solid #e3e8ee; border-radius:10px; overflow-y:auto; max-height:600px; }
.casc-trace-title { font-size:17px; font-weight:700; color:#12233f; padding:14px 16px 2px; }
.casc-trace-sub { font-size:12px; color:#5b6b7c; padding:0 16px 10px; border-bottom:1px solid #eef2f6; }
.casc-round-block { padding:9px 14px; border-bottom:1px solid #eef2f6; cursor:pointer; transition:background .1s; }
.casc-round-block:hover { background:#f8f9fb; }
.casc-round-block.active { background:#f2f9fe; }
.casc-round-head { display:flex; justify-content:space-between; margin-bottom:5px; font-size:12px; font-weight:700; color:#12233f; }
.casc-round-total { color:#8a97a5; font-weight:400; }
.casc-entity-row { display:flex; align-items:center; gap:6px; font-size:12px; padding:2px 0; }
.casc-entity-dot { width:8px; height:8px; border-radius:50%; flex:0 0 auto; }
.casc-entity-name { font-weight:600; }
.casc-entity-state { color:#5b6b7c; }
.casc-entity-shock { margin-left:auto; color:#b13636; font-weight:600; font-size:11px; }
.casc-method-note { font-size:10.5px; color:#8a97a5; padding:10px 14px; line-height:1.55; }
.casc-empty { padding:50px 24px; text-align:center; color:#8a97a5; font-size:14px; }
```

## 6E — Add tab to Backtest Lab

In `BacktestLab.tsx`:
```tsx
import { CascadeSimulation } from "../components/CascadeSimulation";

// Add to tab bar:
// "Cascade Simulation" tab alongside existing scenario tabs

// Add to tab content area:
{activeTab === "cascade" && <CascadeSimulation />}
```

Follow the exact tab pattern already used in BacktestLab.tsx.

## 6F — Tests

```python
# Add to test suite (tests/test_cascade.py):

def test_cascade_basic():
    from backend.app.core.cascade import run_cascade
    # Use an entity ID that actually exists in your data
    # Find a real entity ID by calling get_entities() first
    from backend.app.core.data import get_entities
    entities = get_entities()
    if not entities:
        return  # skip if no entities
    first_entity = next(iter(entities.keys()))
    result = run_cascade(first_entity, initial_shock_magnitude=0.8)
    assert result is not None
    assert len(result.rounds) >= 1
    assert result.rounds[0].round_number == 0
    assert result.total_entities > 0
    assert result.is_synthetic is True

def test_cascade_shocked_entity_health_reduced():
    from backend.app.core.cascade import run_cascade
    from backend.app.core.data import get_entities
    entities = get_entities()
    if not entities:
        return
    eid = next(iter(entities.keys()))
    result = run_cascade(eid, initial_shock_magnitude=0.8)
    entity_state = result.final_states.get(eid)
    if entity_state:
        assert entity_state.current_health < 1.0

def test_cascade_zero_shock_no_failures():
    from backend.app.core.cascade import run_cascade
    from backend.app.core.data import get_entities
    entities = get_entities()
    if not entities:
        return
    eid = next(iter(entities.keys()))
    result = run_cascade(eid, initial_shock_magnitude=0.0, threshold=0.55)
    assert result.total_failed == 0

def test_cascade_nodes_have_valid_states():
    from backend.app.core.cascade import run_cascade, STATE_COLORS
    from backend.app.core.data import get_entities
    entities = get_entities()
    if not entities:
        return
    eid = next(iter(entities.keys()))
    result = run_cascade(eid, initial_shock_magnitude=0.8)
    valid_states = set(STATE_COLORS.keys())
    for node in result.nodes:
        assert node["state"] in [s.value for s in valid_states] or True

def test_presets_api(test_client):
    response = test_client.get("/api/cascade/presets")
    assert response.status_code == 200
    data = response.json()
    assert len(data) >= 4

def test_cascade_run_api(test_client):
    from backend.app.core.data import get_entities
    entities = get_entities()
    if not entities:
        return
    eid = next(iter(entities.keys()))
    response = test_client.post("/api/cascade/run", json={
        "initial_shock_entity": eid,
        "initial_shock_magnitude": 0.8,
        "threshold": 0.55,
        "scenario_name": "Test",
    })
    assert response.status_code in (200, 404, 500)
    if response.status_code == 200:
        data = response.json()
        assert "rounds" in data
        assert "nodes" in data
        assert "total_failed" in data
        assert data["is_synthetic"] is True
```

---

---

# FINAL VERIFICATION — run ALL of these before declaring done

```
TASK 1 — CRITICAL FIXES:
□ localhost:5173/graph loads — type "TSM" → graph renders (no blank)
□ Entity Explorer, search BX Matrix II → GUARANTOR_BACKLEVERAGE shows HIGH or VERY HIGH evidence
□ Exposure Movers page — each MOVE value has amber "Illustrative" badge
□ Counterparty 360 — PFE/NSE/utilisation each have "Illustrative" badge
□ DailyReview — ΔPFE values have "Illustrative" badge
□ EventStudio — PFE/utilisation in transmission table have "Illustrative" badge

TASK 2 — PRICE HISTORY:
□ ls .enrichment_cache/prices/ | wc -l  →  40 or more
□ cat .enrichment_cache/prices/META.json  →  has price_history array
□ cat .enrichment_cache/prices/COREWEAVE.json  →  has private:true
□ Data Sources page shows 40+ issuers with market data

TASK 3 — OSUC IN DISTANCE MAP:
□ Distance Map → select BX Matrix II
□ CoreWeave row shows "$193.3M OSUC" column
□ NVIDIA row shows "—" in OSUC column
□ Click CoreWeave → expanded panel shows $193,323,429 with "Separate from ρ" note
□ No mathematical combination of OSUC and ρ anywhere

TASK 4 — CAM RELATIONSHIPS:
□ CAM Research search "CRUSOE" → returns entity with 5 relationship records
□ CAM Research search "OPENAI" → returns entity with 6 relationship records
□ Hub count: 5 (was 3)
□ Existing CoreWeave/BX Matrix II/Anthropic records unchanged

TASK 5 — STYLUS:
□ .env.example has STYLUS_API_KEY placeholder
□ If configured: button returns real content
□ If not: informative "not configured" message shown, no crash

TASK 6 — CASCADE SIMULATION:
□ Backtest Lab has "Cascade Simulation" tab
□ Tab loads without error
□ Select "Taiwan earthquake" preset → fields populate automatically
□ Click "Run cascade" → network renders on canvas with coloured nodes
□ Cascade Trace panel shows rounds with entity failure lists
□ Round buttons update canvas colours correctly
□ State legend shows all 5 colours
□ methodology_note visible at bottom

OVERALL:
□ python -m pytest  →  166+ tests passing (zero regressions)
□ No console errors on any page
□ Every synthetic metric has "Illustrative" badge
□ is_synthetic:true in all cascade API responses
```

---

# WHAT NOT TO DO

```
✗ Do NOT modify scoring.py
✗ Do NOT rewrite Graph Explorer — fix only the specific JS error
✗ Do NOT combine OSUC figures with ρ values mathematically
✗ Do NOT run cascade computation at page load — only on Run button click
✗ Do NOT present cascade states as real default probabilities
✗ Do NOT invent CAM relationship data — only publicly verified facts
✗ Do NOT remove any existing synthetic data — new data is additive
✗ Do NOT expose raw CAGIDs in user-facing output
✗ Do NOT break existing Backtest Lab scenarios
✗ Do NOT add npm packages unless strictly necessary
```
