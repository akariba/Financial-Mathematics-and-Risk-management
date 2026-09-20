LENDING CANONICAL DATA REMEDIATION — FULL CONTROLLED PASS

You are now performing the remediation stage for the Lending Relationship Intelligence data layer.

This is NOT a UI task.

Do not work on the frontend.
Do not redesign any page.
Do not touch CCR.
Do not call R2D2.
Do not call Web.
Do not call SEC.
Do not use external research.
Do not modify source documents.
Do not modify source workbooks.
Do not fabricate entities, relationships, paths, dates, states, directions, confidence, materiality, or evidence.

Proceed autonomously through the entire approved scope below.
Do not stop for confirmation.
Do not ask me to approve intermediate decisions.
Make reasonable implementation decisions from the repository and available local data.
Stop only for a genuine external blocker that cannot be resolved from the repository/environment.

Once the requested remediation and final validation pass are complete, STOP.
Do not continue with speculative improvements or additional redesign.

==================================================
1. OBJECTIVE
==================================================

Repair the Lending canonical relationship layer so that the application can later be rebuilt on top of a defensible and auditable dataset.

The existing evidence extraction layer has substantially passed:
- physical Lending narrative files are being parsed;
- source locations/excerpts exist;
- canonical relationships generally have textual evidence.

The main problems are downstream:
- document subject resolution;
- entity resolution;
- canonical endpoint identity;
- relationship reconciliation;
- direction;
- state;
- connectivity;
- indirect path representation;
- quality metadata;
- duplicate semantic relationships;
- contradictory evidence handling;
- canonical promotion rules.

The target state is:

RAW SOURCE
    ↓
PARSED EVIDENCE
    ↓
DOCUMENT SUBJECT RESOLUTION
    ↓
ENTITY RESOLUTION
    ↓
ATOMIC RELATIONSHIP OBSERVATIONS
    ↓
EVIDENCE RECONCILIATION
    ↓
QUALITY / GOVERNANCE GATES
    ↓
CANONICAL RELATIONSHIP
    ↓
REVIEW_REQUIRED when unresolved

Do not allow uncertain data to silently become trusted canonical Lending truth.

==================================================
2. HARD SCOPE BOUNDARIES
==================================================

LENDING ONLY.

IN SCOPE:
- Lending narrative PDF/DOCX evidence.
- Lending structured reference workbooks where they provide:
  - population;
  - CAGID;
  - legal/client names;
  - CAM availability/control metadata;
  - exposure/reference metadata.
- Lending SQLite database.
- Lending relationship JSON artifacts.
- frozen Lending baseline only as a historical comparison/reference.
- Lending ingestion/entity-resolution/canonicalization/quality code.
- local Lending APIs needed to validate the corrected data contract.
- tests specific to Lending canonical data.

OUT OF SCOPE:
- CCR.
- CCR CSV.
- CCR frontend.
- RPR.
- R2D2.
- Web.
- SEC.
- external news.
- Stylus preset changes.
- frontend/UI reconstruction.
- materiality scoring changes.
- production architecture refactoring.
- unrelated code cleanup.

Do not mix Lending and CCR under any circumstance.

==================================================
3. IMMUTABILITY AND SAFETY RULE
==================================================

The current frozen Lending baseline is an audit reference.

DO NOT overwrite it in place before the corrected candidate passes validation.

Preserve:
- original source documents;
- original source workbooks;
- original raw extracted evidence;
- current frozen baseline;
- original source inventory.

You MAY modify Lending code required to correct:
- subject resolution;
- entity resolution;
- canonicalization;
- relationship reconciliation;
- state/direction/connectivity logic;
- quality metadata persistence;
- semantic duplicate handling;
- review routing.

You MAY generate:
- a corrected candidate canonical dataset;
- a corrected candidate SQLite database or corrected canonical tables;
- validation artifacts;
- before/after reports;
- migration/reconciliation artifacts.

Do not mutate source evidence in order to make a relationship pass.

Evidence is evidence.
Canonicalization must adapt to the evidence, not the reverse.

