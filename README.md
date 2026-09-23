LENDING — PLAN REBASELINE AND IMPLEMENTATION STATE RECONCILIATION

Work only in the CURRENT Lending repository.

THIS IS A READ-ONLY REBASELINE TASK.

Do not implement Prompt 4D.
Do not modify frontend behavior.
Do not modify backend behavior.
Do not modify data.
Do not modify databases.
Do not run migrations.
Do not call SEC, GLEIF, Web, Stylus, Helix, AI, or any external provider.
Do not modify CCR files.
Do not use Customer_latest.parquet or any CCR customer-master asset.
Do not attempt to "fix" inconsistencies during this task.

OBJECTIVE

The Lending implementation has progressed through several planned prompts,
but some additional work and cross-project prompts may have been executed
between planned stages.

Reconstruct the ACTUAL current Lending state from repository evidence and
re-establish the authoritative implementation plan before any further work.

The purpose is to answer:

1. What from Prompt 4A is actually implemented?
2. What from Prompt 4B is actually implemented?
3. What from Prompt 4C is actually implemented?
4. Has ANY Prompt 4D work actually begun?
5. What additional/unplanned work exists?
6. Did any CCR-specific concept or asset accidentally enter Lending?
7. What exists locally versus what is deployed?
8. What is the exact safe starting point for the next planned prompt?

==================================================
A. READ THE EXISTING LENDING REPORTS
==================================================

Locate and read all relevant Lending reports, including where present:

- LENDING_FOUNDATION_AUDIT.md
- LENDING_CANONICAL_RELATIONSHIP_CONTRACT_REPORT.md
- LENDING_PROMPT3_ACCEPTANCE_REPORT.md
- LENDING_PROMPT3C_REMEDIATION_REPORT.md
- LENDING_PROMPT4A_EXECUTIVE_HOME_REPORT.md
- LENDING_PROMPT4B_PORTFOLIO_CLIENT_REPORT.md
- LENDING_PROMPT4C_NETWORK_REPORT.md
- any Prompt 4C deployment report
- any Prompt 4D report
- any later Lending implementation report
- any deployment or SHA verification report

Do not assume the reports are mutually consistent.

Use repository/source state as final evidence where reports conflict.

==================================================
B. RECONSTRUCT THE PLANNED PRODUCT SEQUENCE
==================================================

The intended Lending product sequence is:

PROMPT 4A
Executive Home + common Lending shell

PROMPT 4B
Portfolio + Client Detail

PROMPT 4C
Network

PROMPT 4D
Relationship Explorer

PROMPT 4E
Governed Intelligence / AI relationship-definition experience

PROMPT 4F
External Research / supplemental evidence experience

PROMPT 4G
Review / analyst decision workflow

PROMPT 4H
Cross-route hardening, accessibility, performance,
regression validation, and release readiness

Confirm whether the repository still reflects this decomposition.

Do not redefine the plan.

==================================================
C. INVENTORY CURRENT ROUTES AND UI
==================================================

Inspect the active Lending frontend routes and determine the current
implementation status of:

/lending
/lending/clients
/lending/client/{cagid}
/lending/network
/lending/relationships
/lending/workbench
/lending/external-research
/lending/review

For each route classify:

NOT STARTED
LEGACY ONLY
PARTIALLY REFINED
PLANNED PROMPT COMPLETE
EXTRA / OUT-OF-SEQUENCE ENHANCEMENT

Also identify the shared Lending shell and navigation currently in use.

==================================================
D. INVENTORY BACKEND CONTRACTS
==================================================

Inspect all Lending backend APIs used by the above routes.

For each relevant endpoint identify:

- source lane;
- source population;
- authority;
- filtering;
- pagination;
- limit behavior;
- offset behavior;
- whether it reads bounded V3/CAM data;
- whether it reads normalized history;
- whether it reads external proposals;
- whether it reads AI instances;
- whether it can invoke a provider;
- whether it mutates anything.

Pay particular attention to the Prompt 4C Network changes.

Confirm whether the backend currently supports:

- bounded relationship pagination;
- offset;
- explicit supplemental/external inclusion;
- CAM/V3-first default loading;
- no automatic AI/provider/external execution.

