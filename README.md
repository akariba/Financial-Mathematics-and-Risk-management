CCR RELATIONSHIP INTELLIGENCE — PROVIDER CONNECTIVITY + EVIDENCE ACQUISITION

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_LIVE_RELATIONSHIP_PILOT_REPORT.md
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md
backend/data/CCR_PHASE3A_CONNECTIVITY_REPORT.md if present

Inspect existing provider code for:

GLEIF
SEC
Web
Helix/internal gateway helpers
certificate/proxy/network configuration

IMPORTANT

The previous bounded pilot proved the orchestrator works, but:

GLEIF failed DNS resolution
SEC failed DNS resolution
Web had no approved adapter configured

Do NOT broaden the pilot.
Do NOT lower evidence standards.
Do NOT create relationships merely to prove the pipeline works.
Do NOT change canonical data.
Do NOT fabricate evidence.

OBJECTIVE

Make the external evidence acquisition layer operational on this Windows
workstation for:

GLEIF
SEC
APPROVED HIGH-QUALITY WEB

Then prove each provider can retrieve one bounded, verifiable document/result.

==================================================
1. DIAGNOSE CURRENT CONNECTIVITY
==================================================

Reproduce the current failures separately from the research orchestrator.

For GLEIF report:

hostname used
DNS resolution result
TCP connection result
TLS result
HTTP result
proxy behavior if applicable
safe error category

For SEC report the same.

Do not print credentials or sensitive headers.

Determine whether failures are caused by:

Windows DNS
corporate proxy
certificate trust
provider hostname/config
Python networking
environment variables
application configuration
other

Do not guess.

==================================================
2. CHECK EXISTING WORKSTATION NETWORK PATTERN
==================================================

Inspect the current environment/repository for approved working outbound
network patterns already used elsewhere.

Look for:

HTTP_PROXY
HTTPS_PROXY
NO_PROXY

enterprise certificate bundle
REQUESTS_CA_BUNDLE
SSL_CERT_FILE

internal gateway helpers
Helix/R2D2 approved network wrappers
existing provider transport abstraction

Reuse approved enterprise configuration.

Do not disable certificate verification.

Do not hardcode personal machine paths if avoidable.

==================================================
3. GLEIF PROVIDER
==================================================

Verify the configured official GLEIF endpoint.

Perform one bounded identity lookup using an existing known-valid local LEI.

Expected:

network works
response is official GLEIF data
response is cached according to current policy
source tier = TIER_1_AUTHORITATIVE_EXTERNAL

Do not yet create a relationship.

Store/retrieve only enough information to prove provider functionality.

==================================================
4. SEC PROVIDER
==================================================

Verify official SEC provider configuration.

Inspect:

User-Agent
headers
request pacing
endpoint paths
CIK discovery behavior

Use only official SEC endpoints already permitted by source policy.

Perform one bounded request against a CCR entity that has a defensible SEC
identity.

Expected:

one official SEC response/document retrieved
source tier = TIER_1_AUTHORITATIVE_EXTERNAL

Respect SEC request-rate expectations.

No broad filing crawl.

==================================================
5. WEB ADAPTER
==================================================

The prior pilot produced:

Web network attempts = 0

because no approved adapter was configured.

Implement/configure ONE approved Web research adapter.

Its job is discovery + retrieval of admissible Web sources.

It must support source quality classification.

Allowed targets:

official company site
official investor relations
official regulatory/government site
major established financial/business publication
approved specialist source

Reject:

SEO pages
anonymous sites
content farms
AI-generated sites
scraped mirrors
search snippets as evidence

Search snippets may identify a candidate URL but cannot become evidence.

==================================================
6. WEB SOURCE CLASSIFICATION
==================================================

Every Web result must carry:

URL
domain
publisher
title
published date if available
retrieved_at

source_tier

TIER_1_AUTHORITATIVE_EXTERNAL
TIER_2_HIGH_QUALITY_SECONDARY
TIER_3_CORROBORATIVE
INADMISSIBLE

admissibility_reason

