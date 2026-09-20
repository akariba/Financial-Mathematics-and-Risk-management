CONTINUE READ-ONLY DATA QUALITY AUDIT.

LENDING ONLY.
NO UI WORK.
NO CCR.
NO R2D2.
NO MODIFICATIONS.
NO REBUILD.
NO RE-INGESTION.

The source hierarchy and truth boundary are now established.

AUTHORITATIVE RELATIONSHIP EVIDENCE:
Only supplied narrative PDF/DOCX CAM, Annual Review, Quarterly Review,
Credit Approval, Credit Committee, and Facility/Financing documents may
establish a Lending relationship.

Structured workbooks may provide:
- population
- CAGID
- client/entity name
- CAM availability metadata
- exposure
- facility
- rating
- industry
- geography

They MUST NOT independently establish a relationship.

CURRENT DOCUMENT CORPUS:
- 48 narrative files
- determine exact unique-content count
- currently expected: 46 unique contents
- identify every duplicate explicitly

OBJECTIVE

Perform a complete document-to-database reconciliation.

PHASE 1 — DOCUMENT INVENTORY

For ALL 48 narrative files produce:

file_name
file_type
document_class
content_hash
duplicate_of
parse_status
page_count_or_docx_location_count
intended_client_name
intended_CAGID
resolved_database_entity
resolved_CAGID
subject_resolution_status
subject_resolution_reason

Do not infer an intended client merely from arbitrary text.
Use filename, document title/header, tracker/reference mapping and explicit
document identity together.

PHASE 2 — DOCUMENT COVERAGE

For every physical document determine:

candidate_relationships
validated_relationships
review_required_relationships
rejected_relationships

Flag:
- parsed but produced no candidates
- candidates but no validated relationships
- subject mismatch
- unresolved subject
- duplicate document
- document mapped to wrong CAGID
- document mapped to entity outside intended Lending population

PHASE 3 — CANONICAL RELATIONSHIP TRACEABILITY

Audit ALL 767 validated/canonical relationships.

For every relationship prove:

relationship_id
subject_entity
subject_CAGID
related_entity
related_CAGID_if_available
relationship_type
state
direction
connectivity
source_document
source_location
exact_evidence_excerpt

Then independently test:

A. subject is correct
B. related entity is a genuine legal/business entity
C. related entity is not narrative text
D. relationship type is explicitly supported
E. direction is explicitly supported
F. state is explicitly supported
G. connectivity is supported
H. evidence really occurs in source document
I. evidence contains/supports both endpoints
J. evidence supports the claimed relationship
K. source document belongs to the resolved subject
L. no contradictory evidence invalidates canonical status

DO NOT accept database status as proof.
Re-evaluate against the original document evidence.

PHASE 4 — ENTITY QUALITY

Specifically detect related entities that look like sentence fragments,
roles, clauses, or narrative phrases.

Examples include but are not limited to:

"as the company"
"which is Company"
"supported by company"
"wholly owned holding"
"by the Group"
"during the Company"
"will provide limited"
"borrower and holding"
"subject to Corp"

Return ALL such records, not examples only.

PHASE 5 — DUPLICATE CONTROL

Identify:

- exact duplicate files
- near-duplicate document versions
- duplicate evidence excerpts
- duplicate subject/related/type relationships
- duplicate semantic relationships with different entity IDs
- same normalized entity represented by multiple entity IDs

Do not delete anything.

PHASE 6 — COVERAGE RECONCILIATION

Keep these denominators separate:

1. 418 Masterfile Lending benchmark clients
2. 75 CoreAI population
3. 72 CoreAI CAM tracker rows
4. physical-document represented clients
5. 48 physical narrative files
6. unique narrative document contents
7. 767 canonical relationships

Do not call a benchmark client "missing CAM" unless the applicable
control/tracker explicitly establishes that a physical CAM document
was expected.

PHASE 7 — FINAL DATA QUALITY RESULT

Return:

DOCUMENT CORPUS
Total narrative files:
Unique contents:
Exact duplicates:
Parse failures:
Correctly resolved documents:
Incorrectly resolved documents:
Unresolved documents:

RELATIONSHIP QUALITY
Canonical relationships audited: 767
Fully supported:
Unsupported:
Invalid related entities:
Wrong subject:
Wrong relationship type:
Wrong direction:
Wrong state:
Wrong connectivity:
Evidence mismatch:
Source-subject mismatch:
Contradictory evidence:
Duplicate semantic relationships:

COVERAGE
418 benchmark population:
75 CoreAI population:
72 tracker population:
Tracker clients with physical documents:
Tracker clients without expected physical documents:
Tracker clients genuinely missing expected documents:
Physical-document clients with >=1 validated relationship:
Physical-document clients with zero validated relationships:

FINAL RESULT:
DATABASE FACTUAL ACCURACY: PASS / FAIL

Then output a failed-record exception table.

Do not modify anything.
STOP after the audit.
