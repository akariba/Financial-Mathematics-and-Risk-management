Name
Lending Relationship Research - Web + SEC

Description
Research credit-relevant relationships between Lending clients and related entities using approved R2D2 Web and SEC evidence. Return structured, source-grounded findings for corroboration, new relationship proposals, conflicts, confidence, materiality, and mention-only exclusion. CAM remains authoritative.

Shortcut Key
lending-relationship-research

Then click Next.

For the knowledge package, I would create these files:

00_PRESET_READINESS.md
Contains the exact marker:
relationship_research_ready: true
01_LENDING_RELATIONSHIP_RESEARCH_POLICY.md
CAM authority, external evidence rules, no overwrite, corroboration vs proposal.
02_RELATIONSHIP_TAXONOMY.md
Supplier, Critical Supplier, Customer, Sponsor, Guarantor, Parent, Subsidiary, Investor, Lender, Technology Dependency, Infrastructure Dependency, Revenue Concentration, Strategic Partner, etc.
03_SOURCE_AND_EVIDENCE_RULES.md
SEC vs R2D2 Web, credible-source hierarchy, exact excerpts, dates, contradiction handling.
04_CONFIDENCE_AND_CROSSCHECK_RULES.md
High/Medium/Low based on source authority, explicitness, corroboration, entity certainty, recency and conflicts.
05_CREDIT_MATERIALITY_RULES.md
MATERIAL / POTENTIALLY_MATERIAL / CONTEXTUAL / UNKNOWN, kept separate from evidence confidence.
06_ENTITY_RESOLUTION_RULES.md
Legal names, aliases, CAGID, CIK/LEI if present, ambiguity handling.
07_OUTPUT_SCHEMA.md
Exact structured output the app expects.
08_RESEARCH_EXAMPLES.md
Good examples for CAM corroboration, new proposal, conflict, mention-only, current/historical/emerging, direct/indirect.
09_EXCLUSIONS_AND_GUARDRAILS.md
No co-mention = relationship, no fabricated sources, no unsupported confidence, no automatic CAM mutation.
Give Luna this prompt now
Create the complete knowledge package required for the manually configured Stylus preset:

"Lending Relationship Research - Web + SEC"

IMPORTANT BOUNDARY:
You are NOT configuring or creating the Stylus preset.
You are ONLY creating the knowledge files that I will manually upload into Stylus Preset Builder.

Use the existing Lending relationship solution, R2D2 integration code, current relationship taxonomy, external research models, confidence logic, review workflow, and RPR Runner integration as the source of truth.

Do not invent runtime input names or output fields if they already exist in the code.

FIRST inspect:
- current Lending R2D2 Assist implementation
- external research persistence models
- relationship taxonomy
- confidence-factor model
- proposal/review model
- Runner response parser
- any preset validation logic in stylus_preset.py
- the exact structured result schema expected by the Lending backend

Then create the following Markdown knowledge files in a dedicated folder such as:

preset_knowledge/lending_relationship_research/

==================================================
FILE 1
00_PRESET_READINESS.md
==================================================

This file must contain:

relationship_research_ready: true

Also state:

Preset purpose:
Lending relationship research using approved R2D2 Web and SEC evidence.

Authority rule:
CAM/internal approved Lending evidence remains authoritative.
External evidence can corroborate, supplement, conflict, or create reviewable proposals.
External evidence must never silently overwrite CAM.

Do not add pending/TODO language to this file.

==================================================
FILE 2
01_LENDING_RELATIONSHIP_RESEARCH_POLICY.md
==================================================

Document the governing research rules.

Include:

1. CAM is authoritative
2. External evidence is supplementary
3. Existing CAM relationship + external support = CORROBORATES_CAM
4. Relationship absent from CAM + defensible external evidence = NEW_TO_BASELINE / proposal
5. External evidence contradicts CAM = CONFLICTS_WITH_CAM
6. Co-mention without a defensible economic/credit relationship = MENTION_ONLY / INSUFFICIENT_EVIDENCE
7. No automatic CAM overwrite
8. No automatic promotion of proposals to validated internal relationships
9. Exact evidence and source provenance are mandatory
10. Findings must remain auditable

Clearly distinguish:

relationship truth
evidence
confidence
credit materiality
review state