==================================================
4. ESTABLISH AUTHORITATIVE SOURCE HIERARCHY
==================================================

Before changing code, enforce the following authority model.

A. POPULATION AUTHORITY
Use the appropriate structured Lending workbook/reference source for:
- target population;
- CAGID;
- canonical Lending client identity;
- CAM control population;
- CAM availability metadata.

Known cohorts currently include approximately:
- 418 Lending benchmark clients;
- 72 CoreAI CAM-control/tracker rows;
- 346 CAM Data rows;
- 343 Technology population rows.

Recalculate these from source.
Do not hardcode the numbers.

B. RELATIONSHIP-EVIDENCE AUTHORITY
Only supplied narrative Lending PDF/DOCX documents may independently establish a Lending relationship.

Structured exposure/facility/workbook rows are NOT relationship evidence merely because:
- two names occur in the same row;
- there is a CAGID;
- there is an obligor;
- there is a facility;
- there is exposure;
- two entities share industry/geography.

C. SUPPLEMENTARY REFERENCE DATA
Other structured files may assist with:
- identity resolution;
- aliases;
- CAGID resolution;
- industry;
- geography;
- facility/exposure context.

They must not manufacture a relationship.

==================================================
5. BASELINE AUDIT FINDINGS TO REMEDIATE
==================================================

Treat these as known prior findings that MUST be independently recomputed before and after remediation.

Previous audit identified approximately:

- 767 canonical relationships.
- 442/767 canonical relationships with at least one name-only/CAGID-less endpoint.
- 18/767 with both endpoints name-only.
- only ~325/767 with both endpoints CAGID-backed.
- 181 indirect relationships with no persisted intermediate entity/path.
- 767/767 missing usable quality-factor metadata.
- 767/767 missing validation-reason arrays.
- 28 normalized semantic duplicate groups covering 56 relationship rows.
- 64 normalized entity-name collision groups.
- ~82 suspicious entity classifications / phrase-like entities.
- ~155 canonical relationships failing the established contradiction predicate.
- broader diagnostics showing about:
  - 203 state-observation conflicts;
  - 173 connectivity-observation conflicts.
- several document subject/CAGID mismatches.
- frozen inventory subject defects.
- examples of invalid entity-like text such as:
  - "as of Company"
  - "subject to Corp"
  - "wholly owned holding"
  - "which is Company"
  - "with each bank"
  - other narrative fragments.

Do NOT blindly trust these counts.

Recalculate them independently from the current data before remediation.

==================================================
6. PHASE 1 — DOCUMENT SUBJECT RECONCILIATION
==================================================

For EVERY supplied Lending narrative document:

Determine the intended document subject using the strongest available evidence, in this order:

1. explicit CAGID from authoritative control/reference source;
2. authoritative client/control workbook mapping;
3. document title/header/legal-name content;
4. filename;
5. other bounded local aliases.

Never infer a subject from a random sentence fragment.

Create an explicit document-subject reconciliation record containing at minimum:

- source_file
- source_hash
- file_type
- intended_subject_name
- intended_subject_cagid
- sqlite_subject_name_before
- sqlite_subject_cagid_before
- resolution_status
- resolution_method
- confidence
- discrepancy_reason
- action_taken
- subject_name_after
- subject_cagid_after

Resolution statuses should include:
- RESOLVED
- UNRESOLVED
- CONFLICT
- NOT_APPLICABLE

If the subject cannot be defended:
DO NOT guess.
Mark the document subject unresolved and prevent relationships dependent on that subject from becoming canonical unless independently resolvable.

Specifically inspect all previously identified subject mismatches and frozen subject defects.

==================================================
7. PHASE 2 — ENTITY RESOLUTION
==================================================

Build a defensible local entity-resolution layer.

Each entity should preferably have:

- canonical_entity_id
- canonical_name
- normalized_name
- CAGID where available
- aliases
- entity_type/category when evidenced
- source provenance
- resolution_method
- resolution_confidence

Resolution priority:

