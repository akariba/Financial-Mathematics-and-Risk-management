==================================================
CRITICAL BUSINESS BREAKDOWN — TWO BUSINESS LANES
==================================================

There are TWO distinct business lanes and they must remain clearly separated.

--------------------------------------------------
LANE 1 — LENDING BUSINESS
--------------------------------------------------

For Lending:

PRIMARY INTERNAL SOURCE:
- CAM

ADDITIONAL DISCOVERY / CORROBORATION SOURCE:
- R2D2 web research

Business logic:

CAM is the authoritative baseline for Lending relationships.

R2D2 may be used to:

- corroborate CAM relationships
- find additional evidence
- discover additional relationship types
- discover additional connected companies
- identify potential relationships not explicitly present in the currently available CAM data

However:

R2D2 must NEVER silently overwrite CAM.

The intended Lending flow is:

CAM relationships
    ↓
apply configurable relationship definitions
    ↓
R2D2 web discovery / corroboration
    ↓
entity reconciliation
    ↓
relationship reconciliation
    ↓
canonical relationship dataset
    ↓
portfolio table / graph / analyst review


--------------------------------------------------
LANE 2 — CCR BUSINESS
--------------------------------------------------

CCR is fundamentally different.

For CCR:

CAM IS NOT CURRENTLY AVAILABLE.

Therefore DO NOT assume CAM exists for CCR.

The current CCR source is:

1. The CCR CSV already attached / available inside the project folder
2. R2D2 web research for relationship discovery

IMPORTANT:

The CCR CSV is the population / counterparty universe.

It is NOT a CAM relationship source.

Use the existing CSV directly from the project folder.

Do NOT:

- convert it
- replace it
- create another copy unnecessarily
- change its structure
- rewrite the source file
- manufacture additional rows
- treat it as relationship evidence

First locate the existing CCR CSV in the repository/project folder.

Inspect its headers and reuse the fields already present.

The CSV should define the CCR companies/entities to analyze.

Use whatever identifiers and metadata already exist in the CSV, for example where available:

- CAGID
- counterparty / relationship name
- country
- risk rating
- credit classification
- industry L1
- industry L2
- industry L3
- exposure / OSUC or similar portfolio amount

Do not assume fields that are not actually present.

The CCR CSV is the portfolio universe.

R2D2 is then used to discover relationships among / around those CCR entities.


CCR intended flow:

CCR CSV
    ↓
load CCR entity universe
    ↓
select one or more configured relationship types
    ↓
use R2D2 web research
    ↓
discover evidence-backed relationships
    ↓
entity reconciliation
    ↓
relationship reconciliation
    ↓
structured CCR relationship dataset
    ↓
portfolio table / graph / analyst review


==================================================
IMPORTANT DIFFERENCE BETWEEN LENDING AND CCR
==================================================

LENDING:

CAM
+
R2D2 web

CAM is authoritative.

R2D2 is supplementary.


CCR:

CCR CSV
+
R2D2 web

There is currently NO CAM baseline.

Therefore CCR relationships discovered through R2D2 should be treated as:

EXTERNAL_PROPOSED

until reviewed or confirmed by an analyst.

Do NOT label CCR relationships as CAM_CONFIRMED.

Do NOT reuse Lending CAM relationships as if they were CCR CAM relationships.


==================================================
UI / BUSINESS LANE BEHAVIOR
==================================================

Preserve a clear Lending / CCR selector.

When user selects:

LENDING

show:

Source availability:
[x] CAM
[x] R2D2 Web

and relationship status can include:

CAM_CONFIRMED
EXTERNAL_CORROBORATED
EXTERNAL_PROPOSED
ANALYST_CONFIRMED
ANALYST_REJECTED


When user selects:

CCR

show:

Source availability:
[x] CCR CSV population
[x] R2D2 Web

CAM must NOT appear as an available CCR evidence source.

For CCR:

CSV = population source
R2D2 = relationship discovery source


==================================================
PORTFOLIO ANALYSIS — LENDING
==================================================

For Lending allow:

Population:
- all available CAM clients
- selected CAM clients

Relationship Types:
- multi-select configured relationship types

Sources:
[x] CAM
[x] R2D2 Web

Example:

Population:
Available Lending CAM population

Relationship Types:
[x] Contracted Customer
[x] Supplier
[x] Guarantor
[ ] Ownership
[x] Infrastructure Dependency

Run Relationship Analysis


==================================================
PORTFOLIO ANALYSIS — CCR
==================================================

For CCR:

Population must come from the existing CCR CSV.

Allow:

- all CCR CSV entities
- selected entities
- filtering using CSV metadata if already available

Examples of useful filters where supported by the CSV:

