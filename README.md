Apply the engineering operating contract.

TASK: CUSTOMER MASTER + EXPOSURE POPULATION FOUNDATION

READ-ONLY ANALYSIS FIRST.

Primary sources:

backend/Customer_latest.parquet
backend/thousandClients.csv

Customer_latest.parquet is believed to contain approximately 3.6M master customer rows.
thousandClients.csv originated from an exposure population.

Do NOT assume those statements are perfectly correct. Validate them.

Do not modify the two files.

PURPOSE

Determine the correct distinction between:

MASTER CUSTOMER UNIVERSE
PORTFOLIO / EXPOSURE SUBJECT
CANONICAL ENTITY
RELATIONSHIP COUNTERPARTY

These must not be collapsed into one concept.

==================================================
1. PROFILE BOTH FILES
==================================================

Report:
- rows
- columns
- types
- null rates
- cardinality
- identifier candidates
- duplicate rates
- sample values
- status/date fields
- names
- countries
- industries
- organizational hierarchy fields
- customer lifecycle fields
- exposure fields

Use memory-efficient/chunked processing where appropriate.

==================================================
2. LINKAGE ANALYSIS
==================================================

Determine how thousandClients rows can map to Customer_latest.

Test in order:
- exact CAGID/customer identifier
- other governed IDs
- normalized legal name
- name + country
- other deterministic combinations

Do NOT use fuzzy matching as proof.

Report:
- exact matches
- one-to-many matches
- many-to-one matches
- unmatched exposure subjects
- duplicate master identifiers
- master records with conflicting attributes

==================================================
3. ACTIVE / INACTIVE
==================================================

Determine whether Customer_latest really contains active/inactive customers.

Identify the exact fields and value meanings.

Do not infer status only from filenames or missing exposure.

==================================================
4. HIERARCHY
==================================================

Identify any fields supporting:
- legal entity
- ultimate parent
- immediate parent
- branch
- subsidiary
- group
- booking entity
- relationship/customer level

Determine whether these are identities, attributes, or relationships.

==================================================
5. TARGET MODEL RECOMMENDATION
==================================================

Recommend conceptual roles for:
- master customer record
- canonical entity
- portfolio/exposure membership
- exposure measurement
- aliases
- identifiers
- historical customer state

Do not create tables yet.

==================================================
6. OUTPUT
==================================================

Create:

backend/data/LENDING_CUSTOMER_MASTER_RECONCILIATION.md

Include SQL/model implications for the next migration.

STOP.
