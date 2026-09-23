CCR CONNECTIVITY — WINDOWS NETWORK TRANSPORT DIAGNOSTIC

Work only in the CURRENT CCR repository and CURRENT Windows workstation.

Read:

backend/data/CCR_PROVIDER_CONNECTIVITY_EVIDENCE_REPORT.md
backend/data/CCR_PHASE3A_CONNECTIVITY_REPORT.md if present

The current provider tests fail before HTTP:

GLEIF = DNS_ERROR / Windows error 11001
SEC = DNS_ERROR / Windows error 11001

Reuters Web is NOT part of this task.

Do NOT modify relationship logic.
Do NOT create relationships.
Do NOT modify canonical data.
Do NOT lower TLS/security controls.
Do NOT disable certificate verification.
Do NOT run broad external research.

OBJECTIVE

Find and fix the approved Windows networking path so Python can resolve and
reach official GLEIF and SEC endpoints.

==================================================
1. REPRODUCE OUTSIDE APPLICATION
==================================================

Using PowerShell and Python separately, test:

DNS resolution
TCP 443
TLS
HTTP HEAD/GET where appropriate

for the exact hostnames currently configured by the GLEIF and SEC providers.

Report each layer independently.

Do not infer DNS failure from a higher-level request.

==================================================
2. WINDOWS DNS
==================================================

Inspect safely:

Get-DnsClientServerAddress

Resolve-DnsName for provider hostnames

nslookup for provider hostnames

Python socket.getaddrinfo()

Determine whether:

Windows itself cannot resolve

or

only Python cannot resolve.

Record Windows error codes.

==================================================
3. PROXY / ENTERPRISE NETWORK
==================================================

Inspect:

HTTP_PROXY
HTTPS_PROXY
NO_PROXY
REQUESTS_CA_BUNDLE
SSL_CERT_FILE

Also inspect Windows proxy state:

netsh winhttp show proxy

and current user Internet/WinINET proxy configuration where accessible.

Do not print credentials embedded in proxy URLs.

If an approved enterprise proxy already exists, reuse it.

Do not invent a proxy.

==================================================
4. EXISTING WORKING NETWORK PATTERN
==================================================

Search the repository and current environment for an already working approved
network implementation.

Look for:

requests.Session
httpx.Client
proxy helpers
certificate bundle helpers
Helix/R2D2 network helpers
internal gateway transport
corporate CA configuration

We previously had connectivity work in this environment, so prefer reuse of an
existing approved pattern over creating a new transport stack.

==================================================
5. HOSTNAME VALIDATION
==================================================

Confirm the provider hostnames are still the intended configured hosts.

Do not silently replace provider endpoints.

If a configured hostname is wrong/stale, document the exact configuration
issue before changing it.

==================================================
6. PYTHON TRANSPORT TEST
==================================================

Create a minimal temporary diagnostic using the SAME Python environment as the
CCR backend.

Test:

socket DNS
TLS handshake
HTTP response

separately.

Safe output only:

hostname
resolved IP count
TCP success
TLS success
HTTP status
error category

Never output cookies, authorization headers, or secrets.

==================================================
7. APPLY MINIMAL FIX
==================================================

Only after root cause is proven, make the smallest approved fix.

Possible examples:

reuse approved proxy settings

reuse corporate CA bundle

correct provider transport configuration

inherit Windows approved proxy in Python

fix an incorrect hostname/config value

Do NOT:

disable TLS verification

use hardcoded public DNS

change system DNS without explicit necessity

bypass enterprise controls

==================================================
8. RETEST PROVIDERS
==================================================

After the transport fix run exactly:

one GLEIF request

one SEC request

No broad search.

Expected progression:

DNS = PASS
TCP = PASS
TLS = PASS
HTTP = PASS or a provider-specific governed HTTP result

If HTTP fails after DNS succeeds, report that as the NEW root cause rather
than continuing to modify unrelated code.

==================================================
9. REGRESSION
==================================================

Run backend tests.

Expected:

0 failed
0 errors

No canonical counts changed.

No relationships created.

No evidence fabricated.

==================================================
10. REPORT
==================================================

Create:

backend/data/CCR_WINDOWS_NETWORK_TRANSPORT_REPORT.md

FINAL RESPONSE:

CCR WINDOWS NETWORK TRANSPORT: PASS / FAIL

ROOT CAUSE:
<exact>

GLEIF
DNS:
TCP:
TLS:
HTTP:

SEC
DNS:
TCP:
TLS:
HTTP:

WINDOWS DNS:
PASS / FAIL

PYTHON DNS:
PASS / FAIL

PROXY REQUIRED:
YES / NO / UNKNOWN

PROXY CONFIGURATION SOURCE:
<safe description>

CORPORATE CA REQUIRED:
YES / NO / UNKNOWN

FIX APPLIED:
<exact safe summary>

TLS VERIFICATION DISABLED:
0 / FAIL

RELATIONSHIPS CREATED:
0 / FAIL

EXTERNAL RESEARCH QUESTIONS:
0 / FAIL

REGRESSION:
passed:
failed:
errors:

REPORT:
backend/data/CCR_WINDOWS_NETWORK_TRANSPORT_REPORT.md

STOP.