- country
- RRR / rating
- credit classification
- industry L1
- industry L2
- industry L3
- exposure / OSUC threshold

Then select relationship types:

[x] Customer Dependency
[x] Supplier
[x] Common Owner
[x] Sponsor
[x] Technology Dependency
[x] Infrastructure Dependency

Source:

[x] R2D2 Web

Run Relationship Analysis


==================================================
CCR RELATIONSHIP DISCOVERY
==================================================

For every selected CCR entity:

Use:

- canonical company name
- CAGID or internal identifier if available
- country
- industry
- other CSV metadata

to help establish entity identity.

Then use the configured relationship definition to instruct R2D2 what to search for.

Example:

Subject:
Company X

Relationship Type:
Critical Supplier

Objective:
Identify suppliers whose disruption could materially impact the subject company.

Inclusion:
- major supplier
- sole source
- important hardware / infrastructure supplier
- material dependency

Exclusion:
- incidental vendor
- generic partnership
- speculation
- unrelated share ownership

Ask R2D2 for evidence.

Return structured candidate relationships only.

If no sufficient evidence exists:

return no relationship.

Do NOT force a relationship.


==================================================
CCR OUTPUT
==================================================

For CCR structured output should include:

Subject CAGID
Subject Name
Related Entity
Relationship Type
Relationship Family
Direction
Subject Country
Subject Industry
Subject Rating / RRR if available
Subject Exposure / OSUC if available
Discovery Source
Evidence Summary
Evidence Reference
Confidence
Credit Relevance
Review State

For CCR:

Discovery Source = R2D2

Initial Review State = EXTERNAL_PROPOSED

unless an analyst explicitly confirms it.


==================================================
COMMON CONFIGURATION ACROSS BOTH LANES
==================================================

Use ONE relationship-type configuration framework across Lending and CCR.

Example configured relationship:

NAME:
Critical Supplier

FAMILY:
Operational Dependency

OBJECTIVE:
Identify suppliers whose disruption could materially impact operations or credit quality.

INCLUDE:
- material supplier
- sole-source dependency
- infrastructure dependency
- significant capacity dependency

EXCLUDE:
- incidental vendor
- generic partnership
- weak association
- unsupported inference

APPLICABLE BUSINESS LANES:

[x] Lending
[x] CCR

ALLOWED SOURCES:

Lending:
[x] CAM
[x] R2D2

CCR:
[x] R2D2

The same business relationship definition can therefore be reused across both populations, while the evidence sources differ.


==================================================
VERY IMPORTANT IMPLEMENTATION RULE
==================================================

Do NOT create two completely separate relationship engines.

Use:

ONE relationship configuration model
ONE canonical relationship model
ONE analyst review model

but TWO source/population strategies:

LENDING STRATEGY:
CAM + R2D2

CCR STRATEGY:
existing CCR CSV + R2D2


==================================================
CSV HANDLING RULE
==================================================

The CCR CSV already exists in the project folder.

Locate it programmatically.

Inspect it.

Reuse it.

Treat it as READ-ONLY input unless there is a genuine technical reason otherwise.

Do not ask me to upload it again.

Do not create a replacement CSV.

Do not transform the source file as part of this task.

If normalization is needed internally, create an in-memory/internal representation while preserving the original CSV unchanged.


==================================================
ACCEPTANCE TEST — BUSINESS LANE SEPARATION
==================================================

Test A — Lending

Select Lending.

Verify:

CAM is available.
R2D2 is available.

Run one relationship type.

Verify:

existing CAM relationship is CAM_CONFIRMED.

R2D2 corroboration attaches evidence rather than creating a duplicate relationship.


Test B — CCR

Select CCR.

Load entities from the existing CCR CSV in the project folder.

Verify:

CAM is NOT used.

Select a small sample of CCR entities.

Select one configured relationship type.

Use R2D2.

Return evidence-backed proposed relationships.

Verify:

Source = R2D2
Review State = EXTERNAL_PROPOSED


Test C — Same Configuration

Use the same configured relationship type, e.g.:

Critical Supplier

Run it once for Lending and once for CCR.

Verify:

Lending:
CAM + R2D2

CCR:
CSV population + R2D2

Same business definition.
Different evidence strategy.


==================================================
CORE PRODUCT PRINCIPLE
==================================================

The application supports two portfolio-analysis populations:

LENDING
Known internal CAM relationships can be analyzed, enriched and extended using R2D2.

CCR
The existing CSV defines the counterparty universe, and R2D2 is used to discover relationships because CAM is not currently available.

Configuration defines WHAT relationship the credit analyst wants to identify.

The business lane determines WHERE the evidence can come from.

Do not mix these concepts.
