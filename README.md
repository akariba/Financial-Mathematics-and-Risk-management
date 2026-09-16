# CCRIG — Complete Task Backlog
## All improvements identified across all rounds
## Ala-Eddine Karib, ICM First Line of Defense

---

## HOW TO READ THIS

Each task has:
- **What:** exactly what to build
- **Why:** what decision or capability it unlocks
- **Depends on:** what must exist first
- **Effort:** S (hours) / M (1-2 days) / L (3-5 days) / XL (week+)
- **Data needed:** what data source is required

Priority tiers:
- 🔴 CRITICAL — broken or missing something that blocks the demo
- 🟠 HIGH — significant value, no blockers
- 🟡 MEDIUM — good improvement, some dependency
- 🟢 LATER — valid but not urgent

---

# TIER 1 — CRITICAL (fix first)

## T1.1 — Fix Graph Explorer blank page
**What:** `/graph` loads blank. Open browser console, find the JS error, fix only that specific error. Do not rewrite the renderer.
**Why:** Only broken page in the tool. Embarrassing in a demo.
**Depends on:** Nothing — just find and fix the error
**Effort:** S
**Data needed:** None

## T1.2 — Fix LOW EVIDENCE badge on GUARANTOR_BACKLEVERAGE
**What:** BX Matrix II → CoreWeave shows LOW EVIDENCE despite source being "BX Matrix II CAM; SEC 10-K/10-Q" — two independent sources. The confidence-to-evidence mapping in the HTML parser is broken. Fix the mapping so CAM + SEC → HIGH, CAM + SEC + News → VERY HIGH, CAM only → MEDIUM, CAM never → LOW.
**Why:** A credit officer seeing LOW EVIDENCE on the core structural relationship of a $435M facility will distrust everything else the tool shows.
**Depends on:** Nothing
**Effort:** S
**Data needed:** None — fix is in parsing logic

## T1.3 — Wire "Illustrative" badges to 4 frontend files
**What:** The `metric_provenance` field already exists in `ccr_priority.py:46-52` but PFE/NSE/utilisation/ΔPFE render without the "Illustrative" label in:
- `DailyReview.tsx:140-145`
- `Counterparty360.tsx:420-423`
- `ExposureMovers.tsx:70-81`
- `EventStudio.tsx:137-155`

Add a small amber badge "Illustrative" next to every synthetic metric. One component, used in four places.
**Why:** Without it, any external viewer reads PFE numbers as real. Governance risk.
**Depends on:** Nothing
**Effort:** S
**Data needed:** None

---

# TIER 2 — HIGH VALUE, NO BLOCKERS

## T2.1 — Extend price history from 14 to 40+ entities
**What:** Run existing Yahoo Finance fetcher for: GOOGL, AMZN, META, AVGO, QCOM, ARM, MU, AMAT, INTC, Samsung (005930.KS), BX, CG, JPM, C, GS, MS, CORZ, RTX, LMT, NOC, GD, BA, XOM, SHEL, BP, CVX, RIO, FCX, MAERSK-B.CO. Mark private companies (CoreWeave, Anthropic, OpenAI, Mistral) explicitly as `{"private": true, "price_history": null}`.
**Why:** Historical Correlation channel in Distance Map currently uses sector/news proxy. Real Pearson correlations from price history make the ρ values more accurate.
**Depends on:** Nothing — fetcher already works
**Effort:** S
**Data needed:** Yahoo Finance (public, free, already implemented)

## T2.2 — Join OSUC exposure to Distance Map issuer rows
**What:** Add one column to each issuer row in the Distance Map: `$193.3M OSUC` where the issuer is a Masterfile obligor, `—` where it is not. Show in both the row header and the expanded detail panel. Never mathematically combine with ρ.
**Why:** Answers MJ's exact question ("how much is Citi exposed to OpenAI") in the same view as the correlation. Highest demo value of any single change.
**Depends on:** OSUC lookup already works in coreai.py
**Effort:** M
**Data needed:** Masterfile (already loaded)

## T2.3 — Add Crusoe Inc CAM relationships
**What:** Add Crusoe Inc (CAGID 1040287325, TFA ~$739M — largest CoreAI exposure) to the CAM relationship matrix. Known relationships: NVIDIA (Supplier/Customer), Andreessen Horowitz (Equity Investor), Stripe (Select Customer), Flatiron Capital (Lender). Hub count 3→4.
**Why:** Largest CoreAI exposure with no relationship data. Gap in the most important part of the tool.
**Depends on:** CAM ingestion pipeline (already exists)
**Effort:** S
**Data needed:** Public sources only — no additional CAM needed for this

