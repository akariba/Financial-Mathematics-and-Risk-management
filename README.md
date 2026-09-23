CCR EXTERNAL RESEARCH — SEC IDENTITY + APPROVED WEB ACTIVATION

Work only in the CURRENT CCR repository.

Read first:

backend/data/CCR_WINDOWS_NETWORK_TRANSPORT_REPORT.md
backend/data/CCR_PROVIDER_CONNECTIVITY_EVIDENCE_REPORT.md
backend/data/CCR_RESEARCH_ORCHESTRATOR_REPORT.md
backend/data/CCR_RELATIONSHIP_EVIDENCE_PATH_POLICY.md

The Windows enterprise network route is now operational.

Known state:

GLEIF:
READY
HTTP 200
verified official identity payload

SEC:
READY
HTTP 200
official reference endpoint reachable
but the bounded subject returned governed NOT_FOUND because no unique SEC
identity mapping was accepted.

Web:
adapter code exists but approved Web execution is not yet operational.

Regression:
56 passed
0 failed
0 errors

Do NOT change the working Windows proxy/TLS solution.

Do NOT disable TLS verification.

Do NOT perform broad external research.

Do NOT create CONFIRMED relationships.

OBJECTIVE

Complete the external provider readiness layer by:

1. making SEC entity/CIK resolution robust and governed;
2. activating one approved high-quality Web research adapter;
3. proving both with bounded verified-source retrievals.

==================================================
1. PRESERVE WORKING TRANSPORT
==================================================

Reuse the existing approved ZSATunnel / proxy transport.

Do not:

change DNS
invent another proxy
disable certificates
bypass enterprise controls

Confirm provider calls inherit the current approved transport.

==================================================
2. SEC IDENTITY RESOLUTION
==================================================

Inspect current SEC identity mapping logic.

The provider can already retrieve:

www.sec.gov/files/company_tickers_exchange.json

but the previous CCR subject could not be uniquely mapped.

Build a deterministic SEC identity-resolution process.

Possible authoritative inputs:

existing local CIK
verified ticker
exact official legal name
known former legal name
SEC company ticker reference data
SEC submissions metadata

Do not use fuzzy name matching alone.

Resolution outputs:

SEC_IDENTITY_RESOLVED
SEC_IDENTITY_AMBIGUOUS
SEC_IDENTITY_NOT_FOUND
SEC_NOT_APPLICABLE

==================================================
3. SEC RESOLUTION QUALITY
==================================================

For each SEC identity candidate capture:

entity_key
CCR/master legal name

candidate CIK
SEC registered name
ticker if available
exchange if available

match_basis
identity_quality

Allowed strong match bases include combinations such as:

existing verified CIK

exact normalized legal name + compatible country/entity context

verified ticker + compatible legal name

authoritative alias + corroborating identity field

Do not resolve merely because names are similar.

==================================================
4. FIND A VALID SEC PILOT SUBJECT
==================================================

From the CCR population identify ONE entity that is:

research_allowed = true
high identity quality
clearly SEC applicable
uniquely resolvable to a CIK

Do not hardcode a famous company if the database can select one dynamically.

Report:

CCR entity
legal name
GFCID
LEI
CIK
SEC registered name
resolution method

==================================================
5. BOUNDED SEC DOCUMENT RETRIEVAL
==================================================

For the selected entity retrieve only a small bounded set.

Prefer:

latest 10-K / 20-F / 10-Q as applicable

or another relevant official filing.

Maximum:

3 SEC filing documents.

Store:

accession
filing type
filing date
official source URL
retrieved_at
source tier

Tier must be:

TIER_1_AUTHORITATIVE_EXTERNAL

No relationship inference required yet.

==================================================
6. WEB ADAPTER ACTIVATION
==================================================

Inspect the existing Web adapter implementation created during the previous
connectivity task.

If it is Reuters-specific, determine the actual approved configuration needed.

Do NOT invent credentials, provider URLs, or undocumented APIs.

If Reuters cannot be legitimately configured from the current environment,
use another already-approved Web/search mechanism available in the repository
or workstation.

The Web layer must support discovery across:

official corporate sites
investor-relations sites
regulatory/government sites
established financial/business publications
approved specialist publications

The Web layer must NOT be tied exclusively to one publisher if the product is
intended for holistic research.

==================================================
7. WEB SOURCE POLICY
==================================================

Every retrieved Web document must be classified as:

TIER_1_AUTHORITATIVE_EXTERNAL
TIER_2_HIGH_QUALITY_SECONDARY
TIER_3_CORROBORATIVE
INADMISSIBLE

Tier 1 examples:

official company
official investor relations
regulator
government
stock exchange

Tier 2:

approved major financial/business journalism

Tier 3:

approved specialist corroboration

Search snippets are:

DISCOVERY_ONLY

never evidence.

==================================================
8. WEB DOCUMENT CONTRACT
==================================================

Store for each retrieved document:

URL
domain
publisher
title
publication date if known
retrieval date

source tier
source type
admissibility
admissibility reason

content fingerprint

Do not store search-result snippets as evidence snippets.

==================================================
9. WEB BOUNDED TEST
==================================================

Using the SAME SEC pilot entity:

retrieve at most:

1 official company/IR document

and

1 high-quality secondary document

if legitimately available.

If no approved Tier-2 provider is configured:

report:

TIER_2_PROVIDER_NOT_CONFIGURED

Do not lower standards.

==================================================
10. GLEIF CROSS-CHECK
==================================================

If the selected entity has an LEI:

perform one bounded GLEIF identity lookup.

Use it only to cross-check identity.

Do not automatically create a parent relationship.

==================================================
11. UNIFIED EXTERNAL IDENTITY
==================================================

Demonstrate that one CCR entity can now have a governed identifier set such as:

GFCID
CAGID
LEI
CIK
ticker
official domain

with provenance per identifier.

Do not treat all identifiers as equally authoritative.

==================================================
12. PROVIDER READINESS STATES
==================================================

Provider diagnostics should now distinguish:

READY
READY_NO_IDENTITY_MATCH
NOT_APPLICABLE
NOT_CONFIGURED
DNS_ERROR
PROXY_ERROR
TLS_ERROR
HTTP_ERROR
RATE_LIMITED
ERROR

Do not report a reachable SEC provider as UNAVAILABLE merely because an entity
was not found.

==================================================
13. NO RELATIONSHIP CREATION YET
==================================================

This task proves identity + evidence retrieval only.

Expected production relationship observations:

0

Expected confirmed relationships:

0

Expected synthetic edges:

0

Identity/source documents are allowed.

==================================================
14. REGRESSION
==================================================

Run full backend tests.

Expected:

0 failed
0 errors

Protected source hashes and Phase-2 fingerprint must remain unchanged.

==================================================
15. REPORT
==================================================

Create:

backend/data/CCR_EXTERNAL_PROVIDER_READINESS_REPORT.md

Include:

SEC identity algorithm
selected SEC pilot subject
SEC filing retrieval
Web adapter/configuration
Web source-tier enforcement
GLEIF identity cross-check
identifier provenance
provider readiness
limitations

==================================================
16. FINAL RESPONSE
==================================================

Return:

CCR EXTERNAL PROVIDER READINESS: PASS / FAIL

TRANSPORT
Approved Windows route:
PASS / FAIL

GLEIF
Connectivity:
Identity lookup:
Status:

SEC
Connectivity:
Resolvable CCR subjects found:
Pilot subject:
CIK:
Resolution basis:
Official filing documents retrieved:
Status:

WEB
Adapter:
Configured:
Official company document:
Tier-2 document:
Search snippets used as evidence:
0 / FAIL
Status:

UNIFIED IDENTITY
GFCID:
LEI:
CIK:
Ticker:
Domain:
Identity quality:

SAFETY
Relationships created:
0 / FAIL

Confirmed relationships:
0 / FAIL

Synthetic edges:
0 / FAIL

AI evidence:
0 / FAIL

TLS verification disabled:
0 / FAIL

REGRESSION
passed:
failed:
errors:

REPORT:
backend/data/CCR_EXTERNAL_PROVIDER_READINESS_REPORT.md

STOP.