==================================================
E. DETECT CROSS-PROJECT CONTAMINATION
==================================================

Search the CURRENT Lending implementation for accidental dependencies on:

- Customer_latest.parquet
- CCR customer master
- CCR population logic
- CCR exposure logic
- CCR relationship database
- CCR canonical entity model
- CCR-specific GFICD population rules
- CCR-specific migration scripts
- CCR-specific provider orchestration

Distinguish:

1. files merely coexisting in the monorepo;
2. references in documentation only;
3. actual Lending runtime dependency.

Only #3 is a Lending contamination problem.

Do not delete anything.

==================================================
F. IDENTIFY OUT-OF-SEQUENCE WORK
==================================================

Identify work performed outside the formal 4A–4H order.

Examples may include:

- map fly-lines;
- animation;
- visual indicators;
- deployment-only changes;
- extra CSS;
- experimental graph behavior;
- additional API optimizations;
- partial Relationship Explorer work.

Classify every such change as:

SAFE ENHANCEMENT
KEEP BUT ISOLATE

RELEVANT TO LATER PROMPT
KEEP AND CONSUME LATER

PLAN CONFLICT
MUST BE CORRECTED BEFORE CONTINUING

UNKNOWN
NEEDS INVESTIGATION

Do NOT revert safe enhancements simply because they were out of sequence.

==================================================
G. AUTHORITY MODEL CHECK
==================================================

Confirm the Lending authority rules remain:

CAM/V3
= authoritative Lending relationship truth.

V2
= conditional fallback/history only.

Normalized workbench
= separately governed projection.

External research
= supplemental evidence/proposals only.

Published AI instances
= separate governed analytical projection.

Portfolio and ordinary Network analytics
= read-only.

No universal relationship denominator is to be invented.

No cross-lane composite relationship score is to be invented.

No external or AI result may silently become CAM truth.

No UI-derived "credit meaning" may be represented as a persisted source fact.

==================================================
H. COUNT RECONCILIATION
==================================================

Collect the important current counts but DO NOT force them to match.

For each count record:

- population;
- source lane;
- endpoint;
- filter;
- route;
- meaning.

Include where available:

portfolio clients
reported OSUC
CAM-covered clients
V3 canonical relationships
V3 review-required relationships
bounded Network relationships
relationship groups
connected entities
external proposals
external conflicts
AI instances

If values such as:

41 total V3 rows
13 canonical
28 review-required
37 relationships

appear in different screens or reports, explain their scopes rather than
assuming one is wrong.

==================================================
I. LOCAL VERSUS DEPLOYED STATE
==================================================

Determine, from available repository/deployment evidence:

- which Prompt 4A files were deployed;
- which Prompt 4B files were deployed;
- which Prompt 4C frontend files were deployed;
- whether Prompt 4C backend files were deployed;
- whether local and remote versions are known to match.

If deployment truth cannot be established from repository evidence, state:

DEPLOYMENT STATE UNKNOWN

Do not infer successful deployment.

==================================================
J. PROMPT 4D READINESS
==================================================

Evaluate only whether the repository is ready to START Prompt 4D.

Do not implement it.

Prompt 4D should only begin if:

- 4A is stable;
- 4B is stable;
- 4C Network contract is stable;
- CAM/V3 authority remains intact;
- bounded relationship APIs are available;
- no accidental CCR runtime dependency exists;
- no partial incompatible 4D implementation needs reconciliation first.

If there is a blocker, identify the smallest remediation needed.

==================================================
K. CREATE THE REBASELINE REPORT
==================================================

Create:

backend/data/LENDING_IMPLEMENTATION_REBASELINE.md

Use these sections:

1. Executive conclusion
2. Current product architecture
3. Prompt 4A actual status
4. Prompt 4B actual status
5. Prompt 4C actual status
6. Prompt 4D actual status
7. Out-of-sequence enhancements
8. CCR contamination check
9. Authority-model verification
10. Current API/population matrix
11. Count reconciliation
12. Local versus deployed state
13. Technical debt carried forward
14. Exact next action

End with EXACTLY one of:

READY FOR PROMPT 4D

or

REMEDIATION REQUIRED BEFORE PROMPT 4D: <short reason>

Do not perform the remediation.
Do not start Prompt 4D.