## T2.4 — Add OpenAI CAM relationships
**What:** Add OpenAI OPCO LLC (CAGID 9008833883, TFA ~$519M) to the CAM relationship matrix. Known relationships: Microsoft (Strategic Investor/Partner, $13Bn+), CoreWeave (Customer + Equity, $22.4Bn), NVIDIA (Supplier), SoftBank (Investor, $15Bn committed), Apple (Enterprise Partner). Hub count 4→5.
**Why:** Second largest CoreAI exposure. OpenAI is referenced in multiple existing CAM records as a customer of CoreWeave — it should be a hub in its own right.
**Depends on:** CAM ingestion pipeline
**Effort:** S
**Data needed:** Public sources — all figures above are publicly confirmed

## T2.5 — Real news via R2D2 web search for Theme Radar
**What:** When a theme is selected in the Theme Radar, add a "Refresh from R2D2" button that calls the R2D2 web-search endpoint for each covered entity in the theme (max 5 entities, 3 headlines each). Replace SYNTHETIC-tagged evidence with real results. Tag source as `R2D2_LIVE_WEB`.
**Why:** All 34 synthetic news documents show SYNTHETIC tag in evidence panel. Real headlines make the radar credible in a demo.
**Depends on:** R2D2 live web search scope being active
**Effort:** M
**Data needed:** R2D2 web search (check if token has this scope)

## T2.6 — Activate Stylus for real SEC content
**What:** The "Run SEC + Web Assessment" button exists in CAM Research but returns auth error. Find the STYLUS_API_KEY environment variable, configure it, verify the Stylus handler returns real SEC filing excerpts and web assessment per company.
**Why:** Real SEC content (10-K business descriptions, risk factors, concentration disclosures) is the highest-quality evidence the tool can show. For CoreWeave, the S-1 contains exactly the concentration risk data (Microsoft ~79.9%) the tool surfaces from the CAM.
**Depends on:** Stylus credential (ask same colleague as CCR data)
**Effort:** S (once credential obtained)
**Data needed:** Stylus API key

## T2.7 — Expand GLEIF to full CoreAI population
**What:** Currently 40/43 entities have GLEIF LEI data. Run GLEIF fetcher for remaining 3 plus all new entities added (Crusoe, OpenAI, any new counterparties). Prioritise entities where GLEIF Level-2 would reveal parent/subsidiary relationships not in the CAM.
**Why:** GLEIF Level-2 is the ownership layer of the Distance Map. More coverage = more accurate ownership correlation channel.
**Depends on:** Nothing — GLEIF fetcher already works, just re-run
**Effort:** S
**Data needed:** GLEIF API (public, free, already implemented)

## T2.8 — Exposure-weighted Theme Radar bubbles
**What:** Currently bubble size = distinct counterparty count. Change to bubble size = Σ TFA of counterparties exposed to the theme. So AI theme bubble size reflects total TFA of the 17 exposed counterparties, not just 17 as a count.
**Why:** Makes the radar immediately show portfolio concentration in financial terms, not just entity counts. A theme that touches 3 counterparties with $2Bn TFA each matters more than one that touches 17 counterparties at $50M each.
**Depends on:** Counterparty TFA data (from Masterfile, already loaded)
**Effort:** M
**Data needed:** Masterfile TFA figures (already in system)

---

# TIER 3 — MEDIUM VALUE, SOME DEPENDENCY

## T3.1 — Replace synthetic counterparty names with real CCR entities
**What:** When CCR counterparty list is obtained (CAGID, name, product types), replace the 18 fictional wrappers (Sovereign Debt Office Nation Alpha, Meridian Alpha Rates Fund, etc.) with real named entities. Synthetic PFE/utilisation numbers stay but are now attached to real names.
**Why:** Makes the Inbox, Exposure Movers, Counterparty 360, Theme Radar all show real counterparty names. Transforms the tool from POC to real book intelligence.
**Depends on:** CCR counterparty list from colleague
**Effort:** M
**Data needed:** CCR counterparty list (pending colleague response)

## T3.2 — R2D2 price history (Bloomberg quality)
**What:** Route price history fetching through R2D2 Bloomberg data instead of Yahoo Finance. Higher quality, split/dividend adjusted, inside data perimeter. Keep Yahoo Finance as fallback.
**Why:** Bloomberg-grade data is appropriate for internal risk presentations. Yahoo Finance is adequate for POC but not for anything going to a committee.
**Depends on:** R2D2 market data scope confirmation
**Effort:** M
**Data needed:** R2D2 with market data scope

