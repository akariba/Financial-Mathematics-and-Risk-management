You are continuing the Lending Credit Relationship Workbench.

This phase introduces R2D2 external research/enrichment.

This is LENDING ONLY.

Do NOT modify the trusted internal CAM pipeline unless absolutely required for integration.
Do NOT rebuild the frozen internal baseline.
Do NOT redesign the application.
Do NOT introduce another business lane.
Do NOT use direct public internet calls as a substitute for R2D2.

The current Lending foundation already exists:

- target population control
- CAM availability/freshness
- persistent SQLite database
- document/version ingestion
- section extraction
- exact evidence storage
- validated relationship baseline
- review-required workflow
- Lending relationship explorer/map

Treat that foundation as frozen.

==================================================
MOST IMPORTANT INSTRUCTION — REUSE RPR R2D2
==================================================

DO NOT INVENT A NEW R2D2 INTEGRATION.

There is already a known-working R2D2 integration pattern in the RPR project.

FIRST locate and inspect the current RPR implementation.

Reuse the proven RPR approach for:

- authentication
- OAuth / token handling
- token refresh
- environment configuration
- Runner Service configuration
- request construction
- streaming/SSE handling
- error handling
- timeout / bounded completion handling
- response parsing
- preset payload construction
- runtime input mapping

The known RPR pattern uses the Runner Service and sends the FULL PRESET DEFINITION INLINE.

Do NOT assume or invent a preset UUID API.

The proven conceptual flow is:

OAuth / refresh token
    ↓
Runner Service
    ↓
POST /runner-service/chat
    ↓
full preset definition inline
    ↓
runtime inputs
    ↓
streamed response
    ↓
structured result parsing

Inspect the actual CURRENT RPR code and reuse the exact working implementation rather than relying only on this description.

Do NOT change the RPR project itself.

==================================================
IMPORTANT PRESET BOUNDARY
==================================================

The coding agent does NOT create or manually configure Stylus presets.

Presets are created/configured/tested manually in Stylus Workspaces.

The application code only:

- reuses the proven preset definition/configuration already established
- sends the captured equivalent full preset definition inline
- injects runtime company/entity/search inputs
- invokes the Runner
- parses the returned result

If a genuinely new manual Stylus preset is required and no existing RPR preset can satisfy the task, report that as a genuine external blocker.

Do NOT fabricate a preset.
Do NOT guess a preset ID.
Do NOT create fake preset configuration.

Prefer reuse of the existing proven RPR WEB / SEC+WEB capability where appropriate.

==================================================
R2D2 ROLE IN THIS LENDING PRODUCT
==================================================

CAM remains the authoritative internal baseline.

R2D2 must NEVER silently overwrite CAM.

R2D2 has TWO purposes:

1. CORROBORATION
Find external evidence supporting an existing CAM relationship.

2. DISCOVERY
Find a potentially credit-relevant relationship not present in the available CAM baseline.

These outcomes must remain separate.

Example:

CAM:
Company A -> Company B
Relationship = Supplier

R2D2 finds credible external evidence confirming it.

Result:

same canonical CAM relationship
+
external corroborating evidence

DO NOT create a duplicate economic relationship.


Another example:

CAM has no Company A -> Company C relationship.

R2D2 finds strong external evidence of:
Company A -> Company C
Relationship = Critical Supplier

Result:

EXTERNAL_PROPOSED

It must NOT automatically become CAM-confirmed or trusted canonical truth.


==================================================
R2D2 SOURCE MODES
==================================================

Use the RPR-proven R2D2 configuration to expose external research in clearly separated evidence channels.

Where supported by the actual proven RPR configuration:

A. R2D2 WEB
Broad credible public research.

B. SEC FILINGS
Regulatory filing evidence.

Even if both technically run through the same R2D2/Runner framework, preserve the distinction in our data model and UI.

Example:

source_channel = R2D2_WEB

or:

source_channel = SEC_FILING


If an SEC document is discovered through a broad web search but the actual filing content is subsequently retrieved and verified, classify the evidence as SEC filing evidence.

Do not claim SEC support merely because a web page mentions an SEC filing.

==================================================
SOURCE PRIORITY
==================================================

For Lending use this conceptual hierarchy:

1. CAM / internal approved credit evidence
2. SEC filing evidence
3. credible R2D2 Web evidence

CAM remains authoritative.