1. exact CAGID match;
2. exact known canonical-name match;
3. validated alias match;
4. deterministic normalized-name match if unambiguous;
5. bounded local evidence-supported resolution;
6. otherwise unresolved.

Do NOT use broad fuzzy matching to silently merge legal entities.

Never promote a text fragment into an entity solely because it:
- contains "Company";
- contains "Corp";
- contains "Group";
- contains "Holdings";
- is capitalized;
- appears near relationship wording.

Create explicit rejection/guard logic for narrative fragments such as:

- as the company
- as of company
- which is company
- subject to corp
- with each bank
- by the group
- during the company
- supported by company
- wholly owned holding
- wholly owned subsidiary of ...
- borrower and holding
- given the limited
- who directs all activities of the company
- other descriptive clauses

A phrase may only become an entity when it resolves to a genuine legal/entity record through authoritative local evidence.

Do not fabricate a CAGID.

CAGID may be NULL when no authoritative CAGID exists, but such records must carry explicit identity-resolution status.

==================================================
8. ENTITY RESOLUTION QUALITY GATES
==================================================

Before an endpoint can participate in a CANONICAL relationship:

Require:
- a genuine entity;
- defensible canonical name;
- provenance;
- no narrative-fragment classification.

Preferred canonical condition:
- CAGID-backed.

If no CAGID exists but the entity is still clearly a genuine external legal/entity name:
allow only if:
- identity is unambiguous;
- source evidence explicitly names it;
- a resolution method is persisted;
- the absence of CAGID is explicit;
- it does not collide with another entity.

Otherwise route relationship to REVIEW_REQUIRED.

Do not force every external entity to have a Citi CAGID if the source population legitimately does not provide one.

The requirement is defensible identity, not artificial completeness.

==================================================
9. PHASE 3 — RELATIONSHIP ATOMICITY
==================================================

Represent one canonical row per:

SUBJECT
+
RELATED ENTITY
+
RELATIONSHIP TYPE
+
DIRECTION
+
valid relationship state where required by the schema

Do not collapse distinct legitimate relationship types into one generic row.

Examples:
An entity pair may legitimately have:
- equity investor
- strategic partner
- contracted customer

as separate atomic relationships if each is supported.

Do not create multiple records for identical semantics merely because several documents support them.

Evidence should attach many-to-one to a canonical relationship.

==================================================
10. APPROVED RELATIONSHIP TAXONOMY
==================================================

Use the existing approved Lending relationship taxonomy.

Do not invent new taxonomy values.

Before retaining a relationship type:
confirm that its supporting evidence actually expresses that semantic relationship.

Do not infer a relationship type merely from:
- co-mention;
- common ownership elsewhere;
- industry similarity;
- geographic proximity;
- exposure amount;
- document proximity;
- same facility;
- generic wording.

If evidence does not support the taxonomy:
- downgrade to REVIEW_REQUIRED,
or
- REJECT if clearly unsupported.

Do not force-fit evidence into the nearest category.

==================================================
11. PHASE 4 — DIRECTION
==================================================

Direction must be evidence-derived.

Allowed canonical direction values should follow the existing schema, e.g.:

- SUBJECT_TO_RELATED / A_TO_B
- RELATED_TO_SUBJECT / B_TO_A
- BIDIRECTIONAL

depending on the repository's canonical naming.

Do not globally default all relationships to SUBJECT_TO_RELATED.

Infer direction from explicit semantics.

Examples:

"Parent X owns Subject Y"
means:
X → Y for parent/subsidiary semantics,
not automatically Subject → X.

"Subject guarantees Entity B"
means:
Subject → B for guarantor semantics.

"Entity B guarantees Subject"
means:
B → Subject.

For symmetric/bidirectional relationships:
use BIDIRECTIONAL only when the taxonomy/evidence genuinely supports it.

If direction cannot be established:
do not guess.
Route to REVIEW_REQUIRED.

Persist:
- direction
- direction_basis
- supporting evidence IDs

==================================================
12. PHASE 5 — STATE RECONCILIATION
==================================================

