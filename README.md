LENDING V3 — FRESH PRECISION-FIRST CAM RELATIONSHIP EXTRACTION

You are starting a NEW Lending relationship extraction.

This is V3.

IMPORTANT:
Do NOT repair, reuse, promote, migrate, or filter the previous 32,957 relationship-candidate population.

The previous candidate population is diagnostic history only.

V3 must rebuild the relationship population FROM SCRATCH from the original Lending CAM/credit narrative documents.

Proceed autonomously through the entire approved scope.
Do not ask for confirmation.
Do not stop for intermediate approval.
Stop only for a genuine external/environment blocker.

==================================================
1. PRIMARY OBJECTIVE
==================================================

Create a NEW, substantially cleaner Lending relationship dataset using a PRECISION-FIRST extraction strategy.

The source universe is:

- 48 supplied physical Lending narrative PDF/DOCX files
- approximately 46 unique document contents after exact duplicate handling
- approximately 42 intended physical-CAM subject clients

Recompute all numbers from source rather than hardcoding them.

The goal is NOT maximum relationship recall.

The goal is:

HIGH-PRECISION, EVIDENCE-BACKED RELATIONSHIPS
that an analyst can understand and defend.

It is acceptable to miss weak relationships.

It is NOT acceptable to create thousands of speculative relationships.

==================================================
2. HARD BOUNDARIES
==================================================

LENDING ONLY.

DO NOT:
- touch CCR
- use CCR data
- modify CCR
- call SEC
- call R2D2
- call Web
- use external news
- modify the frontend
- redesign the UI
- touch RPR
- modify Stylus presets
- modify original PDF/DOCX source files
- overwrite V1
- promote V2
- reuse V2 relationship rows as V3 truth
- use the old 32,957 candidates as V3 input

V1 remains frozen historical baseline.

V2 remains diagnostic only.

V5 files remain supplemental only.

==================================================
3. V5 FILE POLICY
==================================================

Previous analysis determined:

v5-All-CAGIDs.xlsx:
- supplemental exact-CAGID cross-check only
- not authoritative legal-name master
- not document-subject authority
- not relationship evidence
- no fuzzy matching

v5-All-CAGIDs.json:
- manual-review/discovery aid only
- malformed/non-standard structure
- unknown provenance
- not relationship evidence
- not document-subject authority

Do NOT use either V5 file to manufacture relationships.

Do NOT use RESULT_TEXT from V5 as relationship evidence.

Do NOT use V5 generic narrative keyword matches for subject resolution.

==================================================
4. AUTHORITATIVE SOURCE HIERARCHY
==================================================

A. RELATIONSHIP EVIDENCE

Only the supplied original Lending narrative PDF/DOCX CAM/credit documents may establish CAM relationship evidence in V3.

B. POPULATION / IDENTITY / REFERENCE

Structured Lending workbooks may provide:
- CAGID
- benchmark population
- client identity
- CAM metadata
- exposure
- rating
- sector
- geography
- facility/reference data

But structured files must NOT create relationship facts.

C. V5

Supplemental cross-check only as defined above.

==================================================
5. START FROM ORIGINAL DOCUMENTS
==================================================

Inventory the original physical narrative files again.

Calculate:

- physical files
- PDF count
- DOCX count
- SHA256
- exact duplicate groups
- unique document contents
- intended document subjects
- intended subject CAGIDs
- parse status

Deduplicate exact duplicate document contents BEFORE relationship extraction.

Do not extract the same underlying document twice merely because duplicate file copies exist.

Preserve duplicate provenance.

==================================================
6. DOCUMENT SUBJECT RESOLUTION FIRST
==================================================

Before relationship extraction, determine the subject of every unique narrative document.

Use this priority:

1. authoritative CAGID/control mapping
2. authoritative Lending client/control workbook
3. explicit legal name/CAGID in document header or first-page table
4. filename
5. bounded validated local alias

Never infer the document subject from generic body text.

Never use a random entity mentioned in the CAM as the CAM subject.

Persist:

- document_id
- source_file
- source_hash
- intended_subject_name
- intended_subject_cagid
- subject_resolution_method
- subject_resolution_status
- supporting_basis

Statuses:

RESOLVED
REVIEW_REQUIRED
UNRESOLVED