External evidence may:

- corroborate
- supplement
- add freshness/context
- propose a new relationship
- flag a conflict

External evidence may NOT automatically overwrite CAM.


==================================================
R2D2 ASSIST
==================================================

Add an R2D2 Assist capability to the existing relationship/correlation configuration experience.

Keep it visually separate from the saved business configuration.

The assistant should support two modes:

-----------------------------------------------
MODE 1 — RESEARCH RELATIONSHIP
-----------------------------------------------

User can type:

"Find the relationship between NVIDIA and Anthropic"

or any two entities.

R2D2 should research the selected source channels and return STRUCTURED candidate findings.

Return fields such as:

Entity A
Entity B
Relationship Type
Relationship Family
Direction
Current / Historical / Emerging
Direct / Indirect
Evidence Confidence
Potential Credit Materiality
Source Channel
Source Name
Source Date
Exact Evidence Excerpt
Source Reference
Why the evidence supports the classification
Contradictory Evidence
Known in CAM? yes/no
Discovery Status

Discovery Status values:

CAM_KNOWN
CORROBORATES_CAM
NEW_TO_BASELINE
CONFLICTS_WITH_CAM
INSUFFICIENT_EVIDENCE


Do NOT treat co-mention as a relationship.

If two entities are merely mentioned in the same article:

return:

MENTION_ONLY / INSUFFICIENT_EVIDENCE

and do NOT add a relationship proposal.


-----------------------------------------------
MODE 2 — ASSIST CONFIGURATION
-----------------------------------------------

When the analyst is configuring a relationship type such as:

Critical Supplier

allow R2D2 Assist to suggest:

- objective
- inclusion criteria
- exclusion criteria
- evidence characteristics
- useful terminology
- examples from credible evidence

BUT:

R2D2 must never silently modify the saved business definition.

Provide an explicit:

Apply suggestion

action.

The business user remains authoritative over the configuration.


==================================================
TEST CONFIGURATION
==================================================

Inside the configuration workflow add:

TEST CONFIGURATION

The analyst should be able to test one configured relationship definition against:

- one entity pair
or
- a small selected Lending sample

Example:

Relationship:
Critical Supplier

Test:
CoreWeave / NVIDIA

Return:

MATCH / NO MATCH / INSUFFICIENT

with:

rules matched
rules not matched
evidence
source
confidence
reasoning summary

This is especially important for transparency.

Do not execute large portfolio searches from this configuration test.


==================================================
PORTFOLIO ENRICHMENT
==================================================

Add a bounded R2D2 enrichment workflow using the existing Lending population.

Allow:

- one client
- selected clients
- small controlled batch

Do NOT immediately run R2D2 against all 418 names.

This phase is about proving the integration and governance first.

For each selected Lending client:

1. load canonical entity identity
2. use configured relationship definitions
3. query R2D2
4. parse structured evidence
5. reconcile entity names
6. compare against existing CAM relationships
7. classify as corroboration / proposal / conflict
8. persist external evidence
9. send new candidate relationships to review

==================================================
EXTERNAL DATA MODEL
==================================================

Do NOT insert R2D2 output directly into the internal CAM baseline tables as if it were internal truth.

Use separate persistent structures such as:

EXTERNAL_RESEARCH_RUNS
EXTERNAL_EVIDENCE
RELATIONSHIP_PROPOSALS

or equivalent existing models if already available.

A proposal should support:

proposal_id
entity_a
entity_b
proposed_relationship_type
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
credit_materiality
discovery_status
matching_cam_relationship_id
review_state
created_at

Possible review states:

PENDING_REVIEW
ANALYST_CONFIRMED
ANALYST_MODIFIED
ANALYST_REJECTED

Do not automatically convert external proposals into validated CAM relationships.


==================================================
TRANSPARENCY / CONFIDENCE
==================================================

Leslie's core concern is:

"How accurate is the data?"

Therefore confidence must be explainable.

Do NOT let the LLM produce unexplained:

HIGH
MEDIUM
LOW

Store the factors behind confidence.

At minimum evaluate:

SOURCE AUTHORITY
- regulatory / official company evidence
- high-quality reputable source
- secondary source
- weak commentary

EVIDENCE EXPLICITNESS
- relationship explicitly stated
- strongly implied
- circumstantial only

CORROBORATION
- multiple independent sources
- single source

