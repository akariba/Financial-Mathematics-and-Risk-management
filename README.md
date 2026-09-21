V5 CAGID FILE ANALYSIS — READ ONLY

I added two files to the Lending project:

1. v5-All-CAGIDs.xlsx
2. v5-All-CAGIDs.json

Your task is to analyze these files completely before they are used anywhere.

THIS IS READ-ONLY ANALYSIS ONLY.

DO NOT:
- modify either file;
- modify SQLite;
- modify any canonical relationship dataset;
- modify the frozen baseline;
- modify source CAM/PDF/DOCX files;
- rebuild relationships;
- change entity resolution yet;
- call R2D2;
- call SEC;
- call Web;
- touch CCR;
- touch the frontend.

Proceed autonomously.
Do not ask for confirmation.
Do not stop until the full analysis and statistics report are complete.

==================================================
1. IDENTIFY BOTH FILES
==================================================

For each file report:

- exact path
- file type
- file size
- SHA256
- modification metadata if available
- XLSX sheet names
- JSON top-level structure
- total rows / objects
- total columns / fields
- all column names / JSON keys
- data types
- null counts
- unique counts

Determine whether XLSX and JSON represent:
- exactly the same dataset;
- approximately the same dataset;
- different versions;
- different scopes.

Compare record-by-record where possible.

Report:
- records only in XLSX
- records only in JSON
- differing records
- duplicate rows
- duplicate CAGIDs
- duplicate names

==================================================
2. DETERMINE WHAT THESE FILES ACTUALLY ARE
==================================================

Do NOT infer only from the filename.

Inspect the contents and determine whether they are:

- a customer master;
- CAGID mapping file;
- entity master;
- alias table;
- Lending population;
- CAM population;
- relationship population;
- broad customer universe;
- manually curated mapping;
- derived artifact;
- earlier AI-generated output;
- cached data;
- something else.

Explain the evidence supporting your conclusion.

Determine what one row/object represents:
- one legal entity;
- one client relationship;
- one alias;
- one CAGID;
- one customer;
- one account;
- other.

==================================================
3. CAGID ANALYSIS
==================================================

Identify every field that may contain:

- CAGID
- client/entity name
- legal name
- short name
- alias
- parent name
- country
- industry
- identifier
- source
- status

Report:

- total distinct CAGIDs
- valid-looking CAGIDs
- missing CAGIDs
- malformed CAGIDs
- CAGIDs associated with multiple names
- names associated with multiple CAGIDs
- exact duplicate name+CAGID pairs
- normalized-name collision groups

Do NOT assume that a CAGID is authoritative just because it is present.

==================================================
4. COMPARE TO THE 418 LENDING BENCHMARK CLIENTS
==================================================

Use the current authoritative Lending benchmark population.

Compare v5 against the 418 clients.

Report:

- exact CAGID matches
- benchmark clients not found
- extra v5 CAGIDs outside the 418 population
- CoreAI 75 coverage
- Technology 343 coverage
- CoreAI tracker 72 coverage
- CAM Data 346 coverage

For each unmatched benchmark client report:

CAGID
benchmark_name
possible_v5_match
match_method
confidence
reason

Do not perform silent fuzzy matching.

==================================================
5. COMPARE TO THE 42 PHYSICAL CAM SUBJECT CLIENTS
==================================================

This is a critical section.

Compare v5 against the 42 unique client companies represented by the supplied CAM/credit narrative documents.

Report:

- exact CAGID matches
- exact legal-name matches
- alias matches
- unmatched CAM subjects
- conflicting CAGID assignments
- multiple candidate matches

Create a table:

CAM_CLIENT
CURRENT_CAGID
V5_CAGID
V5_NAME
MATCH_TYPE
MATCH_CONFIDENCE
CONFLICT
NOTES

Specifically inspect the known problematic document subjects, including:

- Compass Creek
- Bridge Data Centres Malaysia / Coral II
- Red Chiles Campus / Project Miner
- Corellia / Project Corellia / AirTrunk
- Southgate Two
- Project FIN 01
- Project Belmont
- Project Indigo / CoreWeave Compute Acquisition
- Amidala

For each, show exactly what v5 contains and whether it can safely resolve the identity.

==================================================
6. COMPARE TO CURRENT SQLITE ENTITIES
==================================================

Current Lending SQLite contains approximately 31k entity records.

Compare v5 against the existing entity universe.

Report:

- SQLite entities matched by exact CAGID
- SQLite entities matched by exact normalized legal name
- SQLite entities not found
- v5 entities not present in SQLite
- name-only SQLite entities that could be safely resolved using v5
- ambiguous SQLite entities where v5 gives multiple candidates
- entity collisions that v5 may help resolve

Do NOT automatically assign any CAGIDs.

