STOP ALL UI WORK.

Perform a COMPLETE READ-ONLY FORENSIC AUDIT of the Lending relationship data, source corpus, ingestion pipeline, database construction, entity extraction, relationship classification, evidence lineage, and benchmark/reference population.

LENDING ONLY.

DO NOT:
- modify the frontend;
- modify the Lending database;
- rebuild or re-ingest anything;
- modify the frozen baseline;
- modify source documents;
- call R2D2;
- run external research;
- inspect CCR business data;
- change parsers or classification logic;
- repair failures;
- automatically retry failed files;
- loop.

This is ONE read-only audit pass.

The objective is to determine whether we genuinely have a reliable Lending relationship database and to understand exactly how it was produced.

======================================================================
1. COMPLETE SOURCE CORPUS INVENTORY
======================================================================

Start from the filesystem, not from the database.

Enumerate ALL files that could belong to the Lending corpus.

For every relevant directory/folder report:

- absolute or workspace-relative folder path;
- purpose if determinable;
- number of files;
- file extensions;
- total size;
- whether the ingestion pipeline scans it;
- whether files from it were actually processed;
- whether files from it were ignored;
- reason for ignored files if known.

Do not assume only one folder contains Lending documents.

Identify:
- root Lending source folders;
- nested folders;
- manually supplied documents;
- CAM folders;
- approval memo folders;
- annual review folders;
- quarterly review folders;
- credit committee documents;
- Excel/workbook reference files;
- CSV files;
- DOCX;
- PDF;
- XLSX;
- TXT/MD reference/configuration files;
- JSON artifacts;
- SQLite artifacts.

For the entire Lending source corpus return:

FILES DISCOVERED
FILES ELIGIBLE
FILES PROCESSED
FILES SUCCESSFULLY PARSED
FILES PARTIALLY PARSED
FILES SKIPPED
FILES FAILED
FILES DUPLICATED
FILES SUPERSEDED BY NEWER VERSION
FILES WITH UNKNOWN STATUS

Reconcile these counts.

======================================================================
2. CAM DOCUMENT COVERAGE
======================================================================

Determine exactly how many CAM-related documents were discovered.

Break them down by identifiable CAM/document type where possible, for example:

- Initial CAM
- Annual Review
- Quarterly Review
- CCM
- Credit Approval Memo
- Credit Committee Memo
- Re-approval
- Amendment
- Extension
- Other Lending credit document
- Unknown / cannot classify

For every document classify:

- source filename;
- source folder;
- detected document type;
- client/entity;
- CAGID if available;
- document date;
- current/stale/unknown;
- pages or rows;
- parser used;
- parsing status;
- sections extracted;
- whether relationship-bearing evidence was found.

Report:

TOTAL CAM / CREDIT DOCUMENTS FOUND: X
CURRENT CAM DOCUMENTS: X
STALE CAM DOCUMENTS: X
UNRESOLVED DOCUMENTS: X
DOCUMENTS WITH NO ENTITY RESOLUTION: X
DOCUMENTS WITH NO RELATIONSHIP EVIDENCE: X
DOCUMENTS FAILED TO PARSE: X

Do not count duplicate versions as independent current CAMs without explicitly identifying them.

======================================================================
3. REFERENCE POPULATION / BENCHMARK
======================================================================

Identify the actual benchmark/reference population used when the Lending database was created.

Do NOT invent a benchmark.

Determine whether the implementation used any of the following:

- AI Economy Study Masterfile.xlsx
- another master client list;
- CAGID master population;
- frozen Lending baseline;
- source inventory;
- relationship taxonomy;
- manually supplied population files;
- any other reference file.

For every benchmark/reference source report:

- filename;
- path;
- purpose;
- number of rows/entities;
- identifiers available;
- whether it was actually used by code;
- where in the code it is loaded;
- whether it determines the target population;
- whether it was merely informational.

If the AI Economy Study Masterfile is present, explicitly verify the expected population from the actual file.