If subject identity is uncertain:
do not guess.

==================================================
7. PRECISION-FIRST ENTITY EXTRACTION
==================================================

Extract only genuine business/legal entities.

Potential entity categories include:

- company
- parent
- subsidiary
- sponsor
- investor
- guarantor
- lender
- agent bank
- customer
- supplier
- strategic partner
- joint venture
- regulator
- advisor
- infrastructure provider
- other genuine legal/business entity

Do NOT create entity records from:

- sentence fragments
- descriptive clauses
- generic nouns
- role descriptions without an actual named entity
- pronouns
- incomplete organization fragments

Reject patterns similar to:

"as of Company"
"which is Company"
"subject to Corp"
"by the Group"
"with each bank"
"wholly owned holding"
"Borrower and Holding"
"the Company"
"the Group"

unless they can be deterministically resolved to an actual named entity from the same bounded evidence.

Do not silently fuzzy-match unrelated entities.

==================================================
8. ENTITY RESOLUTION
==================================================

Resolution priority:

1. exact CAGID
2. exact authoritative legal name
3. validated alias
4. deterministic normalized legal-name match
5. bounded local evidence-supported resolution
6. otherwise unresolved

A CAGID is preferred but not mandatory for a genuine external entity.

A non-CAGID external entity may remain valid when:

- legal/entity identity is explicit
- the name is unambiguous
- the source explicitly names it
- provenance is persisted
- no conflicting entity resolution exists

Never fabricate a CAGID.

==================================================
9. CRITICAL NOISE-REDUCTION RULE
==================================================

DO NOT reproduce the previous ~32,957 candidate explosion.

A relationship candidate MUST NOT be generated simply because:

- two entities are in the same document
- two entities are in the same section
- two entities are in the same paragraph
- two entities are near each other
- a relationship keyword appears nearby
- two entities share industry
- two entities share geography
- an entity is repeatedly mentioned
- two entities participate in the same facility
- two entities occur in similar contexts

CO-MENTION IS NOT A RELATIONSHIP.

==================================================
10. REQUIREMENTS BEFORE CANDIDATE CREATION
==================================================

Create a candidate relationship ONLY when ALL are true:

1. Subject endpoint is a genuine entity.
2. Related endpoint is a genuine entity.
3. Evidence explicitly expresses relationship semantics.
4. Relationship maps to an approved Lending relationship type.
5. Evidence text directly supports the selected relationship type.
6. Evidence location is recoverable.
7. Evidence excerpt is persisted.

If those conditions are not satisfied:

DO NOT create a relationship candidate.

This is different from generating a candidate and rejecting it later.

Stop weak observations BEFORE candidate generation.

==================================================
11. BOUNDED EVIDENCE WINDOW
==================================================

Prefer relationship extraction from:

- same sentence
- neighboring sentence when grammatically necessary
- tightly bounded paragraph
- structured table row where semantics are explicit

Do not infer relationships from distant text across pages or sections.

Persist the exact evidence window used.

==================================================
12. PRIORITIZE RELATIONSHIP-RELEVANT CAM SECTIONS
==================================================

Prioritize sections such as:

- corporate structure
- ownership
- shareholders
- sponsor
- parent/subsidiary
- guarantors
- collateral providers
- customers
- suppliers
- revenue concentration
- strategic partners
- joint ventures
- financing
- lenders
- agent banks
- dependencies
- material contracts
- M&A
- acquisitions/disposals
- counterparty/obligor structure
- business dependencies

Do NOT mine all document sections equally.

Risk narrative sections may contain useful relationships, but only create relationships when explicit semantics exist.

==================================================
13. RELATIONSHIP TAXONOMY
==================================================

Use the existing approved Lending taxonomy only.

Expected existing categories include, where already supported:

- parent_company
- subsidiary
- guarantor
- lender
- agent_bank
- sponsor
- equity_investor
- contracted_customer
- supplier
- strategic_partner
- joint_venture
- advisor
- regulator
- legal_counterparty
- collateral_provider
- m_and_a_target
- backleverage_financing
- revenue_concentration
- customer_dependency
- supplier_concentration
- technology_dependency
- infrastructure_dependency
- competitor
- service_provider

Do NOT invent new relationship types without an existing governed taxonomy definition.