==================================================
FILE 3
02_RELATIONSHIP_TAXONOMY.md
==================================================

Use the EXISTING controlled Lending relationship taxonomy from the current application.

Do not invent a new incompatible taxonomy.

Explain each supported relationship type, including the exact business meaning and inclusion/exclusion criteria.

Cover the current relevant families such as:

COMMERCIAL
- Contracted Customer
- Customer
- Supplier
- Critical Supplier
- Service Provider
- Strategic Partner

OWNERSHIP / CAPITAL
- Parent Company
- Subsidiary
- Sponsor
- Equity Investor
- Joint Venture
- Common Owner where currently supported

CREDIT SUPPORT / FINANCING
- Guarantor
- Backleverage Financing
- Lender
- Collateral Provider
- Agent Bank where supported

DEPENDENCY / CONCENTRATION
- Customer Dependency
- Revenue Concentration
- Technology Dependency
- Infrastructure Dependency
- Supplier Dependency where supported

MARKET / LEGAL / OTHER
- Competitor
- M&A Target
- Legal Counterparty
- Regulator
- Advisor

For each type include:

definition
what qualifies
what does NOT qualify
directionality
common evidence phrases
credit relevance

==================================================
FILE 4
03_SOURCE_AND_EVIDENCE_RULES.md
==================================================

Define source hierarchy and evidence requirements.

Use:

1. Internal CAM / approved Lending evidence — authoritative baseline
2. SEC filing / regulatory filing evidence
3. Official corporate sources
4. High-quality reputable news / public sources
5. Other credible secondary sources
6. Weak commentary / blogs / forums — contextual only unless independently corroborated

For every external finding require:

source channel
source name
source date
source reference
exact supporting excerpt
entity names
relationship classification
why the excerpt supports the classification

Define SEC and Web as separate evidence channels even if they use the same R2D2 Runner framework.

Do not classify a source as SEC merely because a web article mentions an SEC filing.

==================================================
FILE 5
04_CONFIDENCE_AND_CROSSCHECK_RULES.md
==================================================

Create explainable confidence rules.

Confidence must NOT be an arbitrary LLM opinion.

Use factors including:

SOURCE AUTHORITY
EVIDENCE EXPLICITNESS
INDEPENDENT CORROBORATION
ENTITY MATCH CERTAINTY
RECENCY
CONTRADICTORY EVIDENCE

Define:

HIGH
MEDIUM
LOW
INSUFFICIENT

Examples:

HIGH:
- explicit relationship statement
- strong/authoritative source
- clear entity identity
- current evidence
- ideally independently corroborated

MEDIUM:
- credible source and reasonable evidence
- but limited corroboration or some interpretation required

LOW:
- weak/indirect evidence
- ambiguous wording
- uncertain entity resolution

INSUFFICIENT:
- co-mention only
- speculation
- no defensible relationship evidence

Also explain how cross-checking changes confidence.

==================================================
FILE 6
05_CREDIT_MATERIALITY_RULES.md
==================================================

Keep materiality separate from evidence confidence.

Use:

MATERIAL
POTENTIALLY_MATERIAL
CONTEXTUAL
UNKNOWN

Explain factors such as:

- revenue/customer concentration
- critical supplier dependency
- financing/support dependency
- ownership/control
- limited substitutability
- strategic infrastructure dependence
- magnitude/amount/percentage when disclosed
- potential effect on repayment capacity or credit profile

Do NOT create a numerical credit/risk score.

Every materiality classification must include a concise explanation.

==================================================
FILE 7
06_ENTITY_RESOLUTION_RULES.md
==================================================

Document entity matching rules aligned to the current application.

Use identifiers in this order when available:

- internal identifiers / CAGID
- legal entity names
- CIK / LEI or other formal identifiers
- known aliases
- company domains
- normalized names

Do not merge entities purely because names are similar.

Explicitly address:

parent vs subsidiary
SPV vs operating company
fund vs manager
facility vehicle vs borrower
brand vs legal entity

Ambiguous matches must return:

ENTITY_MATCH_REVIEW_REQUIRED

==================================================
FILE 8
07_OUTPUT_SCHEMA.md
==================================================

THIS IS CRITICAL.

Inspect the existing Lending backend / R2D2 response parser and document the EXACT structured output schema expected by the application.

Do not invent field names when code already defines them.