## T3.3 — SVB regional bank funding stress backtest scenario
**What:** Implement the "Regional bank funding stress after a major bank failure (SVB-style)" scenario that currently returns 400 Bad Request. The scenario: March 8-10 2023, data cutoff T0 = March 8 2023. Affected entities: SVB Financial Group, Signature Bank, First Republic, PacWest, Western Alliance, Silvergate. Test whether the Distance Map's financial-sector hidden correlation (ρ ~0.38 for Trireme Shipping Finance ↔ HSBC/Deutsche Bank/JPM) would have surfaced these as a connected cluster before the event.
**Why:** This is the most compelling backtest you can run. If the tool surfaces regional bank stress contagion from hidden correlation before the event, it proves the methodology works on a real historical case.
**Depends on:** Backtest Lab framework (already exists for Taiwan earthquake)
**Effort:** L
**Data needed:** Public price history around March 2023 (Yahoo Finance covers this)

## T3.4 — 2011 Japan earthquake supply-chain backtest
**What:** Implement the third backtest scenario. T0 = March 11 2011. Tests whether the supply-chain correlation channel (TSMC → NVIDIA → AMD path) would have surfaced semiconductor names as affected before market reaction. Measures Precision@K and Recall@K against realised price moves.
**Why:** Validates the supply chain correlation channel specifically. Complements the Taiwan 2026 earthquake scenario already implemented.
**Depends on:** Backtest Lab framework
**Effort:** L
**Data needed:** Yahoo Finance historical data back to 2011 (available)

## T3.5 — CAM-path-sourced theme assignment
**What:** Replace generic TF-IDF theme→entity assignment with CAM-sourced theme→entity assignment. When the AI theme fires on NVIDIA, trace through the CAM graph: NVIDIA → CoreWeave (supplier) → BX Matrix II (guarantor) → all counterparties with BX Matrix II exposure. The "17 counterparties exposed" becomes "17 counterparties exposed through a sourced typed path from the triggering entity."
**Why:** Turns the Theme Radar from a news dashboard into a genuine CCR early-warning system. The transmission chain becomes explicit and auditable.
**Depends on:** Real counterparty names (T3.1) for full value
**Effort:** L
**Data needed:** CAM relationship matrix (already loaded)

## T3.6 — Distance Map bubble/matrix view
**What:** Add two additional tabs to the Distance Map alongside the current ranked-list view: (1) a heat-matrix showing all counterparties × all issuers as a colour-coded grid, (2) a force-directed bubble map where physical distance encodes ρ. Reference: the standalone HTML artifact at https://claude.ai/artifact/Nh86oq7hSsU8wo2H9Ld85j
**Why:** The matrix view lets a portfolio manager see concentration across the whole book at a glance. The bubble map shows clustering visually. Both views are built — they just need to be wired to the real API instead of hardcoded data.
**Depends on:** Distance Map API already working
**Effort:** M
**Data needed:** None — distance API already returns all needed data

## T3.7 — Export functionality from Counterparty 360
**What:** Add "Export to CAM Report" button to Counterparty 360. Generates a structured HTML or PDF containing: counterparty name/CAGID, exposure summary (PSLE net, facility breakdown), key risk clusters (relationship clusters from Relationships tab), top related entities with ρ and typed paths, active controls/breaches, decision recommendation. Include "SYNTHETIC POC DATA" watermark.
**Why:** MJ's original feature request #3. UW reviewing a CoreAI name should be able to export a report for their CAM workflow.
**Depends on:** Counterparty 360 working (already does)
**Effort:** M
**Data needed:** None — all data already in the page

## T3.8 — Export from CoreAI Network / Relationships filter
**What:** Add "Export filtered view" CSV button to the CAM relationship database. Downloads currently filtered records: Company A, Company B, Type, Relationship, Amount, Source, Confidence, OSUC exposure context.
**Why:** MJ's original feature request #3. Analyst should be able to export the filtered relationship view for a specific company.
**Depends on:** CAM relationship database (already working)
**Effort:** S
**Data needed:** None

