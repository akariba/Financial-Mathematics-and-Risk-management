LENDING RELATIONSHIP INTELLIGENCE
PROMPT 3C — CLOSE PROMPT-4 BLOCKERS

Continue in the CURRENT Lending repository.

Read first:

LENDING_FOUNDATION_AUDIT.md
LENDING_CANONICAL_RELATIONSHIP_CONTRACT_REPORT.md
LENDING_PROMPT3_ACCEPTANCE_REPORT.md

Also inspect the implementation produced by Prompt 3.

This task exists ONLY because Prompt 3B concluded:

PASS WITH CONDITIONS

Do not redesign the UI.
Do not start Prompt 4 visual work.
Do not perform CCR/customer-master work.
Do not call SEC, web, Stylus, or external providers.
Do not rebuild the architecture.
Do not change CAM/V3 source truth.
Do not broaden V2 into a global relationship universe.

OBJECTIVE

Resolve only the conditions/blockers identified in
LENDING_PROMPT3_ACCEPTANCE_REPORT.md that prevent the common Lending
relationship contract from safely supporting:

- executive relationship counts
- semantic relationship grouping
- network visualization
- explainability
- future external intelligence
- future AI interaction

The goal is NOT to increase relationship counts.

The goal is to make the existing common contract semantically safe and
unambiguous for Prompt 4.

==================================================
1. EXTRACT THE CONDITIONS
==================================================

From LENDING_PROMPT3_ACCEPTANCE_REPORT.md, list every reason the result was
PASS WITH CONDITIONS.

Classify each one as:

A. MUST FIX BEFORE PROMPT 4
B. SAFE TO DEFER
C. INFORMATIONAL ONLY

For each condition provide:

- problem
- affected API/store/model
- consequence if not fixed
- proposed smallest safe remediation

Do not implement anything until this classification is complete.

==================================================
2. SEMANTIC RELATIONSHIP GROUPING
==================================================

The acceptance report identified relationship assertions and endpoint-pair
reconciliation.

We now need a stable distinction between:

SOURCE ASSERTION

and

SEMANTIC DISPLAY RELATIONSHIP.

Do NOT delete or overwrite source assertions.

Implement the minimum safe grouping capability required for a future UI.

A semantic relationship group must preserve:

- subject entity identity
- related entity identity
- atomic relationship type
- normalized direction
- relationship state where material
- connectivity
- all contributing source assertion IDs
- all source lanes
- all authority classes
- evidence IDs/counts
- review states
- conflict indicators
- lineage availability

Do NOT group merely because two rows have the same endpoint pair.

Examples that MUST remain separate:

Lambda → NVIDIA : supplier

Lambda ↔ NVIDIA : strategic_partner

Project Indigo → CoreWeave : parent_company

Project Indigo → CoreWeave : guarantor

BO Westover → Blue Owl : backleverage_financing

BO Westover → Blue Owl : guarantor

Same endpoints do not imply same semantic relationship.

==================================================
3. STABLE DISPLAY GROUP KEY
==================================================

Create a deterministic semantic display/group identifier.

It must be derived from governed identity and relationship semantics, not
frontend labels.

It should safely account for:

- canonical subject identity
- canonical related identity
- relationship type
- normalized direction semantics
- material lifecycle/state distinctions where required

Do not use mutable display names as the primary identity.

Do not collapse unresolved entities into resolved ones.

Document the algorithm.

==================================================
4. ASSERTION VERSUS GROUP COUNTS
==================================================

Extend the common read contract so the API can return separately:

- assertion_count
- semantic_relationship_count
- endpoint_pair_count
- connected_entity_count
- review_required_count
- conflict_count

Never make one count masquerade as another.

The existing 808 trusted-read assertions must remain explainable.

Do not silently change the historical source-row count merely to improve
display metrics.

==================================================
5. GROUPED READ MODEL
==================================================

Add a minimal grouped relationship read suitable for Prompt 4.

It may be:

- a grouped mode on the existing common relationship endpoint

OR

- a clearly related read endpoint

Choose the smallest architecture-consistent solution.

Each grouped relationship should expose at minimum:

group_id
subject
related_entity
relationship_type
relationship_family
direction
state
connectivity

assertion_count
source_lanes
authority_classes

evidence_count
source_count
independent_source_count where legitimately measurable

has_review_required
has_conflict
has_external_support
has_ai_support

primary_assertion_id or equivalent
supporting_assertion_ids

