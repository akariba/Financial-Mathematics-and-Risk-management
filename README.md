NEW INPUT FILE ANALYSIS — READ ONLY

I have added two new files to the Lending project:

1. v5-All-CAGIDs.xlsx
2. v5-All-CAGIDs.json

Before using either file anywhere, perform a COMPLETE READ-ONLY ANALYSIS of both files.

DO NOT:
- modify either file;
- modify SQLite;
- modify the canonical relationship dataset;
- modify the frozen baseline;
- modify source CAM/PDF/DOCX files;
- modify the 418-client population;
- rebuild relationships;
- change entity resolution yet;
- call R2D2;
- call SEC;
- call Web;
- touch CCR;
- touch the frontend.

The purpose of this task is ONLY to understand exactly what these two new files contain and whether they can safely help resolve the current Lending entity/CAGID problems.

Proceed autonomously and complete the full analysis.

==================================================
1. IDENTIFY THE FILES
==================================================

For each file report:

- exact path
- file type
- file size
- SHA256
- creation/modification metadata if available
- sheet names for XLSX
- JSON top-level structure
- total rows / objects
- total columns / fields
- column names / JSON keys
- data types
- null counts
- unique counts

Determine whether the XLSX and JSON represent:
- exactly the same dataset;
- approximately the same dataset;
- different versions;
- different scopes.

Compare them record-by-record where possible.

Report:
- records only in XLSX
- records only in JSON
- records differing between XLSX and JSON
- duplicate records
- duplicate CAGIDs
- duplicate names

==================================================
2. DETERMINE WHAT THE DATA REPRESENTS
==================================================

Do not infer from the filename.

Inspect the contents and determine whether this is:

- a customer master;
- CAGID mapping file;
- entity master;
- alias table;
- Lending population;
- CAM population;
- relationship population;
- broad Citi customer universe;
- manually curated mapping;
- derived artifact;
- or something else.

Explain exactly what evidence supports the conclusion.

Determine whether each row/object represents:
- one legal entity;
- one client relationship;
- one alias;
- one CAGID;
- one customer;
- one account;
- something else.

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
- CAGID appearing against multiple names
- names appearing against multiple CAGIDs
- exact duplicate name+CAGID pairs
- normalized-name collisions

Do NOT assume a CAGID is authoritative solely because it is present.

==================================================
4. COMPARE AGAINST CURRENT LENDING POPULATION
==================================================

Compare these files against the authoritative 418-client Lending benchmark.

Report:

- 418 benchmark clients found by exact CAGID
- 418 benchmark clients not found
- extra CAGIDs not in the 418 population
- CoreAI 75 coverage
- Technology 343 coverage
- CoreAI tracker 72 coverage
- CAM Data 346 coverage

For unmatched clients report:

CAGID
benchmark name
possible match in v5 file
match method
confidence
reason

Do not fuzzy-match silently.

==================================================
5. COMPARE AGAINST THE 42 CAM SUBJECT CLIENTS
==================================================

Compare against the 42 unique clients represented by the supplied CAM/credit documents.

Report:

- exact CAGID matches
- exact legal-name matches
- aliases found
- unmatched CAM subjects
- conflicting CAGID assignments
- multiple candidate matches

This is particularly important.

Determine whether the new files can help resolve the known document-subject mismatches.

Check specifically the previously problematic subjects such as:

- Compass Creek
- Bridge Data Centres Malaysia / Coral II
- Red Chiles Campus / Project Miner
- Corellia / Project Corellia / AirTrunk
- Southgate Two
- Project FIN 01
- Project Belmont
- Project Indigo / CoreWeave Compute Acquisition
- Amidala

For each, show exactly what v5 contains.

==================================================
6. COMPARE AGAINST SQLITE ENTITY UNIVERSE
==================================================

Current SQLite contains approximately 31k entity records.

Compare the new v5 data against those entities.

Report:

- SQLite entities matched by exact CAGID
- SQLite entities matched by exact normalized legal name
- SQLite entities not found
- v5 entities not present in SQLite
- current name-only SQLite entities that can now be safely CAGID-resolved
- current ambiguous entities where v5 gives multiple possibilities
- current entity collisions that v5 could help resolve