## T3.9 — Inbox ranked by real materialised exposure
**What:** Currently the Inbox ranks counterparties by synthetic ΔPFE/utilisation. Once real OSUC data is joined (T2.2), the ranking should incorporate real exposure magnitude — a counterparty with $519M OSUC and a market move should rank above one with $50M OSUC and the same market move.
**Why:** Makes the investigation queue actually reflect portfolio materiality, not arbitrary synthetic numbers.
**Depends on:** T2.2 (OSUC in Distance Map) + T3.1 (real counterparty names)
**Effort:** M
**Data needed:** Masterfile OSUC (already loaded)

## T3.10 — Add more real news headlines (50+ target)
**What:** Currently 14 real / 34 synthetic. Target: 50+ real, synthetic kept as fallback only. For each CoreAI entity, find 3-5 verified real public headlines (Reuters, Bloomberg, FT, CNBC, WSJ, White House, SEC.gov). Tag source_type=REAL_PUBLIC_NEWS, is_synthetic=false, with source URL.
**Why:** Theme Radar evidence panel shows SYNTHETIC tags on all visible headlines. Real headlines make the radar credible.
**Depends on:** Either R2D2 web search (T2.5) or manual curation
**Effort:** M if manual, S if R2D2 web search works
**Data needed:** R2D2 web search or manual research

---

# TIER 4 — LATER (valid but not urgent now)

## T4.1 — Rank/Spearman correlation replacing Pearson
**What:** Replace the Pearson correlation in the market_positive/market_negative scoring components with Spearman rank correlation. More robust to fat tails and non-linear relationships — which describes financial returns almost universally.
**Why:** Methodologically correct improvement. Finance returns are not normally distributed.
**Depends on:** More price history (T2.1) to make it meaningful
**Effort:** S
**Data needed:** Price history (T2.1)

## T4.2 — Dynamic Conditional Correlation (DCC-GARCH) for market component
**What:** Replace static Pearson in the market correlation component with DCC-GARCH, allowing correlation to vary over time. Show the time-varying correlation chart in Entity Explorer.
**Why:** Captures the empirical fact that correlations jump during volatile periods. Critical for stress scenarios.
**Depends on:** T2.1 (price history) + significant historical data
**Effort:** XL
**Data needed:** Long price history (10+ years for meaningful GARCH estimation)

## T4.3 — Tail dependence / copula correlation
**What:** Compute lower tail dependence coefficient λL between entity pairs using a Clayton copula fitted to historical return pairs. Display alongside the linear ρ in Entity Explorer.
**Why:** Standard correlation misses the empirical fact that assets crash together more than they rally together. Tail dependence is the most important correlation type for CCR stress scenarios.
**Depends on:** T2.1 + T4.1 + significant price history
**Effort:** XL
**Data needed:** Long price history, option market data for calibration

## T4.4 — Wrong-Way Risk quantification
**What:** Add a WWR diagnostic that computes the joint conditional distribution of exposure and counterparty credit quality. Flag specific pairs where exposure increases when counterparty credit deteriorates. Show as a structured finding in Counterparty 360 Decision tab.
**Why:** WWR is the most directly capital-relevant correlation type in CCR. Currently only flagged qualitatively in the tool.
**Depends on:** Real CCR counterparty data (T3.1) + production exposure engine access
**Effort:** XL
**Data needed:** Production PFE engine (not currently accessible)

## T4.5 — DebtRank network contagion propagation
**What:** Implement DebtRank (Battiston et al. 2012) shock-propagation on the exposure graph. When a hub entity (CoreWeave) experiences a stress, propagate the loss through the network weighted by exposure amounts. Show which counterparties are reachable within 1, 2, 3 hops and with what residual impact.
**Why:** Network/systemic correlation — the correlation type that arises from the structure of the financial network itself rather than any pairwise relationship. Only visible once the graph exists.
**Depends on:** Real exposure edges (not synthetic), T3.1
**Effort:** XL
**Data needed:** Real exposure amounts per edge — requires CCR + lending data joined

## T4.6 — Concentration limits and headroom alerts
**What:** For each theme in the Theme Radar, add a configurable exposure-concentration limit. When total TFA of counterparties exposed to a theme exceeds the limit, fire an alert in the Inbox. E.g. "AI theme total exposure: $1.2Bn — exceeds $1Bn concentration guideline."
**Why:** Turns the Theme Radar from a monitoring tool into a limit-management tool. Directly supports the CCR portfolio management workflow.
**Depends on:** T2.8 (exposure-weighted bubbles) + T3.1 (real counterparties)
**Effort:** M
**Data needed:** Masterfile TFA + counterparty TFA (already loaded)