Do not rely on domain name alone when source type is ambiguous.

==================================================
7. HELIX ROLE
==================================================

If Helix is already working, it may help classify:

document type
publisher type
relationship relevance
candidate evidence passage

But AI may NOT determine source admissibility by itself.

Deterministic/source-policy rules remain authoritative.

AI output is not evidence.

==================================================
8. PROVIDER NORMALIZATION
==================================================

Ensure all three adapters return the orchestrator's normalized result contract:

provider
status

documents_found
claims_found
identity_candidates
evidence_candidates

network_requests
cache_hits

error_category
safe_error_message

Statuses:

SUCCESS
NOT_FOUND
NOT_APPLICABLE
UNAVAILABLE
ERROR

==================================================
9. SAFE CONNECTIVITY STATUS
==================================================

Update provider diagnostics so the application can distinguish:

DNS_ERROR
PROXY_ERROR
TLS_ERROR
AUTH_ERROR
HTTP_ERROR
RATE_LIMITED
CONFIGURATION_INCOMPLETE
NOT_CONFIGURED
READY

Do not collapse all failures into UNAVAILABLE.

==================================================
10. EVIDENCE ACQUISITION TEST
==================================================

Run exactly three bounded tests:

A. one GLEIF lookup
B. one SEC retrieval
C. one approved Web retrieval

For each prove:

successful network acquisition
source tier
document provenance
cache behavior
no sensitive information logged

Do not create production relationships during these tests.

==================================================
11. RE-RUN SMALL RELATIONSHIP TEST
==================================================

Only after all usable providers are functioning:

take ONE of the previously selected high-quality CCR entities.

Run at most:

3 relationship questions.

Use the existing orchestrator.

Objective:

prove real evidence can flow:

provider
→ source document
→ evidence snippet
→ discovered claim
→ governed outcome

Allowed outcome:

PROPOSAL_PENDING_REVIEW
INSUFFICIENT_EVIDENCE
NOT_FOUND
CONFLICT

Do not force a proposal.

==================================================
12. VALIDATION
==================================================

Report:

GLEIF connectivity:
SEC connectivity:
Web connectivity:

GLEIF verified documents:
SEC verified documents:
Web verified documents:

SOURCE_NOT_VERIFIED documents newly produced:
should be 0 unless genuine reason exists

Relationship questions:
<= 3

Claims discovered:
actual

Proposals:
actual

Confirmed relationships:
0

Synthetic edges:
0

AI evidence:
0

==================================================
13. FULL REGRESSION
==================================================

Run the backend suite.

Expected:

0 failed
0 errors

Confirm protected counts and hashes unchanged.

==================================================
14. REPORT
==================================================

Create:

backend/data/CCR_PROVIDER_CONNECTIVITY_EVIDENCE_REPORT.md

Include:

root cause of prior DNS failure
network/proxy configuration used
GLEIF result
SEC result
Web adapter architecture
source classification
bounded acquisition results
one-entity orchestrator test
security controls
regression results

FINAL RESPONSE:

CCR PROVIDER CONNECTIVITY + EVIDENCE: PASS / FAIL

GLEIF
DNS:
TCP:
TLS:
HTTP:
Verified document:
Status:

SEC
DNS:
TCP:
TLS:
HTTP:
Verified document:
Status:

WEB
Adapter configured:
Network request:
Tier-1 retrieval:
Tier-2 retrieval:
Status:

BOUNDED ORCHESTRATOR TEST
Subject:
Questions:
Verified documents:
Claims:
Proposals:
Insufficient evidence:
Not found:
Conflict:

QUALITY
SOURCE_NOT_VERIFIED new documents:
Inadmissible evidence accepted: 0 / FAIL
AI as evidence: 0 / FAIL
Synthetic edges: 0 / FAIL
Confirmed relationships: 0 / FAIL

REGRESSION
passed:
failed:
errors:

REPORT:
backend/data/CCR_PROVIDER_CONNECTIVITY_EVIDENCE_REPORT.md

STOP.