Check whether the historical working reference of approximately:
- 418 CAGIDs total
- 75 CoreAI
- 343 Technology

is actually supported by the file currently present.

Do not assume these numbers are correct; verify them.

Then reconcile:

REFERENCE POPULATION
vs
CAM COVERAGE
vs
DATABASE ENTITY POPULATION
vs
CLIENTS WITH VALIDATED RELATIONSHIPS

Return exact gaps.

======================================================================
4. HOW THE VS CODE IMPLEMENTATION READ THE DATA
======================================================================

Trace the actual ingestion path through the repository.

Explain technically, but concisely:

SOURCE FILE
→ discovery
→ file-type detection
→ parser
→ text/table extraction
→ section identification
→ subject/client resolution
→ related-entity extraction
→ relationship candidate extraction
→ relationship classification
→ evidence creation
→ canonical/review/rejected decision
→ SQLite persistence
→ JSON artifacts
→ backend/API response
→ frontend

Identify the exact files/modules/functions responsible for each stage.

For example, determine which actual modules perform:

- file discovery;
- PDF parsing;
- DOCX parsing;
- XLSX parsing;
- CSV parsing;
- section detection;
- entity extraction;
- entity resolution;
- CAGID matching;
- relationship extraction;
- taxonomy mapping;
- evidence extraction;
- confidence determination;
- materiality determination;
- canonical validation;
- review-queue assignment;
- rejection;
- database persistence.

Do not describe intended architecture.
Describe what the CURRENT CODE ACTUALLY DOES.

======================================================================
5. PARSER / FILE-TYPE QUALITY
======================================================================

Audit every supported file type separately.

For PDF:
- Were all pages extracted?
- Any image-only/scanned PDFs?
- Any empty pages?
- Any garbled text?
- Any table extraction failures?
- Any pages silently skipped?

For DOCX:
- Were paragraphs extracted?
- Were tables extracted?
- Were headers/footers relevant?
- Were embedded tables missed?

For XLSX:
- Which sheets were read?
- Were hidden sheets ignored?
- Were merged cells handled?
- Were formulas read as formulas or values?
- Were all relevant entity-bearing rows captured?

For CSV:
- encoding;
- delimiter;
- schema;
- row count;
- missing identifiers;
- whether it was Lending-relevant.

For each file type report:

FILES FOUND
FILES PARSED
FILES FAILED
CONTENT COVERAGE
KNOWN LIMITATIONS
POTENTIAL DATA LOSS

======================================================================
6. DOCUMENT CLASSIFICATION ACCURACY
======================================================================

Verify whether the system correctly classified each document.

Check:
- client name;
- document type;
- document date;
- current/stale status;
- source subject;
- CAGID;
- Lending relevance.

Identify files whose inferred classification is wrong or uncertain.

Examples of failure:
- a Quarterly Review labelled Annual Review;
- project name mistaken for company name;
- facility name mistaken for company;
- section heading mistaken for entity;
- narrative text mistaken for entity;
- unrelated workbook treated as CAM.

======================================================================
7. SECTION EXTRACTION COVERAGE
======================================================================

Determine which sections of CAM/credit documents were detected and used.

Specifically check coverage of sections such as:

- Recommendation
- Approval Request
- Relationship / Obligor Structure
- Key Risks and Mitigants
- Historical Financial Analysis
- Outlook and Projections
- Sources of Repayment
- Risk Rating and Classification Assessment
- ORR Overview
- Support
- FRR Overview
- Cluster Analysis
- Classification

For each relevant section report:

DOCUMENTS WHERE SECTION EXISTS
DOCUMENTS WHERE SECTION WAS DETECTED
DOCUMENTS WHERE SECTION WAS MISSED
RELATIONSHIPS EXTRACTED FROM SECTION

Identify whether the system concentrated disproportionately on one section and ignored relationship evidence elsewhere.

======================================================================
8. ENTITY EXTRACTION QUALITY
======================================================================

Audit every extracted entity.

Separate:

A. valid legal/company entities
B. valid funds/SPVs/holding vehicles
C. valid lenders/sponsors/regulators/etc.
D. unresolved entities
E. narrative fragments incorrectly treated as entities
F. headings incorrectly treated as entities
G. descriptions incorrectly treated as entities
H. duplicate aliases
I. ambiguous entities

Explicitly search for bad extracted names similar to:

- "supported by company"
- "which is Company"
- "wholly owned holding"
- "as the company"
- "real estate company"
- "given the limited"
- "who directs all activities of the Company"
- sentence fragments
- clause fragments
- generic nouns

Report every such occurrence.

For entity quality return:

TOTAL EXTRACTED ENTITIES
VALID ENTITIES
RESOLVED ENTITIES
UNRESOLVED ENTITIES
AMBIGUOUS ENTITIES
TEXT-FRAGMENT ENTITIES
DUPLICATE/ALIAS ENTITIES

======================================================================
9. ENTITY RESOLUTION / CAGID QUALITY
======================================================================

Audit how entity resolution works.

Determine:
- exact-match logic;
- alias matching;
- canonical-name matching;
- CAGID matching;
- whether fuzzy matching exists;
- whether fuzzy matching created false matches;
- treatment of external/non-client entities;
- treatment of subsidiaries/SPVs/funds.

For every Lending portfolio client verify:
- canonical name;
- CAGID;
- source reference;
- correct mapping.

Report:

CLIENTS WITH VALID CAGID
CLIENTS WITHOUT CAGID
DUPLICATE CAGIDs
MULTIPLE ENTITIES USING SAME CAGID
ENTITY NAME CONFLICTS
UNRESOLVED PORTFOLIO CLIENTS

======================================================================
10. RELATIONSHIP EXTRACTION ACCURACY
======================================================================

Audit ALL relationship candidates, not only the canonical 767.

Break the population into:

TOTAL CANDIDATES
CANONICAL / VALIDATED
REVIEW REQUIRED
REJECTED
MENTION ONLY
OTHER / UNKNOWN

For every canonical relationship verify:

- subject entity valid;
- related entity valid;
- relationship type supported;
- direction supported;
- state supported;
- connectivity supported;
- confidence justified;
- materiality justified if populated;
- evidence exists;
- source exists;
- excerpt exists;
- excerpt supports relationship.

Also analyze the rejected population.

Determine why the approximately 31k rejected/candidate records exist if that count remains current.

Group rejection reasons, e.g.:

- co-mention only;
- invalid entity;
- unsupported relationship;
- duplicate;
- insufficient evidence;
- taxonomy mismatch;
- ambiguous resolution;
- stale evidence;
- parsing artifact;
- narrative fragment;
- other.

Return counts by rejection reason.

======================================================================
11. RELATIONSHIP TAXONOMY QUALITY
======================================================================

Verify that every relationship maps to the approved Lending taxonomy only.

Report counts by relationship type.

For each type calculate:

CANDIDATES
CANONICAL
REVIEW REQUIRED
REJECTED

Identify suspicious patterns such as:
- one source passage creating many unrelated relationship types;
- same entity pair classified simultaneously into implausible types;
- generic wording creating Guarantor + Parent + Subsidiary + M&A Target + Strategic Partner from the same text;
- relationship type inferred from taxonomy keywords rather than explicit evidence.

Flag these as potential systematic extraction defects.

======================================================================
12. EVIDENCE LINEAGE / PROVENANCE
======================================================================

For every canonical relationship trace:

relationship
→ evidence record
→ exact excerpt
→ source section
→ source page/location
→ source document
→ source file on disk

Verify every link.

Report:

CANONICAL RELATIONSHIPS WITH COMPLETE LINEAGE
MISSING SOURCE FILE
MISSING PAGE/SECTION
MISSING EXACT EXCERPT
EXCERPT DOES NOT SUPPORT ENTITY PAIR
EXCERPT DOES NOT SUPPORT RELATIONSHIP TYPE
WRONG DOCUMENT LINK
DUPLICATE EVIDENCE
MULTIPLE RELATIONSHIPS DERIVED FROM SAME UNSUITABLE EXCERPT