## T4.7 — Counterparty grouping by GFCID
**What:** Add "Group by GFCID/economic group" toggle to the Inbox and Counterparty 360. When active, aggregate synthetic PFE across all counterparties in the same economic group (e.g. all BX Matrix II entities grouped under Blackstone). Show group-level total exposure alongside individual counterparty rows.
**Why:** MJ's original feature request #1. "We should be able to see all combined exposures for a grouping — how much is Citi's exposure related to OpenAI for example."
**Depends on:** GLEIF Level-2 ownership data (T2.7) + real counterparty names (T3.1)
**Effort:** L
**Data needed:** GLEIF Level-2 + real GFCID/CAGID from CCR data

## T4.8 — MSc thesis documentation
**What:** Document the CCRIG architecture, the three-layer data model, the candidate-generation pipeline, the Distance Map methodology, and the backtest results in a form suitable for the MSc thesis at WWSI. Include the Sybil Radar / CCRIG comparison as a case study in applied graph-based risk intelligence.
**Why:** The work done here is genuinely novel — sparse graph + typed multi-layer edges + explainable distance-based correlation inference applied to CCR. Worth documenting academically.
**Depends on:** Current build being stable
**Effort:** XL (writing, not coding)
**Data needed:** None — uses what exists

---

# SUMMARY TABLE

| ID | Task | Tier | Effort | Depends on |
|---|---|---|---|---|
| T1.1 | Fix Graph Explorer blank | 🔴 CRITICAL | S | Nothing |
| T1.2 | Fix LOW EVIDENCE badge | 🔴 CRITICAL | S | Nothing |
| T1.3 | Wire Illustrative badges (4 files) | 🔴 CRITICAL | S | Nothing |
| T2.1 | Extend price history 14→40+ | 🟠 HIGH | S | Nothing |
| T2.2 | OSUC in Distance Map rows | 🟠 HIGH | M | Nothing |
| T2.3 | Add Crusoe CAM relationships | 🟠 HIGH | S | Nothing |
| T2.4 | Add OpenAI CAM relationships | 🟠 HIGH | S | Nothing |
| T2.5 | Real news via R2D2 web search | 🟠 HIGH | M | R2D2 web scope |
| T2.6 | Activate Stylus SEC content | 🟠 HIGH | S | Stylus credential |
| T2.7 | GLEIF full population | 🟠 HIGH | S | Nothing |
| T2.8 | Exposure-weighted Theme bubbles | 🟠 HIGH | M | Nothing |
| T3.1 | Real CCR counterparty names | 🟡 MEDIUM | M | CCR list from colleague |
| T3.2 | R2D2 Bloomberg price history | 🟡 MEDIUM | M | R2D2 market data scope |
| T3.3 | SVB backtest scenario | 🟡 MEDIUM | L | Nothing |
| T3.4 | 2011 Japan earthquake backtest | 🟡 MEDIUM | L | Nothing |
| T3.5 | CAM-path theme assignment | 🟡 MEDIUM | L | T3.1 for full value |
| T3.6 | Distance Map matrix + bubble view | 🟡 MEDIUM | M | Nothing |
| T3.7 | Export from Counterparty 360 | 🟡 MEDIUM | M | Nothing |
| T3.8 | Export from Relationships filter | 🟡 MEDIUM | S | Nothing |
| T3.9 | Inbox ranked by real OSUC | 🟡 MEDIUM | M | T2.2 + T3.1 |
| T3.10 | 50+ real news headlines | 🟡 MEDIUM | M | R2D2 or manual |
| T4.1 | Spearman replacing Pearson | 🟢 LATER | S | T2.1 |
| T4.2 | DCC-GARCH market correlation | 🟢 LATER | XL | T2.1 |
| T4.3 | Tail dependence / copula | 🟢 LATER | XL | T2.1 + T4.1 |
| T4.4 | WWR quantification | 🟢 LATER | XL | T3.1 + production engine |
| T4.5 | DebtRank network contagion | 🟢 LATER | XL | T3.1 + real exposure |
| T4.6 | Theme concentration limits | 🟢 LATER | M | T2.8 + T3.1 |
| T4.7 | GFCID grouping | 🟢 LATER | L | T2.7 + T3.1 |
| T4.8 | MSc thesis documentation | 🟢 LATER | XL | Stable build |

**Total tasks: 28**
**Can do today with no dependencies: T1.1, T1.2, T1.3, T2.1, T2.2, T2.3, T2.4, T2.7, T3.6, T3.7, T3.8**
**That is 11 tasks — a full sprint of work — before needing anything from anyone.**