ENTITY MATCH
- exact legal identity
- strong alias match
- ambiguous identity

RECENCY
- current
- stale
- historical

CONTRADICTION
- conflicting evidence exists / does not exist


The UI should be able to say:

Evidence Confidence: HIGH

Why:
- explicit relationship statement
- official source
- independently corroborated
- entity match confirmed
- current evidence

Do not expose hidden chain-of-thought.
Expose concise evidence-based rationale only.


==================================================
CROSS-CHECKING
==================================================

Implement a transparent cross-check mechanism.

For an external candidate:

Source 1 says:
A -> B Supplier

Source 2 says:
A -> B Supplier

This strengthens corroboration.

But:

one blog / weak commentary only

should remain lower confidence.

If sources conflict:

do NOT choose silently.

Mark:

CONFLICT_REVIEW_REQUIRED

and present both pieces of evidence.


==================================================
CREDIT MATERIALITY
==================================================

Keep evidence confidence separate from credit materiality.

These are different concepts.

Example:

HIGH evidence confidence
LOW credit materiality

is possible.

Example:

MEDIUM evidence confidence
POTENTIALLY MATERIAL

is also possible.

Use categories such as:

MATERIAL
POTENTIALLY_MATERIAL
CONTEXTUAL
UNKNOWN

Materiality must have a short explanation.

Do NOT create a numerical risk score.


==================================================
MENTION / ASSOCIATION HANDLING
==================================================

Explicitly distinguish:

RELATIONSHIP

from:

MENTION / ASSOCIATION

If NVIDIA and another company appear in one news article with no defensible economic relationship:

store it only as research context if useful.

Do not create a relationship edge.

This is essential to reduce false positives.


==================================================
CURRENT / HISTORICAL / EMERGING
==================================================

External evidence may indicate:

CURRENT
HISTORICAL
EMERGING
TERMINATED
UNKNOWN

These labels require evidence.

"HISTORICAL" requires actual temporal evidence.

"EMERGING" should mean a newly forming or recently announced relationship.

"NEW_TO_BASELINE" means:

not currently present in the internal CAM baseline

It does NOT necessarily mean the relationship itself is newly created in the real world.


==================================================
ENTITY RESOLUTION
==================================================

Reuse existing Lending entity reconciliation.

For R2D2 results consider:

internal CAGID if mapped
legal name
known aliases
domains
CIK/LEI or other identifiers where available

Do NOT merge entities purely because names look similar.

Ambiguous matches:

ENTITY_MATCH_REVIEW_REQUIRED


==================================================
DO NOT TOUCH INTERNAL BASELINE
==================================================

Hard rule:

LENDING_INTERNAL_BASELINE_V1 remains frozen.

The 767 validated internal relationships remain unchanged by this phase.

R2D2 enrichment lives on top.

Do not mutate CAM relationships.

Do not reinterpret existing CAM classifications merely because external sources use different wording.


==================================================
NO DIRECT PUBLIC WEB CLIENT
==================================================

Do not create:

requests.get("google...")
BeautifulSoup public scraping
random public search APIs
new external web libraries

All approved external research in this phase must go through the existing RPR-proven R2D2 mechanism.

==================================================
RUNNER RELIABILITY
==================================================

Inspect the latest working RPR implementation and reuse its final Runner behavior.

Do not reintroduce historical RPR issues such as:

- indefinite SSE waiting
- hanging when no model-final event arrives
- expired-token loops
- uncontrolled automatic retriggering

Reuse the current proven bounded completion / refresh behavior if present in RPR.

One explicit user action must produce one R2D2 execution.

No automatic reruns on page load/reconnect.


==================================================
ERROR HANDLING
==================================================

R2D2 failure must not break the Lending application.

Possible outcomes:

SUCCESS
NO_EVIDENCE
AUTH_FAILURE
TIMEOUT
RUNNER_ERROR
ENTITY_AMBIGUOUS

Store research-run status.

Show a concise analyst-facing message.

Do not retry endlessly.

Use the proven RPR retry/auth behavior only.


==================================================
NO LOOPS
==================================================

This is critical.

Do not:

- repeatedly rerun successful R2D2 calls
- rebuild the internal database
- revalidate the 767 baseline
- refactor working code after acceptance
- produce multiple diagnostic reports
- keep tuning prompts after tests pass

If something fails:

identify the specific cause
fix it
rerun only the affected acceptance test

When all acceptance tests pass:

STOP.


==================================================
ACCEPTANCE TESTS
==================================================

TEST 1 — RPR PATTERN REUSE

Identify and document the exact RPR files/functions reused for:

authentication
token refresh
Runner invocation
inline preset payload
stream parsing

Verify no guessed preset-ID mechanism was introduced.

PASS / FAIL


TEST 2 — AUTHENTICATION

Perform one controlled R2D2 call through the reused RPR mechanism.

Verify auth/token refresh succeeds.

PASS / FAIL


TEST 3 — WEB RESEARCH

Research one real entity pair using R2D2 Web.

Return structured evidence with:

source
date
excerpt
relationship classification
confidence factors

PASS / FAIL


TEST 4 — SEC MODE

If SEC capability exists in the proven RPR preset/configuration:

research one entity through SEC evidence.

Verify SEC evidence remains separately labelled.

If the existing RPR capability does not expose SEC:

report that honestly as an external/configuration blocker.

Do not invent it.

PASS / BLOCKED


TEST 5 — CAM CORROBORATION

Choose one existing validated CAM relationship.

Run R2D2.

If corroborating evidence is found:

attach it as external evidence to the existing relationship.

Verify no duplicate canonical relationship is created.

PASS / FAIL


TEST 6 — NEW RELATIONSHIP PROPOSAL

Use R2D2 on a controlled case where a relationship not in CAM is supported by external evidence.

Verify:

proposal created
source retained
evidence retained
review state = PENDING_REVIEW

Verify:

internal CAM baseline unchanged.

PASS / FAIL


TEST 7 — MENTION ONLY

Test a case where sources merely mention both entities without proving a relationship.

Verify:

no relationship proposal is created.

PASS / FAIL


TEST 8 — CONFLICT

Where a controlled conflict can be found:

verify both CAM and external evidence remain visible.

Verify R2D2 does not overwrite CAM.

PASS / FAIL / NOT_APPLICABLE


TEST 9 — R2D2 ASSIST

Open relationship configuration.

Use:

Research Relationship

Verify structured result appears.

Use:

Assist Configuration

Verify suggestions do not alter saved configuration until explicitly applied.

PASS / FAIL


TEST 10 — TEST CONFIGURATION

Run one configured relationship definition against a small test case.

Verify:

MATCH / NO MATCH / INSUFFICIENT

with rule/evidence explanation.

PASS / FAIL


TEST 11 — PERSISTENCE

Verify external research runs, evidence, and proposals persist in the Lending database.

Restart application.

Verify persisted results remain available.

PASS / FAIL


TEST 12 — NO BASELINE MUTATION

Before and after this phase:

internal trusted canonical relationships = 767

unless the baseline count was legitimately changed before this task by an explicit approved action.

R2D2 must not change the frozen baseline.

PASS / FAIL


==================================================
IMPLEMENTATION DISCIPLINE
==================================================

FIRST inspect RPR.

Do not code a new R2D2 client until you have found and understood the proven RPR implementation.

Reuse before creating.

Do not change the RPR project.

Do not create a production architecture.

Do not redesign unrelated UI.

Do not add unrelated features.

Proceed autonomously through the approved scope.

Stop only for a genuine external blocker such as:
- missing manual Stylus preset
- unavailable approved R2D2 credentials
- unavailable SEC capability in the existing RPR configuration


==================================================
FINAL RESPONSE FORMAT
==================================================

When complete provide ONLY:

1. RPR files/functions reused
2. R2D2 auth method reused
3. Runner endpoint/pattern reused
4. Preset strategy used
5. Web research status
6. SEC research status
7. Existing CAM relationship corroboration result
8. New proposal result
9. Mention-only exclusion result
10. R2D2 Assist result
11. Persistent tables/models added
12. Internal baseline before/after
13. TEST 1–12 PASS / FAIL / BLOCKED
14. Genuine blockers

No architecture essay.

STOP immediately after acceptance criteria are satisfied.


==================================================
CORE OBJECTIVE
==================================================

Add R2D2 to the Lending relationship solution by reusing the exact proven RPR authentication + Runner + inline-preset integration pattern, so external Web and SEC evidence can transparently corroborate existing CAM relationships or create reviewable new relationship proposals without ever overwriting the trusted internal Lending baseline.