If evidence does not cleanly fit:
REVIEW_REQUIRED or do not create candidate.

==================================================
14. ONE SEMANTIC RELATIONSHIP — MANY EVIDENCE ITEMS
==================================================

This is mandatory.

If the same relationship appears several times:

DO NOT create several candidate relationships.

Example:

CoreWeave → NVIDIA → technology_dependency

If supported by 6 passages:

relationship count = 1
evidence count = 6

Relationship identity should be based on:

- canonical subject
- canonical related entity
- relationship type
- direction
- relevant state semantics

Repeated evidence must attach to the same relationship.

==================================================
15. EVIDENCE STRENGTH
==================================================

Use evidence-strength categories:

HIGH
MEDIUM
INSUFFICIENT

Do NOT call this "accuracy".

HIGH means:
- explicit named entities
- explicit relationship wording
- semantics clear
- direction clear
- evidence directly supports relationship type
- no material contradictory observation

MEDIUM means:
- genuine entities
- relationship is clearly supported
- wording requires limited interpretation
- no major contradiction
- still defensible to an analyst

INSUFFICIENT means:
- co-mention
- vague wording
- generic business language
- ambiguous endpoint
- ambiguous relationship type
- substantial inference
- contradictory evidence
- unsupported direction

Only HIGH and MEDIUM relationships may proceed toward canonical/review evaluation.

INSUFFICIENT observations must not become canonical relationships.

==================================================
16. DIRECTION
==================================================

Derive direction from evidence.

Do not default every relationship to SUBJECT_TO_RELATED.

Example:

"Parent X owns Borrower Y"

Parent X → Borrower Y

"Borrower Y is guaranteed by Parent X"

Parent X → Borrower Y for guarantor semantics.

Persist:

- direction
- direction_basis
- supporting evidence

If direction is genuinely ambiguous:
REVIEW_REQUIRED.

==================================================
17. STATE
==================================================

Allowed state:

CURRENT
EMERGING
HISTORICAL
TERMINATED

State must come from evidence.

Do not automatically assign CURRENT.

For multiple observations:
reconcile all evidence.

If conflict cannot be resolved:
REVIEW_REQUIRED.

Persist:

- observed_states
- reconciled_state
- reconciliation_reason
- state_conflict flag

==================================================
18. DIRECT RELATIONSHIPS
==================================================

DIRECT requires explicit source linkage between the two entities.

Do not call a relationship DIRECT simply because both entities appear in the same CAM.

==================================================
19. HIDDEN / INDIRECT RELATIONSHIPS
==================================================

Hidden relationships are allowed and important.

But a hidden relationship may exist ONLY when there is a complete evidence-backed path.

Example:

Client A
→ Supplier B
→ NVIDIA

If:

A → B is supported
AND
B → NVIDIA is supported

then:

A → NVIDIA may be represented as HIDDEN / INDIRECT.

Persist for every hidden relationship:

- path_length
- intermediate_entity_ids
- intermediate_entity_names
- relationship_path
- edge relationship types
- evidence IDs for EVERY hop
- evidence strength for EVERY hop
- overall hidden-path evidence strength

No hidden relationship without an actual path.

NO:
A → C indirect merely because:
- common industry
- common supplier category
- common geography
- co-mention
- generic ecosystem inference

==================================================
20. HIDDEN RELATIONSHIP STRENGTH
==================================================

HIGH hidden-path strength:

Every hop is HIGH evidence strength.

MEDIUM hidden-path strength:

All hops are at least MEDIUM and no hop is insufficient.

If ANY hop is INSUFFICIENT:

Do NOT promote the hidden relationship.

The weakest hop limits the path.

==================================================
21. SEMANTIC DUPLICATION
==================================================

Before storing a relationship:

Check whether an identical semantic relationship already exists.

If yes:
attach evidence to existing relationship.

Do not create duplicate rows.

Maintain:
- source count
- evidence count
- document count
- evidence IDs

==================================================
22. CONTRADICTORY EVIDENCE
==================================================

Collect all evidence for the same semantic relationship.

Identify:

- supporting evidence
- conflicting evidence
- state disagreement
- direction disagreement
- connectivity disagreement
- identity disagreement

A relationship with unresolved material contradiction must not become trusted canonical truth.

Route to:
REVIEW_REQUIRED.