Allowed states:

- CURRENT
- EMERGING
- HISTORICAL
- TERMINATED

Do not assign state from one arbitrarily selected evidence row.

For each canonical candidate:
collect ALL associated evidence observations.

Reconcile them.

Rules:

CURRENT:
requires evidence that the relationship is currently active as of the source context.

EMERGING:
requires explicit forward-looking, newly forming, proposed, pending, or developing evidence consistent with the current taxonomy.

HISTORICAL:
requires evidence that the relationship existed previously but is no longer current or is explicitly described historically.

TERMINATED:
requires explicit termination, cancellation, transfer, exit, maturity, disposal, completed transition, etc.

If evidence conflicts materially:
do not silently choose one.

Persist:
- observed_states[]
- reconciled_state
- reconciliation_reason
- conflicting_evidence_ids[]
- state_conflict = true/false

If unresolved conflict remains:
route to REVIEW_REQUIRED.

==================================================
13. PHASE 6 — CONNECTIVITY
==================================================

Allowed connectivity:

- DIRECT
- INDIRECT

DIRECT:
the source explicitly links Subject and Related Entity in the stated relationship.

INDIRECT:
there must be an actual supported path.

Every canonical INDIRECT relationship must persist at least:

- path_length
- intermediate_entity_ids[]
- intermediate_entity_names[]
- relationship_path[]
- path_evidence_ids[]

Example:
A → B → C

Do NOT mark A → C indirect simply because:
- A and C share an owner;
- A and C are in the same industry;
- A and C are geographically related;
- A and C occur in the same source;
- the extractor selected INDIRECT.

If an indirect relationship has no defensible intermediate path:
it may not remain canonical INDIRECT.

Either:
- reconstruct the path from genuine evidence;
- reclassify as DIRECT if evidence supports that;
- route to REVIEW_REQUIRED;
- reject if unsupported.

No canonical INDIRECT row may remain with an empty path.

==================================================
14. PHASE 7 — EVIDENCE RECONCILIATION
==================================================

For every candidate relationship aggregate ALL evidence.

Do not validate a row just because one evidence item is strong.

Evaluate:
- supporting evidence;
- contradicting evidence;
- state observations;
- direction observations;
- connectivity observations;
- source-document identity;
- extraction quality;
- duplicate evidence;
- source versions.

Persist an evidence reconciliation summary.

Required fields should include or equivalent:

- evidence_count
- supporting_evidence_ids
- conflicting_evidence_ids
- source_document_count
- evidence_channels
- observed_states
- observed_directions
- observed_connectivity
- reconciliation_status
- reconciliation_reason

Suggested reconciliation statuses:

- CONSISTENT
- CONSISTENT_WITH_MINOR_VARIATION
- CONFLICT_REQUIRES_REVIEW
- INSUFFICIENT_EVIDENCE

==================================================
15. PHASE 8 — QUALITY FACTORS
==================================================

Do not leave canonical quality metadata empty.

For every canonical/review relationship persist explicit quality factors derived from actual checks.

At minimum include:

ENTITY IDENTITY
- subject_identity_resolved
- related_identity_resolved
- subject_cagid_available
- related_cagid_available
- entity_collision_detected

EVIDENCE
- evidence_exists
- exact_excerpt_verified
- source_exists
- source_hash_verified
- source_location_verified
- relationship_explicit
- co_mention_only

CONSISTENCY
- direction_supported
- state_supported
- connectivity_supported
- evidence_conflict
- semantic_duplicate

INDIRECT
- indirect_path_complete

PROVENANCE
- document_subject_resolved
- source_subject_consistent

Do not invent numeric confidence scores unless an existing documented method already exists.

Prefer transparent categorical/boolean factors.

==================================================
16. PHASE 9 — VALIDATION REASONS
==================================================

Every canonical or review row must have a non-empty persisted decision trail.

For canonical relationships, store validation reasons such as:

- BOTH_ENTITIES_RESOLVED
- EXPLICIT_RELATIONSHIP_EVIDENCE
- DIRECTION_SUPPORTED
- STATE_SUPPORTED
- CONNECTIVITY_SUPPORTED
- INDIRECT_PATH_VERIFIED
- NO_MATERIAL_CONFLICT
- SOURCE_PROVENANCE_VERIFIED

For REVIEW_REQUIRED, use explicit reasons such as:

- SUBJECT_IDENTITY_UNRESOLVED
- RELATED_ENTITY_UNRESOLVED
- NAME_COLLISION
- DIRECTION_AMBIGUOUS
- STATE_CONFLICT
- CONNECTIVITY_CONFLICT
- INDIRECT_PATH_MISSING
- DOCUMENT_SUBJECT_CONFLICT
- SEMANTIC_DUPLICATE_CONFLICT
- INSUFFICIENT_EXPLICIT_EVIDENCE

Do not use generic "review needed" when a precise reason is known.

==================================================
17. PHASE 10 — SEMANTIC DUPLICATES
==================================================

Detect both:

A. exact duplicates
B. semantic duplicates

Exact canonical identity should consider:
- canonical subject
- canonical related entity
- relationship type
- direction
- relevant state semantics

Multiple evidence rows do not justify duplicate canonical rows.

Consolidate evidence under one canonical record where the semantic relationship is identical.

Do NOT combine genuinely different relationship types.

Identify and resolve:
- normalized-name collision groups;
- duplicate entity records;
- duplicate pair/type relationships;
- records differing only because aliases were treated as different entities.

Preserve full provenance after consolidation.

==================================================
18. PHASE 11 — REVIEW_REQUIRED GOVERNANCE
==================================================

Create a strict promotion boundary.

CANONICAL/VALIDATED only if:
- document subject is defensible;
- both endpoints are genuine entities;
- relationship type is supported;
- direction is supported;
- state is supported or legitimately not applicable;
- connectivity is supported;
- indirect path exists when indirect;
- evidence provenance passes;
- no unresolved material contradiction remains.

Otherwise:
REVIEW_REQUIRED.

Do not delete questionable evidence.

Keep:
RAW EVIDENCE
and
REVIEW_REQUIRED

separate from:
TRUSTED CANONICAL.

Do not treat REVIEW_REQUIRED as management truth.

==================================================
19. PHASE 12 — SOURCE DOCUMENT WITH ZERO YIELD
==================================================

The previous audit identified one narrative document with zero relationship evidence.

Investigate it explicitly.

Determine whether:
- it genuinely contains no qualifying relationship;
- parser/extraction failed semantically;
- subject mapping prevented valid extraction;
- relevant relationship sections were missed.

Do not manufacture relationships merely to give every document output.

Report the result.

==================================================
20. PHASE 13 — POPULATION COVERAGE
==================================================

Recompute population coverage correctly.

Keep the following concepts separate:

1. FULL LENDING BENCHMARK POPULATION
2. COREAI CONTROL/TRACKER POPULATION
3. CAM DATA PRESENCE
4. PHYSICAL NARRATIVE DOCUMENT COVERAGE
5. CLIENTS WITH ≥1 CANONICAL RELATIONSHIP
6. CLIENTS WITH REVIEW_REQUIRED RELATIONSHIPS ONLY
7. CLIENTS WITH NO RELATIONSHIP EVIDENCE
8. TECHNOLOGY POPULATION

Do not call structured CAM metadata "physical CAM document coverage."

Do not call Technology clients "missing CAM documents" merely because physical documents were not supplied, unless the control framework explicitly says they were expected.

==================================================
21. PHASE 14 — DO NOT IMPLEMENT MATERIALITY YET
==================================================

Do not build or change materiality scoring in this pass.

However, produce readiness statistics for later UI integration:

For each of the 418 target Lending clients, where available, report whether local structured sources contain:

- OSUC / PSLE amount;
- exposure amount;
- facility amount;
- rating;
- sector/industry;
- geography;
- CAM availability;
- canonical relationship count;
- direct relationship count;
- indirect relationship count;
- review-required count.