Analysis only.

==================================================
7. TEST POTENTIAL IMPACT ON CURRENT CANONICAL RELATIONSHIPS
==================================================

Use the existing relationship data only for diagnostic comparison.

Report current:

- canonical rows with both endpoints CAGID-backed
- canonical rows with one CAGID-backed endpoint
- canonical rows with zero CAGID-backed endpoints

Then calculate POTENTIAL improvement using v5 ONLY where mapping is deterministic and defensible:

- both endpoints CAGID-backed
- one endpoint CAGID-backed
- zero endpoints CAGID-backed

Do NOT count fuzzy or ambiguous mappings as resolved.

Create a table for every current name-only endpoint that can be deterministically resolved:

RELATIONSHIP_ID
CURRENT_ENTITY_NAME
V5_CANONICAL_NAME
V5_CAGID
MATCH_BASIS
SAFE_TO_RESOLVE

==================================================
8. CHECK WHETHER V5 ITSELF CONTAINS RELATIONSHIPS
==================================================

Determine whether either file contains fields representing:

- parent/subsidiary
- ownership
- customer
- supplier
- guarantor
- lender
- sponsor
- investor
- affiliate
- facility linkage
- related party
- counterparty linkage

Classify these fields carefully as:

A. identity/reference metadata
or
B. actual relationship facts.

DO NOT promote any relationship information from v5 into CAM relationship truth.

CAM/PDF/DOCX narrative documents remain the authoritative relationship evidence source for this analysis.

==================================================
9. PROVENANCE / TRUST ASSESSMENT
==================================================

Inspect whether the files contain:

- source system
- extraction date
- as-of date
- creator
- source document
- confidence
- validation flag
- mapping method
- generation metadata

Determine whether each file appears to be:

- authoritative internal master data;
- manually curated mapping;
- derived code output;
- cached artifact;
- previous AI-generated mapping;
- unknown provenance.

If provenance cannot be established, report:

PROVENANCE = UNKNOWN

Do not classify the files as authoritative merely because they contain many CAGIDs.

==================================================
10. IDENTIFY DANGEROUS RECORDS
==================================================

Look for:

- sentence fragments stored as company names
- partial legal names
- truncated names
- generic terms
- aliases incorrectly represented as separate entities
- one CAGID assigned to unrelated companies
- one company assigned several CAGIDs
- corrupted identifiers
- blank legal names
- placeholder values
- duplicate entries

Explicitly check for suspicious names similar to:

- as of Company
- subject to Corp
- which is Company
- wholly owned holding
- with each bank
- by the Group

Report whether any such patterns occur.

==================================================
11. SAFE-USE CLASSIFICATION
==================================================

Classify each file separately as one of:

A. SAFE AS AUTHORITATIVE CAGID REFERENCE
B. SAFE AS SUPPLEMENTAL ENTITY RESOLUTION REFERENCE
C. SAFE ONLY FOR ALIAS MATCHING
D. USE ONLY FOR MANUAL REVIEW
E. DO NOT USE

Explain the reason for each classification.

==================================================
12. REQUIRED STATISTICS REPORT
==================================================

Produce a clear report with:

V5 FILE SUMMARY

XLSX rows:
JSON objects:

XLSX unique CAGIDs:
JSON unique CAGIDs:

Exact XLSX/JSON matches:
Differences:

418 Lending population coverage:
CoreAI 75 coverage:
Technology 343 coverage:
Tracker 72 coverage:
CAM Data 346 coverage:
42 physical-CAM client coverage:

SQLite entities exact-CAGID matched:
SQLite entities exact-name matched:

Current canonical endpoints potentially resolvable:
Still unresolved:
Conflicting mappings:

Duplicate CAGIDs:
Duplicate normalized names:
Ambiguous mappings:
Suspicious entity names:

Known document-subject mismatches potentially solved:
Known document-subject mismatches not solved:

Relationship information present:
YES / NO

Provenance:
AUTHORITATIVE / DERIVED / UNKNOWN

==================================================
13. FINAL DECISION
==================================================

Finish with exactly:

V5 XLSX RECOMMENDATION:
<classification>

V5 JSON RECOMMENDATION:
<classification>

FILES REPRESENT SAME DATA:
YES / NO / PARTIAL

CAN HELP ENTITY RESOLUTION:
YES / NO

CAN HELP DOCUMENT SUBJECT RESOLUTION:
YES / NO

CAN BE USED AS RELATIONSHIP EVIDENCE:
YES / NO

SAFE TO INTEGRATE INTO FUTURE V3 EXTRACTION:
YES / NO / ONLY WITH CONDITIONS

If conditional, list the precise conditions.

DO NOT integrate the files yet.

STOP after the analysis and statistics report.
