CCR RELATIONSHIP INTELLIGENCE — LIVE HIGH-QUALITY RELATIONSHIP PILOT

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_CANONICAL_DATA_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_UNIVERSE_MODEL_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md
backend/data/CCR_PHASE2_FINGERPRINT_RECONCILIATION_REPORT.md

Inspect the current provider connectivity and research orchestration code.

This is the FIRST live external relationship pilot.

Do NOT run across the full CCR population.

Do NOT perform broad crawling.

Do NOT create CONFIRMED relationships automatically.

Do NOT use AI-generated text as evidence.

Do NOT lower evidence standards because a provider fails.

==================================================
1. OBJECTIVE
==================================================

Select 5 real CCR entities with strong identity quality and run bounded
relationship discovery using the existing orchestrator.

The pilot must test:

GLEIF
SEC
authoritative company Web
high-quality secondary Web where configured/allowed

The objective is to discover a small number of HIGH-QUALITY relationship
proposals with real evidence.

Possible relationship types:

PARENT
ULTIMATE_PARENT
SUBSIDIARY
SUPPLIER
CRITICAL_SUPPLIER
CUSTOMER
KEY_CUSTOMER
TECHNOLOGY_PROVIDER
TECHNOLOGY_DEPENDENCY
INVESTOR
SPONSOR
LENDER
FINANCING_RELATIONSHIP
STRATEGIC_PARTNER
JOINT_VENTURE

Do not attempt every relationship type for every entity.

Choose plausible analysis types based on entity profile and source readiness.

==================================================
2. SELECT PILOT ENTITIES
==================================================

Choose 5 CCR entities dynamically from the canonical database.

Selection preference:

HIGH identity quality

research_allowed = true

master-backed

LEI available where possible

public-company / SEC-researchable identity where possible

non-masked identity

Avoid:

REVIEW_REQUIRED

masked/private-bank CCR-only identities

weak identity

Do not hardcode famous companies merely for convenience.

For each selected entity report:

entity_key
legal_name
country
sector/industry
LEI
CIK if already known
identity quality
research readiness
reason selected

==================================================
3. RESEARCH PLAN PER ENTITY
==================================================

Create a bounded plan per entity.

Examples:

If LEI exists:
test parent / ultimate-parent through GLEIF.

If SEC-researchable:
test one or more of:
supplier
customer
technology dependency
subsidiary
financing
strategic partner

Use the relationship-specific source strategy registry.

Do not exceed:

3 relationship-analysis questions per entity

Total pilot:
maximum 15 bounded research questions.

==================================================
4. PROVIDER ORDER
==================================================

Use the configured strategy.

Examples:

PARENT / ULTIMATE_PARENT:
GLEIF
→ SEC
→ authoritative Web

SUPPLIER / CUSTOMER:
SEC
→ official company disclosure
→ high-quality Web

TECHNOLOGY DEPENDENCY:
SEC
→ official company disclosure
→ high-quality Web

LENDER / FINANCING:
SEC
→ official company disclosure
→ high-quality Web

Do not use one generic provider order.

==================================================
5. SOURCE QUALITY
==================================================

Admit only:

TIER_1_AUTHORITATIVE_EXTERNAL

or where policy permits:

TIER_2_HIGH_QUALITY_SECONDARY

Tier-2 evidence alone must obey existing corroboration rules.

Reject:

search snippets
aggregators
SEO pages
anonymous sources
AI-generated pages
unverified scraped copies

==================================================
6. IDENTITY RESOLUTION
==================================================

If research discovers a related entity not already in entity_registry:

resolve identity before creating EXTERNAL_ENTITY.

Prefer:

LEI
CIK
official legal name
official domain
regulatory identity

Do NOT create external entities from:

name similarity alone
search snippets
AI guesses
local correlation score

==================================================
7. CLAIM EXTRACTION
==================================================

For each candidate relationship store:

subject
related entity
relationship type
direction

source document
evidence snippet
source tier

current/historical/unknown
evidence strength
identity quality
source quality
freshness
consistency

Do not store one opaque confidence score.

==================================================
8. PROPOSAL RULE
==================================================

A relationship may become:

PROPOSAL_PENDING_REVIEW

only if the existing evidence threshold is met.

Otherwise:

INSUFFICIENT_EVIDENCE
NOT_FOUND
CONFLICT
PROVIDER_UNAVAILABLE
IDENTITY_UNRESOLVED

