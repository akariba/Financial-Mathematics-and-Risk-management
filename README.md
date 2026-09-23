CCR FOUNDATION — PHASE-2 FINGERPRINT REGRESSION RECONCILIATION

Work only in the CURRENT CCR repository.

The Relationship Research Orchestrator was implemented successfully, but the
full backend suite currently reports:

41 passed
7 failed
8 errors

The reported cause is an existing Phase-2 exposure-record / foundation
metadata fingerprint mismatch.

DO NOT start live external relationship research yet.

No SEC calls.
No GLEIF calls.
No Web calls.
No Helix/AI calls.
No frontend work.
No production relationship creation.

IMPORTANT

Do NOT blindly rebaseline protected fingerprints.

Do NOT modify source data merely to make tests pass.

Do NOT overwrite Phase-2 protected business data.

OBJECTIVE

Determine exactly why the Phase-2 protected fingerprint tests now disagree
with the current database and repair only the metadata/test/migration issue
that is genuinely responsible.

==================================================
1. REPRODUCE FAILURES
==================================================

Run the full backend suite.

List every:

FAILED test
ERROR test

For each report:

test name
expected value
actual value
table/artifact involved
first failing assertion

Group failures by root cause.

==================================================
2. INSPECT PROTECTED PHASE-2 BASELINE
==================================================

Read the Phase-2 foundation report and tests.

Identify the protected fingerprint inputs.

Determine exactly what the fingerprint covers:

business rows
schema
metadata
table ordering
row ordering
generated timestamps
migration metadata
other

Do not assume.

==================================================
3. COMPARE CURRENT VS BASELINE
==================================================

For each protected table compare:

row count
business columns
business values
primary/business keys
ordering assumptions
metadata-only columns
migration-added columns

Determine whether:

A. protected business data changed

or

B. only additive schema/metadata changed

or

C. fingerprint logic incorrectly includes mutable/additive metadata

or

D. baseline itself is stale/inconsistent.

==================================================
4. EXPOSURE RECORDS
==================================================

Pay special attention to:

exposure_records

The canonical migration preserved all:

25,000 rows

Prove whether the actual business payload is unchanged.

Compare business fields row-for-row using stable keys/order.

Do not rely only on one aggregate hash.

==================================================
5. FOUNDATION METADATA
==================================================

Inspect Phase-2 metadata/fingerprint tables.

Determine whether later additive migrations changed fields such as:

schema version
migration version
generated_at
row metadata
semantic metadata
new nullable linkage fields

If such additive metadata is causing the mismatch, separate:

PROTECTED_PHASE2_BUSINESS_FINGERPRINT

from:

CURRENT_SCHEMA/MIGRATION_METADATA

Do not redefine the old Phase-2 business data.

==================================================
6. CANONICAL MIGRATION IMPACT
==================================================

Inspect:

migrate_ccr_canonical_data_model.py

and later relationship-policy/orchestrator migrations.

Confirm whether they altered any Phase-2 protected table values.

Expected:

business values unchanged.

If they added columns/links, determine whether those are legitimately outside
the original protected business fingerprint.

==================================================
7. FIX PRINCIPLE
==================================================

Preferred fix:

make fingerprint validation compare the immutable Phase-2 business payload,
not unrelated additive migration metadata.

Only if actual business data changed should the migration be corrected.

Do NOT simply replace the expected hash with the current hash.

Do NOT weaken tests.

==================================================
8. REGRESSION
==================================================

After the fix run:

Phase-2 tests
Phase-3 tests
canonical-model tests
relationship-universe tests
evidence/path tests
research-orchestrator tests
full backend suite

Expected:

0 failed
0 errors

==================================================
9. SAFETY VALIDATION
==================================================

Confirm:

CCR subjects = 16,769

Canonical entities = 16,767

Exposure rows = 25,000

Production relationships = 0

Production claims = 0

External entities = 0

Candidates promoted = 0

Source files unchanged

External calls = 0

SQLite integrity = PASS

Foreign keys = PASS

==================================================
10. REPORT
==================================================

Create:

backend/data/CCR_PHASE2_FINGERPRINT_RECONCILIATION_REPORT.md

Include:

failing tests
root cause
protected fingerprint definition
actual business-data comparison
metadata/schema difference
fix made
before/after hashes where relevant
full regression results

FINAL RESPONSE:

CCR PHASE-2 FINGERPRINT RECONCILIATION: PASS / FAIL

ROOT CAUSE:
<concise explanation>

PROTECTED BUSINESS DATA CHANGED:
YES / NO

EXPOSURE BUSINESS ROWS CHANGED:
YES / NO

FAILURES BEFORE:
7

ERRORS BEFORE:
8

FAILURES AFTER:
actual

ERRORS AFTER:
actual

PHASE-2:
PASS / FAIL

PHASE-3:
PASS / FAIL

CANONICAL MODEL:
PASS / FAIL

RELATIONSHIP UNIVERSE:
PASS / FAIL

EVIDENCE/PATH POLICY:
PASS / FAIL

RESEARCH ORCHESTRATOR:
PASS / FAIL

FULL BACKEND:
passed:
failed:
errors:

SOURCE FILES MODIFIED:
0 / FAIL

PRODUCTION RELATIONSHIPS:
0 / FAIL

EXTERNAL CALLS:
0 / FAIL

REPORT:
backend/data/CCR_PHASE2_FINGERPRINT_RECONCILIATION_REPORT.md

STOP.