The output should cover, where expected by current code:

entity_a
entity_b
relationship_type
relationship_family
direction
state
connectivity
source_channel
source_name
source_date
source_reference
exact_excerpt
evidence_confidence
confidence_factors
credit_materiality
materiality_rationale
discovery_status
matching_cam_relationship
contradictory_evidence
entity_match_status
review_state

Use exact enum/value names from the implementation.

Document allowed values.

The preset should be instructed to return ONLY the required structured artifact plus concise evidence-grounded fields — no long free-form essay.

==================================================
FILE 9
08_RESEARCH_EXAMPLES.md
==================================================

Create realistic but clearly illustrative examples showing how the model should classify:

A. Existing CAM relationship corroborated by Web
B. Existing CAM relationship corroborated by SEC
C. New external relationship not present in CAM
D. External evidence conflicting with CAM
E. Mention-only / no relationship
F. Direct relationship
G. Indirect relationship
H. Current relationship
I. Historical relationship
J. Emerging relationship
K. High confidence but contextual materiality
L. Medium confidence but potentially material relationship

Do not present fabricated examples as actual Citi/CAM evidence.
Label them as examples.

==================================================
FILE 10
09_EXCLUSIONS_AND_GUARDRAILS.md
==================================================

Explicitly prohibit:

- inventing sources
- inventing excerpts
- inventing relationship amounts
- treating co-mention as relationship
- using pre-trained model knowledge as evidence
- silently resolving ambiguous entities
- silently overwriting CAM
- automatically validating external proposals
- using unsupported SEC claims
- conflating confidence with materiality
- conflating direct/indirect with cross-document discovery
- calling a relationship historical without temporal evidence
- calling something NEW merely because a new article exists

When evidence is insufficient, return:

INSUFFICIENT_EVIDENCE

rather than forcing a relationship.

==================================================
PRESET PROMPT RECOMMENDATION
==================================================

Also create:

10_PRESET_SYSTEM_INSTRUCTION.md

This should contain a concise production-ready instruction suitable for pasting into the Stylus preset prompt field.

It must instruct the preset to:

- research only the requested subject/entity pair/context
- use approved R2D2 Web and SEC tools
- retrieve source-grounded evidence
- cross-check when possible
- classify relationships using the controlled taxonomy
- separate confidence from materiality
- return structured output matching the application schema
- identify contradictions
- reject mention-only findings
- avoid unsupported conclusions
- preserve CAM authority
- never overwrite internal truth

Keep the prompt complete but concise enough for a production preset.

==================================================
RUNTIME INPUTS
==================================================

DO NOT invent the six runtime input keys.

Inspect the current Lending Runner adapter and stylus_preset validation code.

Create:

11_RUNTIME_INPUTS.md

List the EXACT runtime input keys expected by the current implementation.

For every input give:

- exact key
- purpose
- required/optional
- example value
- whether it is supplied by the application or manually

If the current code expects six inputs, document exactly those six.

==================================================
TOOLS / INTEGRATIONS
==================================================

Create:

12_REQUIRED_TOOLS_AND_INTEGRATIONS.md

Document exactly which Stylus tools/integrations the preset must enable based on the currently proven RPR configuration.

Clearly separate:

REQUIRED
OPTIONAL
NOT SUPPORTED

For example:
- Web search / R2D2
- SEC filing integration if genuinely supported by the existing RPR setup

Do not claim a tool exists unless it is present in the current proven configuration.

==================================================
VALIDATION
==================================================

Before finishing:

1. Verify all knowledge files exist.
2. Verify no TODO / pending placeholders remain.
3. Verify `relationship_research_ready: true` exists exactly.
4. Verify output schema matches current code.
5. Verify runtime input keys match current code exactly.
6. Verify no incompatible taxonomy was invented.
7. Verify CAM authority is explicit throughout.
8. Verify no knowledge file instructs the model to fabricate missing evidence.

Do NOT modify application code unless required only to inspect/document the existing schema.

Do NOT configure Stylus.
Do NOT run the preset.
Do NOT upload files.
Do NOT modify RPR.

When complete, report only:

- knowledge folder path
- files created
- exact six runtime input keys
- required Stylus tools/integrations
- recommended model if already established by the existing proven RPR setup
- readiness validation PASS / FAIL

Then STOP.