This is readiness reporting only.

Do not assign materiality labels or ranking in this remediation stage.

==================================================
22. PHASE 15 — BUILD CORRECTED CANDIDATE
==================================================

After implementing the corrections:

Create a corrected candidate Lending canonical layer.

Do NOT overwrite the frozen historical baseline.

Prefer a clearly named candidate artifact, for example:

LENDING_CANONICAL_V2_CANDIDATE

or equivalent existing repository convention.

The candidate must be reproducible from:
- unchanged source documents;
- unchanged structured reference data;
- corrected deterministic code.

==================================================
23. PHASE 16 — FULL VALIDATION
==================================================

Run one complete full-data validation pass.

NOT A SAMPLE.

Validate EVERY candidate canonical relationship.

For each canonical row verify:

1. Subject genuine and correctly resolved.
2. Related entity genuine and correctly resolved.
3. Approved relationship taxonomy.
4. Explicit relationship support.
5. Correct direction.
6. Correct state.
7. Correct connectivity.
8. Indirect path present when indirect.
9. Source exists.
10. Source hash matches.
11. Source location exists.
12. Exact excerpt exists.
13. Evidence supports both endpoints.
14. No unresolved material conflict.
15. No exact semantic duplicate.
16. Non-empty quality factors.
17. Non-empty validation reasons.
18. Provenance complete.
19. No CCR source.
20. Correct canonical/review separation.

Do not merely rerun the old quality predicate.
The new validation must test the actual corrected rules above.

==================================================
24. CCR ISOLATION CHECK
==================================================

Explicitly verify:

- zero CCR relationship evidence in Lending;
- zero CCR relationships in Lending;
- zero CCR source documents used to create Lending canonical relationships;
- no CCR CSV used for Lending entity resolution;
- no CCR-only population row promoted into Lending population because of CCR membership.

If an existing SQLite operational inventory still contains CCR provenance unrelated to Lending relationships:
report it separately.

Do not silently treat that as Lending evidence.

==================================================
25. BASELINE COMPARISON
==================================================

Compare candidate V2 against frozen V1.

Report:

- relationships retained;
- relationships removed from canonical;
- relationships moved to REVIEW_REQUIRED;
- relationships newly canonical because identity/reconciliation was corrected;
- endpoint identity changes;
- subject changes;
- relationship type changes;
- direction changes;
- state changes;
- connectivity changes;
- duplicate consolidations.

Do not mutate V1.

==================================================
26. STATISTICS REPORT — REQUIRED
==================================================

At completion generate a detailed machine-readable and human-readable statistics report.

Create something like:

LENDING_CANONICAL_V2_REMEDIATION_REPORT.json

and, if appropriate in the repository:

LENDING_CANONICAL_V2_REMEDIATION_REPORT.md

The report MUST include all sections below.

-----------------------------------------
A. SOURCE CORPUS
-----------------------------------------

- physical narrative files discovered
- PDFs
- DOCX
- unique narrative contents
- duplicate source groups
- structured reference files used
- files parsed successfully
- files failed
- documents producing ≥1 relationship candidate
- documents producing ≥1 canonical relationship
- documents producing review-only relationships
- documents producing zero relationship evidence

-----------------------------------------
B. POPULATION
-----------------------------------------

- Lending benchmark clients
- CoreAI control/tracker clients
- Technology clients
- CAM Data unique clients
- physical CAM/document-covered clients
- clients with canonical relationships
- clients with review-required only
- clients with no narrative relationship evidence
- population disconnected from every canonical relationship

-----------------------------------------
C. ENTITY QUALITY
-----------------------------------------

BEFORE and AFTER:

- total entity records
- CAGID-backed entities
- name-only entities
- ambiguous entities
- unresolved entities
- narrative-fragment entities
- normalized-name collision groups
- alias groups
- duplicate entity records
- canonical relationships with:
  - both endpoints CAGID-backed
  - one CAGID-backed endpoint
  - zero CAGID-backed endpoints
- canonical relationships with unresolved endpoint
- suspicious entity classifications