==================================================
23. CANONICAL PROMOTION RULE
==================================================

A relationship may become CANONICAL only when:

- document subject is resolved
- both endpoints are genuine entities
- relationship semantics are explicit
- approved taxonomy used
- direction supported
- state supported/reconciled
- connectivity supported
- evidence strength = HIGH or MEDIUM
- provenance intact
- no unresolved material contradiction
- not a semantic duplicate

For INDIRECT:
complete evidence-backed path is additionally mandatory.

==================================================
24. REVIEW_REQUIRED
==================================================

Use REVIEW_REQUIRED for potentially genuine relationships with:

- unresolved identity
- ambiguous direction
- state conflict
- connectivity conflict
- unresolved semantic duplicate
- document-subject issue
- Medium evidence with a material unresolved question
- other clearly documented governance issue

Persist the exact review reason.

Do NOT put obviously weak co-mentions into REVIEW_REQUIRED.

Weak/noisy observations should simply not become relationship candidates or should be rejected at extraction control.

We do NOT want another 30,000-row review queue.

==================================================
25. REJECTED / SUPPRESSED OBSERVATIONS
==================================================

Maintain statistics about suppressed observations, including:

- co-mention only
- invalid entity
- fragment entity
- unsupported relationship semantics
- taxonomy mismatch
- ambiguous endpoints
- duplicate evidence
- insufficient evidence strength

But do not create full canonical-style relationship rows for obviously weak observations unless needed for diagnostic statistics.

==================================================
26. BUILD V3 AS NEW DATASET
==================================================

Create a new candidate dataset.

Suggested name:

LENDING_CANONICAL_V3_CANDIDATE

or repository-equivalent naming.

Do not overwrite:

- V1
- V2
- original SQLite
- original relationship JSON
- source files

V3 should be independently traceable to the original documents.

==================================================
27. DO NOT USE SEC / R2D2 / WEB YET
==================================================

This stage is CAM-only.

SEC/R2D2/Web will be added AFTER V3 CAM extraction passes validation.

Do not use external sources to rescue weak CAM observations.

Do not use external sources to reduce the old 32k dataset.

==================================================
28. FULL VALIDATION
==================================================

Validate every V3 canonical relationship.

For every canonical row verify:

1. valid subject identity
2. valid related entity identity
3. explicit relationship evidence
4. approved taxonomy
5. correct direction
6. supported state
7. supported connectivity
8. path completeness if indirect
9. exact source document
10. source hash
11. page/paragraph/table location
12. exact evidence excerpt
13. evidence strength
14. no unresolved contradiction
15. no semantic duplicate
16. complete provenance
17. no CCR evidence
18. non-empty validation reason
19. non-empty quality metadata

==================================================
29. REQUIRED BEFORE/AFTER EXTRACTION STATISTICS
==================================================

Generate a detailed report.

A. DOCUMENTS

- physical source files
- unique contents
- exact duplicate groups
- subject clients
- resolved subjects
- unresolved subjects
- documents parsed
- failed documents

B. RAW EXTRACTION

Report:

- total entity mentions observed
- genuine entities retained
- fragment/non-entity observations suppressed

- raw possible relationship observations encountered
- suppressed because co-mention only
- suppressed because invalid entity
- suppressed because relationship semantics absent
- suppressed because taxonomy unsupported
- suppressed because evidence insufficient
- repeated evidence consolidated

C. V3 CANDIDATE POPULATION

- total unique candidate relationships
- average candidates per unique CAM
- median candidates per CAM
- maximum candidates for one CAM
- minimum candidates for one CAM

This must be compared explicitly with OLD candidate count:
~32,957

Calculate percentage reduction.

Do NOT aim for an arbitrary reduction target.
Explain the cause of the reduction.

D. EVIDENCE STRENGTH

- HIGH
- MEDIUM
- INSUFFICIENT/suppressed

E. V3 RESULTS

- canonical
- review required
- rejected/suppressed

F. TAXONOMY

Canonical count by relationship type.

G. SUBJECT COVERAGE

For each of the ~42 CAM subject clients:

- CAGID
- client
- unique source documents
- extracted direct relationships
- extracted hidden relationships
- canonical
- review required
- evidence count

H. DIRECT / HIDDEN

- canonical direct
- canonical hidden/indirect
- hidden paths complete
- hidden paths missing path