IMPORTANT:

Do not automatically assign CAGIDs yet.

This task is analysis only.

==================================================
7. TEST AGAINST THE 767 CURRENT CANONICAL RELATIONSHIPS
==================================================

Analyze how much these files could improve endpoint resolution.

Report:

BEFORE:
- canonical rows with both endpoints CAGID-backed
- one endpoint CAGID-backed
- zero endpoints CAGID-backed

POTENTIAL AFTER USING V5:
- both endpoints CAGID-backed
- one endpoint CAGID-backed
- zero endpoints CAGID-backed

But ONLY count a potential resolution where the mapping is deterministic and defensible.

Do not count fuzzy/ambiguous guesses.

List:
- relationships potentially resolvable using v5
- relationships still unresolved
- relationships where v5 creates a conflict

==================================================
8. DETECT WHETHER V5 CONTAINS RELATIONSHIPS
==================================================

Very important:

Determine whether either file itself contains relationship facts.

Look for:
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
- related-party fields

If such fields exist, classify them carefully as:

A. identity/reference metadata
or
B. actual relationship information.

DO NOT promote anything from these files into CAM relationship truth during this analysis.

The supplied narrative CAM/PDF/DOCX documents remain the authoritative relationship-evidence source unless explicitly established otherwise later.

==================================================
9. PROVENANCE / TRUST ASSESSMENT
==================================================

Determine whether the files themselves contain provenance such as:

- source system
- extraction date
- as-of date
- creator
- source document
- confidence
- validation flag
- mapping method

Assess whether these files appear to be:

- authoritative internal master data;
- manually curated mapping;
- derived output from earlier code;
- cached artifact;
- prior AI-generated entity mapping;
- unknown provenance.

This matters greatly.

If provenance cannot be established, state:

PROVENANCE = UNKNOWN

Do not call the file authoritative merely because it has many CAGIDs.

==================================================
10. IDENTIFY DANGEROUS RECORDS
==================================================

Look for:

- sentence fragments stored as company names
- partial legal names
- truncated names
- generic terms
- aliases incorrectly promoted as separate entities
- one CAGID assigned to clearly different companies
- one company assigned several CAGIDs
- corrupted identifiers
- blank legal names
- duplicate entries
- placeholder values

Examples of suspicious names:
- as of Company
- subject to Corp
- which is Company
- wholly owned holding
- with each bank
- by the Group

Report whether these appear in v5.

==================================================
11. DETERMINE SAFE USE CASE
==================================================

At the end classify each file as one of:

A. SAFE AS AUTHORITATIVE CAGID REFERENCE
B. SAFE AS SUPPLEMENTAL ENTITY RESOLUTION REFERENCE
C. SAFE ONLY FOR ALIAS MATCHING
D. USE ONLY FOR MANUAL REVIEW
E. DO NOT USE

Do this independently for:
- v5-All-CAGIDs.xlsx
- v5-All-CAGIDs.json

Explain why.

==================================================
12. REQUIRED STATISTICS REPORT
==================================================

Generate a concise but complete report with:

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

Current canonical endpoints potentially resolved:
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
13. REQUIRED OUTPUT TABLE — IMPORTANT
==================================================

Produce a table specifically for the 42 CAM-subject clients:

CAM_CLIENT
CURRENT_CAGID
V5_CAGID
V5_NAME
MATCH_TYPE
MATCH_CONFIDENCE
CONFLICT
NOTES

Then a second table containing every current canonical name-only endpoint that can be deterministically resolved using v5:

RELATIONSHIP_ID
CURRENT_ENTITY_NAME
V5_CANONICAL_NAME
V5_CAGID
MATCH_BASIS
SAFE_TO_RESOLVE

==================================================
14. FINAL DECISION
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

SAFE TO INTEGRATE INTO V2 REMEDIATION:
YES / NO / ONLY WITH CONDITIONS

If conditional, list the precise conditions.

DO NOT integrate the files yet.

STOP after the analysis and statistics report.