-----------------------------------------
D. RELATIONSHIPS
-----------------------------------------

BEFORE and AFTER:

- total candidates
- canonical validated
- review required
- rejected
- canonical by relationship type
- canonical by relationship family
- canonical direct
- canonical indirect
- canonical current
- canonical emerging
- canonical historical
- canonical terminated

-----------------------------------------
E. INDIRECT RELATIONSHIPS
-----------------------------------------

BEFORE and AFTER:

- total indirect
- indirect with path
- indirect missing path
- average path length
- max path length
- intermediate entities count

Target:
canonical indirect missing path = 0

-----------------------------------------
F. DIRECTION
-----------------------------------------

BEFORE and AFTER:

- A_TO_B / SUBJECT_TO_RELATED
- B_TO_A / RELATED_TO_SUBJECT
- BIDIRECTIONAL
- unresolved/ambiguous direction
- rows routed to review due to direction

Highlight if every record still has the same direction because that likely indicates fallback logic.

-----------------------------------------
G. STATE QUALITY
-----------------------------------------

BEFORE and AFTER:

- state conflicts
- unsupported persisted states
- state-reconciled records
- routed-to-review state conflicts
- current
- emerging
- historical
- terminated

-----------------------------------------
H. CONNECTIVITY QUALITY
-----------------------------------------

BEFORE and AFTER:

- direct
- indirect
- connectivity conflicts
- unsupported connectivity
- connectivity-reconciled rows
- routed-to-review due to connectivity

-----------------------------------------
I. EVIDENCE
-----------------------------------------

- evidence rows
- source/hash/location/excerpt PASS
- source/hash/location/excerpt FAIL
- canonical-linked evidence rows
- average evidence rows per canonical relationship
- canonical relationships with 1 source
- canonical relationships with >1 source
- conflicting evidence cases
- document-subject inconsistencies

-----------------------------------------
J. DUPLICATES
-----------------------------------------

BEFORE and AFTER:

- exact relationship duplicates
- semantic duplicate groups
- rows consolidated
- duplicate evidence payloads
- entity collision groups

-----------------------------------------
K. QUALITY METADATA
-----------------------------------------

BEFORE and AFTER:

- canonical rows with quality factors populated
- canonical rows with empty quality factors
- canonical rows with validation reasons populated
- canonical rows with empty validation reasons
- review rows with explicit review reason
- review rows with generic/empty reason

Target:
canonical empty quality metadata = 0
canonical empty validation reason = 0

-----------------------------------------
L. SUBJECT RECONCILIATION
-----------------------------------------

- documents with correct subject
- documents corrected
- documents unresolved
- documents conflicted
- list every subject correction:
  source_file
  before_name
  before_cagid
  after_name
  after_cagid
  resolution_basis

-----------------------------------------
M. V1 → V2 MOVEMENT
-----------------------------------------

- V1 canonical total
- V2 canonical total
- retained
- moved canonical → review
- moved canonical → rejected
- newly canonical
- duplicates consolidated
- subject corrected
- endpoint corrected
- type corrected
- direction corrected
- state corrected
- connectivity corrected

-----------------------------------------
N. MATERIALITY/UI READINESS
-----------------------------------------

Do NOT score materiality.

Report data availability only for the Lending benchmark population:

- clients with OSUC/PSLE
- clients without OSUC/PSLE
- clients with rating
- clients with industry
- clients with geography
- clients with exposure/facility data
- clients with CAM metadata
- clients with canonical relationships
- clients with both exposure + canonical relationship data
- clients with insufficient data for future materiality prioritization

-----------------------------------------
O. CCR ISOLATION
-----------------------------------------

- CCR relationship rows in Lending
- CCR evidence rows in Lending
- CCR source documents contributing relationship evidence
- CCR-only entities incorrectly promoted
- residual operational provenance references

Expected relationship/evidence contamination = 0

-----------------------------------------
P. FINAL PASS/FAIL
-----------------------------------------

Report individually:

SOURCE PARSING: PASS / FAIL
DOCUMENT SUBJECT RESOLUTION: PASS / FAIL
ENTITY RESOLUTION: PASS / FAIL
EVIDENCE INTEGRITY: PASS / FAIL
RELATIONSHIP TAXONOMY: PASS / FAIL
DIRECTION: PASS / FAIL
STATE: PASS / FAIL
CONNECTIVITY: PASS / FAIL
INDIRECT PATH COMPLETENESS: PASS / FAIL
DUPLICATE CONTROL: PASS / FAIL
QUALITY METADATA: PASS / FAIL
REVIEW GOVERNANCE: PASS / FAIL
CCR ISOLATION: PASS / FAIL
POPULATION RECONCILIATION: PASS / FAIL
V2 CANONICAL DATASET: PASS / FAIL

Then:

OVERALL LENDING CANONICAL DATA QUALITY:
PASS / FAIL

==================================================
27. FINAL EXCEPTION REGISTER
==================================================

Produce an exception table containing all remaining non-PASS issues.

Required columns:

exception_id
severity
source_file
document_subject
document_subject_cagid
relationship_id
subject_entity
subject_cagid
related_entity
related_cagid
relationship_type
direction
state
connectivity
failure_category
failure_reason
evidence_ids
source_location
resolution_status
recommended_action

Recommended action is advisory only.
Do NOT automatically perform actions beyond the approved remediation scope.

Severity:
- CRITICAL
- HIGH
- MEDIUM
- LOW

==================================================
28. ACCEPTANCE CONDITIONS
==================================================

The candidate is acceptable for UI integration only if ALL are true:

1. No narrative fragments remain as canonical entities.
2. No canonical relationship has unresolved endpoint identity.
3. Every canonical relationship has explicit textual relationship support.
4. Every canonical direction is evidence-supported.
5. Every canonical state is evidence-supported/reconciled.
6. Every canonical connectivity value is supported.
7. Every canonical INDIRECT relationship has a persisted path.
8. No unresolved material evidence contradiction remains canonical.
9. Exact/semantic duplicate canonical rows are resolved.
10. Every canonical row has populated quality factors.
11. Every canonical row has populated validation reasons.
12. Review-required rows remain outside trusted canonical truth.
13. No CCR evidence or relationships enter Lending.
14. Source evidence remains unchanged.
15. Frozen V1 remains unchanged.
16. Full statistics report is produced.
17. Full exception register is produced.

If some conditions cannot be satisfied from the available evidence:
DO NOT manufacture data to force a PASS.

Route affected records to REVIEW_REQUIRED and report the limitation.

A lower canonical count is acceptable.

Accuracy and defensibility are more important than preserving the current count of 767.

==================================================
29. FINAL RESPONSE FORMAT
==================================================

When finished, return ONLY:

LENDING CANONICAL REMEDIATION: PASS / FAIL

V1 canonical relationships: X
V2 canonical relationships: X
Retained canonical: X
Moved to review: X
Rejected: X
Newly canonical: X

Entities corrected: X
Narrative-fragment entities remaining: X
Canonical rows with unresolved endpoints: X
Canonical rows with both endpoints CAGID-backed: X
Indirect relationships: X
Indirect relationships with verified path: X
Indirect relationships missing path: X

Direction conflicts remaining: X
State conflicts remaining: X
Connectivity conflicts remaining: X
Semantic duplicate groups remaining: X
Canonical rows missing quality metadata: X
Canonical rows missing validation reasons: X

Documents audited: X/X
Documents with corrected subject: X
Documents unresolved: X
Documents producing zero evidence: X

CCR relationship contamination: X
CCR evidence contamination: X

Population reconciliation: PASS / FAIL
Evidence integrity: PASS / FAIL
Canonical quality gates: PASS / FAIL
Frozen V1 unchanged: PASS / FAIL

Statistics report:
<path>

Exception register:
<path>

V2 candidate:
<path>

UI READY: YES / NO

If UI READY = NO:
list the precise blocking controls only.

Then STOP.
