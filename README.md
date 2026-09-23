LENDING RELATIONSHIP INTELLIGENCE
PROMPT 3B — CANONICAL CONTRACT ACCEPTANCE AND TRUSTED-READ VERIFICATION

Continue in the CURRENT Lending repository.

This is a READ-ONLY / TEST-ONLY verification of Prompt 3.

Do not redesign the UI.
Do not create new architecture.
Do not change relationship policy unless an actual Prompt-3 defect is proven.
Do not perform CCR or customer-master work.
Do not call SEC, web, Stylus, or external providers.

Use as authoritative inputs:

- LENDING_FOUNDATION_AUDIT.md
- LENDING_CANONICAL_RELATIONSHIP_CONTRACT_REPORT.md
- the Prompt-3 implementation
- the existing benchmark/golden-sample fixtures

OBJECTIVE

Verify that the new common relationship contract and unified Lending read
model are semantically safe before the executive UI, network visualization,
external-intelligence automation, and AI assistant are built on top of it.

The Prompt-3 completion reported a trusted read of:

808 total
41 CAM_V3
767 NORMALIZED_JSON

Explain and prove exactly what those numbers mean.

==================================================
1. TRUSTED READ COMPOSITION
==================================================

Inspect the default unified trusted read.

Report exact counts by:

- source_lane
- authority_class
- quality_status
- review_status
- publication_status
- relationship_family
- relationship_type
- state
- connectivity

Specifically prove whether the 767 NORMALIZED_JSON rows are:

- validated/canonical only
- review-required
- rejected
- or a mixture

The default trusted read MUST NOT silently include rejected normalized rows.

If review-required rows are included, explain the declared policy and why.

==================================================
2. CROSS-LANE DUPLICATION
==================================================

Determine how many of the 808 assertions represent the same semantic
real-world relationship in more than one source lane.

Compute and report:

A. total relationship assertions
B. distinct source relationship IDs
C. distinct semantic relationship groups
D. distinct endpoint pairs
E. endpoint pairs with multiple relationship types
F. semantic groups supported by multiple source lanes
G. exact duplicate assertions, if any

Do NOT delete legitimate multi-source assertions.

We need to distinguish:

SOURCE ASSERTION COUNT

from

DISPLAY RELATIONSHIP COUNT.

==================================================
3. DISPLAY GROUPING CONTRACT
==================================================

Verify that the implementation has a safe way for a future UI to render:

one semantic relationship
    +
multiple source assertions/evidence lanes

without losing provenance.

For a semantic group expose, at minimum:

- display/group key
- subject
- related entity
- atomic relationship type
- direction
- state
- source lanes supporting it
- authority classes
- assertion count
- evidence count
- independent source count where meaningful
- conflict indicator
- review indicator

If the backend does not currently expose such grouping, DO NOT implement a
large redesign.

Instead identify the smallest required addition for Prompt 4.

==================================================
4. AUTHORITY VERIFICATION
==================================================

Prove the authority semantics for each active lane.

Expected conceptual behavior:

CAM_V3
    authoritative CAM assertion

NORMALIZED_CAM / NORMALIZED_JSON
    governed derived assertion

EXTERNAL
    supplemental

AI_PUBLISHED
    governed AI assertion

V2_FALLBACK
    compatibility fallback only

Verify that no normalized/external/AI operation can silently overwrite or
masquerade as CAM authority.

==================================================
5. V2 VERIFICATION
==================================================

Prove that V2 remains conditional.

Report:

- whether V2 rows appear in the default global trusted read
- whether they can appear only for client-specific fallback
- how the source lane is labelled
- whether a client with V3 relationships can accidentally receive V2 rows

Expected result:

V2 is NOT a global relationship universe.

==================================================
6. REVIEW / REJECTED VERIFICATION
==================================================

Verify separately:

- CAM V3 canonical
- CAM V3 review-required
- normalized validated
- normalized review-required
- normalized rejected
- external pending/review/conflict
- AI draft
- AI published

State which are visible in:

A. default trusted relationship read
B. explicit review read
C. relationship detail
D. network-ready read

No lifecycle state may be silently promoted.

==================================================
7. LINEAGE VERIFICATION
==================================================

Select examples representing:

- fully persisted new lineage
- historical incomplete lineage
- taxonomy substitution
- entity-resolution issue
- evidence-gate failure
- direction/state issue
- multi-source semantic relationship

For each show the actual returned lineage.

Prove that missing historical stages return an explicit:

LINEAGE_INCOMPLETE

or equivalent.

The implementation must not manufacture intermediate history.

==================================================
8. BENCHMARK TRACES
==================================================

Run the common-contract/detail/lineage APIs against available benchmark
cases including:

- Lambda / NVIDIA
- Project Indigo / CoreWeave
- Applied Digital / CoreWeave
- Serverfarm / Meta
- BO Westover / Blue Owl
- OpenAI relationship cases
- Hut 8
- Cavalry / CyrusOne

For every case report:

- endpoint identity
- relationship type
- source lane
- authority
- review status
- taxonomy mapping if any
- evidence availability
- lineage completeness
- whether it would appear in default trusted read
- whether it would appear in a future grouped display

Do not change benchmark truth.

==================================================
9. EXPLAINABILITY RESPONSE
==================================================

Call the new relationship-detail/read logic directly for representative
records.

Confirm that a future frontend can answer:

WHY AM I SEEING THIS RELATIONSHIP?

using one response or a deterministic linked response set.

Verify availability of:

- identity
- relationship semantics
- authority
- source lane
- source documents
- source location
- representative evidence/excerpt where available
- evidence count
- quality/review status
- entity-resolution state
- taxonomy-resolution state
- lineage
- conflict
- supporting source assertions

Clearly identify any field that remains unavailable.

Do not synthesize missing facts.

==================================================
10. NETWORK SAFETY CHECK
==================================================

Before Prompt 4 builds a sophisticated graph, report what the graph should
use as:

NODE IDENTITY

EDGE ASSERTION IDENTITY

EDGE DISPLAY/GROUP IDENTITY

EDGE STRENGTH / SUPPORT METRICS

Do not implement visualization yet.

Specifically explain how the network should avoid:

- duplicate edges caused only by multiple source lanes
- collapsing supplier and strategic-partner semantics
- collapsing parent and guarantor semantics
- turning review-required relationships into accepted facts
- making external proposals look like CAM facts
- making AI relationships look like CAM facts

==================================================
11. EXECUTIVE COUNT CONTRACT
==================================================

Define which numbers future executive cards should display.

Distinguish:

relationship assertions
semantic relationships
connected entities
relationships requiring review
externally corroborated relationships
external proposals
conflicts
AI-published relationships

Never place different denominators under one label.

==================================================
12. OUTPUT
==================================================

Create:

LENDING_PROMPT3_ACCEPTANCE_REPORT.md

Include:

1. trusted-read composition
2. exact 808-row explanation
3. source/assertion/group counts
4. duplicate and multi-source analysis
5. authority verification
6. V2 verification
7. review/rejection verification
8. lineage verification
9. benchmark traces
10. explainability readiness
11. network identity recommendations
12. executive count contract
13. remaining Prompt-3 defects, if any
14. blockers for Prompt 4
15. PASS / PASS WITH CONDITIONS / FAIL readiness conclusion

Do not alter the UI.

If a genuine Prompt-3 implementation defect is discovered, document it
rather than silently redesigning the architecture.

At the end STOP.