Target:
canonical hidden relationships missing paths = 0

I. ENTITY QUALITY

- total unique V3 entities
- CAGID-backed
- non-CAGID genuine external entities
- unresolved
- fragment entities in canonical set

Target:
fragment entities in canonical = 0

J. DIRECTION

- subject→related
- related→subject
- bidirectional
- unresolved routed to review

Check for suspicious direction fallback.

K. STATE

- current
- emerging
- historical
- terminated
- unresolved state conflicts

L. DUPLICATES

- exact duplicates
- semantic duplicates
- repeated evidence consolidated
- duplicate canonical rows remaining

Target:
0 duplicate canonical rows

M. EVIDENCE

- evidence records
- average evidence items per canonical relationship
- single-evidence canonical relationships
- multi-evidence canonical relationships
- source/hash/location/excerpt failures

N. COMPARISON TO OLD PIPELINE

Report:

OLD:
32,957 candidates
767 old canonical
916 old review-required
31,274 old rejected

V3:
X candidates
X canonical
X review-required
X rejected/suppressed

Explain why V3 differs.

==================================================
30. RELATIONSHIP EXAMPLES
==================================================

Provide at least:

- 10 representative HIGH-confidence canonical examples
- 10 representative MEDIUM-confidence examples
- all hidden/indirect examples if ≤20
- otherwise top 20 hidden examples

For each show:

subject
related entity
type
direction
state
direct/hidden
evidence strength
source file
page/location
short supporting excerpt
path if hidden

Do not expose more source text than necessary.

==================================================
31. EXCEPTION REGISTER
==================================================

Produce all remaining review issues.

Fields:

exception_id
source_file
document_subject
subject_entity
related_entity
relationship_type
failure_reason
evidence_strength
review_reason
recommended_action

==================================================
32. OUTPUT ARTIFACTS
==================================================

Create:

1. V3 candidate dataset
2. V3 statistics report JSON
3. V3 human-readable report MD
4. V3 exception register
5. V3 subject reconciliation report

Use clear filenames such as:

LENDING_CANONICAL_V3_CANDIDATE
LENDING_V3_EXTRACTION_REPORT.json
LENDING_V3_EXTRACTION_REPORT.md
LENDING_V3_EXCEPTION_REGISTER.csv
LENDING_V3_SUBJECT_RECONCILIATION.csv

==================================================
33. FINAL ACCEPTANCE TEST
==================================================

V3 CAM EXTRACTION is acceptable only if:

- old 32,957 candidate population was NOT reused
- extraction was rerun from original narrative sources
- no co-mention-only canonical relationships
- no narrative fragments as canonical entities
- canonical relationships have explicit evidence
- one semantic relationship does not appear repeatedly
- all hidden relationships have complete paths
- no hidden path contains unsupported hop
- no canonical relationship has unresolved identity
- no unresolved material contradiction remains canonical
- evidence provenance is complete
- no CCR contamination
- V1 unchanged
- V2 unchanged
- V5 not promoted to relationship evidence
- statistics report produced

==================================================
34. FINAL RESPONSE
==================================================

When complete return:

LENDING V3 PRECISION EXTRACTION: PASS / FAIL

Unique CAM contents:
Physical CAM subject clients:

OLD candidate population:
V3 candidate population:
Candidate reduction:

V3 canonical relationships:
V3 review-required:
V3 rejected/suppressed:

HIGH evidence:
MEDIUM evidence:

Direct canonical:
Hidden canonical:
Hidden with complete path:
Hidden missing path:

Unique entities:
CAGID-backed entities:
Valid external non-CAGID entities:
Fragment entities in canonical:

Unresolved canonical endpoints:
Direction conflicts:
State conflicts:
Connectivity conflicts:
Semantic duplicate canonical rows:

Documents with resolved subjects:
Documents with unresolved subjects:

CCR contamination:
0 / non-zero

V1 unchanged:
PASS / FAIL

V2 unchanged:
PASS / FAIL

V5 relationship evidence used:
NO / YES

Statistics report:
<path>

Exception register:
<path>

V3 candidate:
<path>

V3 CAM DATA READY FOR EXTERNAL CORROBORATION:
YES / NO

If NO:
list only the blocking controls.

Then STOP.