======================================================================
13. CROSS-DOCUMENT BEHAVIOR
======================================================================

Audit whether cross-document relationship discovery actually works.

Report:

SUBJECT_DOCUMENT relationships
CROSS_DOCUMENT relationships
MULTI_DOCUMENT relationships

If current counts are zero, determine WHY.

Possible causes to investigate:
- feature intentionally disabled;
- source documents not linked;
- entity resolution prevents cross-document joins;
- insufficient evidence;
- code path not implemented;
- test data unavailable.

Do not fabricate cross-document relationships.

======================================================================
14. DUPLICATES / CONTRADICTIONS
======================================================================

Detect:

- exact duplicate relationships;
- duplicate pair/type relationships;
- same evidence copied multiple times;
- same pair with conflicting states;
- same pair with conflicting direction;
- same pair with conflicting connectivity;
- parent/subsidiary contradictions;
- current vs terminated conflicts;
- duplicate documents/versions creating duplicate records.

Return exact counts and affected record IDs.

======================================================================
15. REVIEW QUEUE QUALITY
======================================================================

Audit all review-required relationships.

Determine:
- why each entered review;
- whether reason is valid;
- whether any should clearly have been rejected;
- whether any canonical relationship accidentally remains in review;
- whether any review record leaked into trusted CAM results.

Report:

TOTAL REVIEW REQUIRED
VALID REVIEW CASES
LIKELY FALSE-POSITIVE REVIEW CASES
UNRESOLVED ENTITY CASES
INSUFFICIENT EVIDENCE CASES
CONFLICT CASES
OTHER

======================================================================
16. CCR ISOLATION
======================================================================

Do not open or analyze CCR business data.

Instead inspect ONLY Lending provenance, source paths, metadata, configuration, and database rows for signs that CCR sources entered the Lending pipeline.

Look for:
- /ccr/ paths;
- CCR filenames;
- CCR CSV provenance;
- CCR-specific schema fields;
- records whose source inventory classifies them as CCR.

Report any Lending records contaminated by CCR source provenance.

======================================================================
17. DATABASE / ARTIFACT RECONCILIATION
======================================================================

Reconcile counts across:

- source files;
- source inventory;
- SQLite;
- lending_relationship_database.json;
- frozen baseline JSON;
- quality report;
- API response;
- any current backend status endpoint.

Reconcile at least:

entities
documents
document versions
sections
evidence records
candidate relationships
canonical relationships
review-required relationships
rejected relationships
portfolio clients
connected entities

Explain every mismatch.

======================================================================
18. FROZEN BASELINE VALIDATION
======================================================================

Verify:

- frozen baseline file exists;
- checksum/hash if available;
- current persisted canonical relationship count;
- no records added;
- no records removed;
- no records modified;
- no external R2D2 evidence inserted into frozen CAM baseline.

Return:
BASELINE INTEGRITY: PASS / FAIL

======================================================================
19. DATA QUALITY TESTS
======================================================================

Perform systematic data-quality checks across the full Lending dataset.

Check:

COMPLETENESS
- missing subject;
- missing related entity;
- missing relationship type;
- missing evidence;
- missing source;
- missing document date;
- missing CAGID where expected.

VALIDITY
- invalid enum values;
- invalid dates;
- malformed CAGIDs;
- unsupported relationship types.

UNIQUENESS
- duplicate entities;
- duplicate relationships;
- duplicate evidence.

CONSISTENCY
- parent/subsidiary direction;
- current vs terminated;
- direct vs indirect;
- subject/related reversal;
- entity IDs vs names;
- CAGID consistency.

ACCURACY
- evidence supports classification;
- entity is correctly extracted;
- relationship is actually stated.

TIMELINESS
- stale CAM;
- superseded document;
- old evidence being represented as current.

LINEAGE
- every trusted relationship traceable to source.

