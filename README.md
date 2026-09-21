SubjectEntity: COREWEAVE INC
RelatedEntity: NVIDIA CORP
RelationshipScope: technology_dependency,supplier
SourceChannels: R2D2_WEB,SEC_FILING
ResearchInstruction:
Validate whether CoreWeave has an explicit supplier and/or material technology dependency relationship with NVIDIA. Use only strong authoritative or high-quality sources. Return separate atomic findings for each supported relationship type. Do not infer from co-mention. Identify conflicts or insufficient evidence explicitly.

AsOfDate: your current analysis date.


NEW CAM CAGID POPULATION FILE — READ-ONLY RECONCILIATION

A new file has been added to the Lending project:

CAM CAGIDs List_20260918.xlsx

This file was supplied by the Tech/CAM data team together with reported
portfolio statistics.

YOUR TASK IS READ-ONLY ANALYSIS ONLY.

DO NOT:
- modify this workbook;
- modify any other source workbook;
- modify SQLite;
- modify V1;
- modify V2;
- modify V3;
- rerun CAM relationship extraction;
- change the 13 V3 canonical relationships;
- change the 28 V3 review relationships;
- call SEC;
- call R2D2;
- call Web;
- change the Stylus preset;
- modify the frontend/UI;
- touch CCR.

This analysis is intended ONLY to establish what population this workbook
represents, validate the colleague-provided statistics, and determine how it
relates to the existing Lending populations.

Proceed autonomously and complete the entire analysis.

==================================================
1. FILE IDENTITY
==================================================

Report:

- exact path
- file size
- SHA256
- workbook sheets
- rows/columns per sheet
- headers
- data types
- null counts
- duplicate rows
- duplicate CAGIDs
- unique CAGIDs
- relevant date/as-of metadata
- workbook creator/modification metadata if available

Do not infer scope from filename alone.

==================================================
2. DETERMINE WHAT POPULATION THIS IS
==================================================

Determine whether the workbook represents:

- full Lending population;
- CAM-priority population;
- AI ecosystem population;
- underwriting population;
- credit portfolio subset;
- prior CAM Priority Population Batch 1;
- a new broader CAM-control population;
- or another scope.

Use workbook contents and existing local reference files to determine this.

Explicitly compare against:

1. CAM Priority Population_Batch 1.xlsx
2. AI Economy Study_Masterfile.xlsx
3. Core AI CAMs.xlsx
4. CAM Data sheet in AI Economy Study_Masterfile.xlsx
5. v5-All-CAGIDs.xlsx
6. Citi Data Layer_July ME 2026.xlsx
7. Customer_latest.parquet where useful for exact-CAGID reference

Do not use relationship data to infer population membership.

==================================================
3. VALIDATE THE REPORTED 2,484 POPULATION
==================================================

The colleague reported:

TOTAL PORTFOLIO:
2,484 CAGIDs

CAM DATA AVAILABLE:
1,698 CAGIDs

NO CAM DATA:
786 CAGIDs

1 CAM:
928 CAGIDs

2 CAMs:
770 CAGIDs

Validate these numbers directly from the workbook.

Report independently:

- physical rows
- distinct CAGIDs
- duplicates
- 1-CAM count
- 2-CAM count
- >2 CAM count if any
- no-CAM count
- total with CAM
- total without CAM

Check all arithmetic:

928 + 770 = 1,698
1,698 + 786 = 2,484

Do not assume the email numbers are correct merely because they were supplied.

==================================================
4. VALIDATE OSUC STATISTICS
==================================================

The colleague reported approximately:

TOTAL PORTFOLIO OSUC:
$349.27B

CAM-COVERED OSUC:
$259.93B
74.42%

NO-CAM OSUC:
$89.33B
25.58%

1-CAM OSUC:
$124.90B
35.76%

2-CAM OSUC:
$135.04B
38.66%

Recalculate all values from source where the workbook contains sufficient
data.

Determine:

- exact OSUC field used
- reporting/as-of date
- whether OSUC is already aggregated per CAGID
- whether multiple rows/facilities require aggregation
- whether values are net of hedges
- whether multiple reporting periods exist

CRITICAL:

Never sum the same CAGID across multiple reporting periods.

Use one consistent reporting period/as-of date.

Reconcile totals and percentages.

If the workbook does not itself contain OSUC and the colleague statistics
must have been joined to another source:
state that explicitly and identify the likely local source only if evidence
supports it.

==================================================
5. COMPARE TO THE PREVIOUS 2,484 FILE
==================================================

Earlier repository analysis identified:

CAM Priority Population_Batch 1.xlsx

with approximately:
- 2,484 rows
- 2,482 unique CAGIDs

Compare it directly against the new file.

Report:

- exact CAGID intersection
- CAGIDs only in old file
- CAGIDs only in new file
- whether the two files represent the same population
- whether duplicates explain the 2,484 vs 2,482 distinction
- changes in CAM coverage
- changes in OSUC where comparable
- changes in sector/rating/status where comparable

Determine whether the new workbook should be understood as:
- an updated version of that population;
- a CAM-coverage enrichment of that population;
- a different population.

==================================================
6. RECONCILE ALL KNOWN LENDING POPULATIONS
==================================================

Create one population hierarchy/reconciliation table containing:

POPULATION
DISTINCT CAGIDS
OVERLAP WITH 2484
NOT IN 2484
DESCRIPTION / ROLE

Include:

- New CAM CAGIDs population
- CAM Priority Population Batch 1
- AI Economy Masterfile population = approximately 418
- Technology population = approximately 343
- CoreAI population = approximately 75
- CoreAI tracker = approximately 72
- CAM Data = approximately 346
- V5 = approximately 346
- physical CAM subject clients = approximately 42

Recalculate all numbers rather than hardcoding them.

==================================================
7. CRITICAL 418 VS 2,484 QUESTION
==================================================

Determine explicitly:

What is the relationship between:

418 AI Economy Study clients

and

2,484 CAM-priority/portfolio CAGIDs?

Report:

- exact overlap
- 418 clients present in 2,484
- 418 clients absent from 2,484
- 2,484 clients outside the 418
- CoreAI overlap
- Technology overlap

Then state which interpretation is supported:

A. 418 is the full Lending population.
B. 418 is a specific AI/Technology subset of a broader 2,484 portfolio.
C. They represent different populations and neither contains the other fully.
D. Other — explain.

Do NOT change any application denominator yet.

==================================================
8. CAM COVERAGE CONCEPT
==================================================

Determine exactly what:

"has CAM data"

means in the new workbook.

Distinguish:

- CAM metadata availability
- digital CAM data availability
- physical PDF/DOCX CAM supplied locally
- CCM availability
- one CAM
- two CAMs
- current/active CAM
- historical CAM

The colleague's email states CAM data includes CCM.

Confirm how this is represented in the workbook.

Do NOT equate "digital CAM data available" with "physical CAM document
present in this repository."

==================================================
9. COMPARE AGAINST THE 42 PHYSICAL CAM SUBJECTS
==================================================

Check all approximately 42 physical CAM subject clients against the new
2,484 population.

Report:

- exact CAGID matches
- missing clients
- CAM count in new file
- CAM-data flag
- OSUC if available
- sector
- any conflicting status

This is comparison only.

Do not modify V3.

==================================================
10. COMPARE AGAINST V3
==================================================

V3 currently has:

- 13 canonical relationships
- 28 review-required relationships
- 0 unresolved document subjects

Do NOT modify these.

Report only:

- how many V3 subject clients appear in the new population
- how many V3 endpoint entities appear by CAGID
- whether the new workbook provides any new structured portfolio metadata
  useful later for:
  - exposure
  - CAM coverage
  - sector
  - portfolio prioritization

The new workbook is NOT relationship evidence.

==================================================
11. INDUSTRY STATISTICS
==================================================

The colleague reported CAM-covered population industry statistics including:

Technology:
464 CAGIDs
~$68.93B OSUC

Finance Companies - Indirect:
272
~$67.49B

Power:
184
~$32.83B

Capital Goods:
185
~$23.33B

Chemicals:
211
~$20.87B

Telecom:
81
~$20.75B

Metals & Mining:
130
~$10.93B

Finance Companies - Direct:
92
~$8.56B

Building Products & Related:
75
~$6.03B

Energy:
4
~$0.22B

Validate these from source if possible.

Report exact values and reconcile totals to:
1,698 CAM-covered CAGIDs
and approximately
$259.93B CAM-covered OSUC.

==================================================
12. AUTHORITATIVE USE ASSESSMENT
==================================================

Classify the new workbook separately for:

POPULATION AUTHORITY:
YES / SUPPLEMENTAL / NO

CAM COVERAGE AUTHORITY:
YES / SUPPLEMENTAL / NO

CAGID IDENTITY AUTHORITY:
YES / SUPPLEMENTAL / NO

OSUC AUTHORITY:
YES / SUPPLEMENTAL / NO

SECTOR AUTHORITY:
YES / SUPPLEMENTAL / NO

RELATIONSHIP EVIDENCE:
YES / NO

DOCUMENT SUBJECT AUTHORITY:
YES / NO

Explain each conclusion.

==================================================
13. UI / MATERIALITY READINESS — ANALYSIS ONLY
==================================================

Do NOT change the UI.

Determine whether this dataset could later support portfolio-level KPIs such
as:

- Total portfolio CAGIDs
- Total OSUC
- CAM-covered CAGIDs
- CAM-covered OSUC
- No-CAM exposure
- 1-CAM vs 2-CAM coverage
- sector exposure
- top exposure clients
- exposure concentration
- CAM coverage by materiality

State which KPIs are defensible from the available data and which are not.

Do NOT implement them.

==================================================
14. REQUIRED FINAL REPORT
==================================================

Finish with:

NEW CAM CAGID FILE ASSESSMENT

Distinct CAGIDs:
Rows:

Clients with CAM:
Clients without CAM:

1 CAM:
2 CAMs:
>2 CAMs:

Total OSUC:
CAM-covered OSUC:
No-CAM OSUC:

CAM-covered OSUC %:

Previous 2,484 population overlap:
418 Masterfile overlap:
343 Technology overlap:
75 CoreAI overlap:
72 CoreAI tracker overlap:
42 physical-CAM subject overlap:

Is 418 a subset of the broader population:
YES / NO / PARTIAL

Is the new file relationship evidence:
YES / NO

Population authority:
<classification>

CAM-coverage authority:
<classification>

OSUC authority:
<classification>

SAFE TO USE LATER FOR PORTFOLIO/UI ANALYTICS:
YES / NO / WITH CONDITIONS

SAFE TO MODIFY V3 RELATIONSHIPS:
NO

V1 unchanged:
PASS / FAIL

V2 unchanged:
PASS / FAIL

V3 unchanged:
PASS / FAIL

SEC/R2D2 preset unchanged:
PASS / FAIL

Then STOP.

DO NOT integrate anything yet.