Do not create CONFIRMED relationships.

==================================================
9. DIRECT VS INDIRECT
==================================================

For this pilot:

discover DIRECT evidence-backed claims first.

If multiple direct relationships create an indirect path:

record/display the path separately.

Do NOT create a synthetic direct edge from an indirect path.

==================================================
10. HIDDEN RELATIONSHIPS
==================================================

If an externally evidenced direct relationship was not already known internally:

classify it as:

HIDDEN_DIRECT

This means:

externally discovered direct relationship

not:

AI-inferred relationship.

If an indirect path emerges from multiple valid edges:

classify path as:

HIDDEN_INDIRECT

without creating a direct relationship.

==================================================
11. HELIX / AI
==================================================

If Helix is available, it may assist with:

document classification
claim extraction
relationship-type classification
direction extraction
evidence summarization
contradiction detection

AI must NOT:

act as evidence
invent evidence
create CONFIRMED status
create an entity without identity evidence
fill missing relationship hops

If AI is unavailable:

continue with deterministic/provider extraction where possible.

==================================================
12. BOUNDED NETWORK LIMIT
==================================================

This is a pilot.

Maximum:

5 subject entities
15 research questions
50 retrieved source documents total
30 discovered claims total
20 external entities created maximum

If limits are reached:

stop gracefully and report BOUNDED_LIMIT_REACHED.

==================================================
13. PRODUCTION WRITES
==================================================

Allowed production writes:

research_runs
research plans
source documents
evidence snippets
discovered claims
defensible external entities
PROPOSAL_PENDING_REVIEW relationship observations
paths composed only of valid stored edges

Not allowed:

CONFIRMED relationships
synthetic relationships
candidate promotion from local correlation alone

==================================================
14. VALIDATION
==================================================

After pilot report:

subjects researched

research questions

provider attempts by provider

documents retrieved

Tier-1 documents

Tier-2 documents

inadmissible documents rejected

claims discovered

proposals created

insufficient-evidence outcomes

conflicts

provider unavailable

external entities created

direct relationships proposed

hidden-direct relationships

indirect paths

hidden-indirect paths

CONFIRMED relationships created = 0

AI evidence rows = 0

synthetic edges = 0

==================================================
15. QUALITY REVIEW
==================================================

For every proposal verify manually in code/data:

the evidence snippet actually supports the relationship

the source identity matches the entity

direction is correct

relationship type is not overstated

CRITICAL_SUPPLIER / KEY_CUSTOMER / TECHNOLOGY_DEPENDENCY
is not assigned without explicit dependency/materiality evidence

If questionable:

downgrade to INSUFFICIENT_EVIDENCE.

Prefer false negatives over low-quality false positives.

==================================================
16. REPORT
==================================================

Create:

backend/data/CCR_LIVE_RELATIONSHIP_PILOT_REPORT.md

Include one section per pilot entity:

identity
research questions
provider waterfall
documents
claims
proposals
rejected claims
research gaps

Include a final quality summary.

==================================================
17. FINAL RESPONSE
==================================================

Return:

CCR LIVE RELATIONSHIP PILOT: PASS / FAIL

SUBJECTS RESEARCHED:
actual

RESEARCH QUESTIONS:
actual

PROVIDER ATTEMPTS
GLEIF:
SEC:
AUTHORITATIVE WEB:
HIGH-QUALITY WEB:

DOCUMENTS
Total:
Tier-1:
Tier-2:
Rejected/inadmissible:

CLAIMS
Discovered:
Accepted:
Rejected:

RELATIONSHIP PROPOSALS:
actual

HIDDEN DIRECT:
actual

INDIRECT PATHS:
actual

HIDDEN INDIRECT:
actual

EXTERNAL ENTITIES CREATED:
actual

OUTCOMES
Proposal pending review:
Insufficient evidence:
Conflict:
Not found:
Provider unavailable:
Identity unresolved:

QUALITY
Wrong-entity matches:
0 / FAIL

Unsupported relationship types:
0 / FAIL

Critical/key relationships without materiality evidence:
0 / FAIL

AI AS EVIDENCE:
0 / FAIL

CONFIRMED RELATIONSHIPS CREATED:
0 / FAIL

SYNTHETIC EDGES:
0 / FAIL

REPORT:
backend/data/CCR_LIVE_RELATIONSHIP_PILOT_REPORT.md

STOP.