lineage_status

Do not infer unsupported fields.

==================================================
6. AUTHORITY PRESERVATION
==================================================

Grouping MUST NOT flatten source authority.

A grouped relationship may contain:

CAM_V3 assertion
+
NORMALIZED assertion
+
EXTERNAL corroboration
+
AI published assertion

but the API must still make clear which source supplied which assertion.

A supplemental/external/AI source cannot become CAM authority simply
because it belongs to the same semantic group.

Preserve source lane and authority on every supporting assertion.

==================================================
7. REVIEW AND CONFLICT SEMANTICS
==================================================

A semantic group may contain assertions with different quality/review
states.

Do NOT solve this by declaring the whole group canonical.

Expose a deterministic group summary such as:

trusted CAM assertion exists
trusted governed normalized assertion exists
review-required assertion exists
external proposal exists
external conflict exists
AI-published assertion exists

The raw assertion statuses must remain available.

The future UI must be able to distinguish:

CONFIRMED RELATIONSHIP

SUPPORTED BY ADDITIONAL SOURCES

REVIEW REQUIRED

CONFLICTING EVIDENCE

PROPOSED EXTERNALLY

AI-GOVERNED

without altering underlying source truth.

==================================================
8. 376 ENDPOINT-PAIR ANALYSIS
==================================================

The Prompt 3B report references 376 endpoint-pair reconciliation.

Verify exactly what 376 represents.

Report:

- endpoint-pair count
- semantic relationship-group count
- assertion count
- number of endpoint pairs with one semantic type
- number with multiple semantic types
- number supported by more than one source lane
- number containing review-required assertions
- number containing conflicts

Do not use 376 as an executive “relationship” count unless the semantics
actually justify it.

==================================================
9. EXPLAINABILITY CONTRACT
==================================================

For a grouped relationship, future UI must support:

WHY AM I SEEING THIS?

Return or link deterministically to:

- source assertions
- authority of each assertion
- source documents
- evidence records
- source location/page where available
- exact excerpt where available
- identity-resolution information
- taxonomy mapping
- review status
- conflicts
- lineage

If historical lineage is incomplete, expose:

LINEAGE_INCOMPLETE

Do not manufacture missing historical stages.

==================================================
10. NETWORK CONTRACT
==================================================

Prepare, but do NOT build, the graph contract.

Define:

NODE_ID
ASSERTION_EDGE_ID
DISPLAY_EDGE_ID

The future graph should normally render DISPLAY_EDGE_ID.

Selecting an edge must allow drill-down to all ASSERTION_EDGE_ID records.

Specify how graph styling can safely reflect:

- CAM authority
- additional source support
- external corroboration
- review requirement
- conflict
- AI-published status

without converting presentation state into source truth.

==================================================
11. BENCHMARK REGRESSION
==================================================

Re-run the benchmark cases after remediation:

- Lambda / NVIDIA
- Project Indigo / CoreWeave
- Applied Digital / CoreWeave
- Serverfarm / Meta
- BO Westover / Blue Owl
- OpenAI cases
- Hut 8
- Cavalry / CyrusOne

Prove specifically that grouping does NOT collapse distinct semantics.

Examples:

supplier != strategic_partner

parent_company != guarantor

guarantor != backleverage_financing

contracted_customer != service_provider

==================================================
12. API ACCEPTANCE TESTS
==================================================

Add tests covering:

1. assertion read remains stable
2. grouped read deterministic
3. same pair / different type stays separate
4. same semantic relationship / multiple lanes groups correctly
5. authority remains assertion-level
6. review status is not silently promoted
7. rejected rows do not enter trusted default
8. V2 remains conditional
9. external proposals do not become CAM
10. AI-published rows do not become CAM
11. lineage incomplete is explicit
12. pagination/filtering produce consistent counts
13. group IDs are stable across repeated reads

==================================================
13. REPORT
==================================================

Create:

LENDING_PROMPT3C_REMEDIATION_REPORT.md

Include:

- original PASS WITH CONDITIONS items
- what was fixed
- what was intentionally deferred
- assertion count
- endpoint-pair count
- semantic group count
- multi-source group count
- multi-type pair count
- authority verification
- review/conflict behavior
- network contract
- explainability contract
- benchmark results
- test results
- remaining blockers

Conclude with exactly one of:

READY FOR PROMPT 4

or

NOT READY FOR PROMPT 4

Do not begin Prompt 4.

STOP when complete.