======================================================================
20. SYSTEMATIC FAILURE PATTERN ANALYSIS
======================================================================

Do not look only for individual bad records.

Identify systematic causes.

Examples:

- regex extracting sentence fragments as entities;
- section parser misidentifying text;
- generic keyword mapping creating multiple relationship types;
- one passage creating five relationship types;
- incorrect subject/related orientation;
- stale documents overriding newer documents;
- workbook rows creating phantom entities;
- alias resolver overmatching;
- failure to distinguish legal entity from descriptive text;
- evidence parser truncating context;
- relationship state inferred incorrectly;
- indirect relationship assigned by default;
- confidence always set HIGH;
- materiality populated without source support.

For every systematic issue report:

ISSUE
ROOT CAUSE / LIKELY CODE PATH
NUMBER OF RECORDS AFFECTED
SEVERITY
EXAMPLE RECORD IDs

Do not fix it.

======================================================================
21. BLOCKERS AND LIMITATIONS
======================================================================

Explicitly identify anything that prevents a definitive audit.

Separate:

TECHNICAL BLOCKERS
DATA BLOCKERS
SOURCE-DOCUMENT BLOCKERS
ENTITY-RESOLUTION BLOCKERS
PARSER LIMITATIONS
MISSING REFERENCE DATA
MISSING HISTORICAL SNAPSHOTS
OTHER

Do not mark the database PASS if material accuracy cannot actually be verified.

======================================================================
22. FINAL OUTPUT
======================================================================

Return a structured audit report only.

Start with:

OVERALL LENDING DATABASE QUALITY: PASS / FAIL / PARTIALLY VERIFIED

Then:

A. SOURCE COVERAGE
- source folders discovered
- files discovered
- files processed
- files skipped
- files failed
- parsing coverage %

B. CAM COVERAGE
- CAM/credit documents found
- current
- stale
- unresolved
- failed
- clients with CAM
- clients without CAM

C. BENCHMARK POPULATION
- benchmark source
- expected entities
- matched entities
- unmatched entities
- coverage %

D. INGESTION QUALITY
- PDFs
- DOCX
- XLSX
- CSV
- parser failures

E. ENTITY QUALITY
- extracted entities
- valid
- unresolved
- ambiguous
- narrative fragments
- duplicate aliases

F. RELATIONSHIP QUALITY
- candidates
- canonical
- review required
- rejected
- mention only
- unsupported

G. CANONICAL ACCURACY
- checked
- valid
- invalid

H. EVIDENCE QUALITY
- complete lineage
- missing source
- missing excerpt
- unsupported excerpt
- wrong source
- duplicates

I. CLASSIFICATION QUALITY
- wrong relationship type
- wrong direction
- wrong state
- wrong connectivity
- unjustified confidence
- unjustified materiality

J. DATABASE RECONCILIATION
- SQLite vs JSON vs baseline vs API
- PASS / FAIL
- explain mismatches

K. ISOLATION
- CCR contamination detected: YES / NO

L. BASELINE
- frozen baseline unchanged: PASS / FAIL

M. SYSTEMATIC DEFECTS
List defects ordered by number of affected records.

N. BLOCKERS
List unresolved blockers.

O. DATA QUALITY SCORECARD
Do NOT invent a synthetic numeric score.
Use:
PASS
FAIL
PARTIALLY VERIFIED
NOT VERIFIABLE

for:
- completeness
- validity
- uniqueness
- consistency
- accuracy
- timeliness
- provenance
- entity resolution
- document coverage

P. EXCEPTION TABLE
Include ONLY failed/questionable records with:

record_id
subject_entity
related_entity
relationship_type
document
document_type
source_location
exact_excerpt_present
entity_issue
relationship_issue
evidence_issue
failure_reason
recommended_action

Do not execute recommended actions.

Q. TOP 10 FINDINGS

Return the ten most important factual findings from the audit.

Then STOP.

Do not repair.
Do not rebuild.
Do not rerun ingestion.
Do not change UI.
Do not loop.
