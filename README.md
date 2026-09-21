EXTERNAL RELATIONSHIP RESEARCH — SOURCE AND EVIDENCE GOVERNANCE

PURPOSE

Research external evidence for the requested entity relationship.

External research is supplemental to CAM/internal Lending evidence.

External evidence must NEVER silently overwrite, replace, or become CAM-authoritative truth.

SOURCE PRIORITY

TIER 1 — PRIMARY / AUTHORITATIVE
Prefer these whenever available:

- SEC filings
- company investor-relations disclosures
- company official press releases
- company regulatory filings
- stock-exchange filings
- government/regulatory sources
- official transaction/financing disclosures
- rating-agency publications when directly relevant

TIER 2 — HIGH-QUALITY SECONDARY
Allowed when primary evidence is unavailable or for corroboration:

- Reuters
- Bloomberg
- Financial Times
- Wall Street Journal
- S&P
- Moody's
- Fitch
- other established institutional financial/business publications

TIER 3 — SPECIALIST / TRADE SOURCES
May be used only as supplemental corroboration when clearly attributable and reputable.

DO NOT USE AS RELATIONSHIP PROOF

- personal blogs
- anonymous blogs
- SEO/content-farm sites
- article aggregators
- scraped/reposted content
- forums
- Reddit/social-media posts
- AI-generated summaries
- generic company-profile websites
- Wikipedia as final evidence
- unsourced claims

RELATIONSHIP EVIDENCE RULE

Do not report a relationship merely because two entities are mentioned together.

A relationship finding requires:

1. clearly identified entities;
2. explicit relationship semantics;
3. an evidence excerpt directly supporting the relationship;
4. source URL/reference;
5. publication/filing date when available;
6. source tier;
7. relationship type;
8. evidence-strength classification.

Do not infer relationships from:
- co-mention;
- same industry;
- geographic proximity;
- common market theme;
- generic ecosystem association;
- similar products;
- proximity in an article.

EVIDENCE STRENGTH

HIGH

Use only when:
- an authoritative primary source explicitly supports the relationship;
OR
- two independent high-quality sources explicitly support the same relationship.

MEDIUM

Use when:
- one strong reputable source explicitly supports the relationship;
- entity identity and relationship semantics are clear;
- no material conflicting evidence exists.

INSUFFICIENT

Use when:
- evidence is vague;
- relationship is inferred;
- source quality is weak;
- only co-mention exists;
- entity identity is uncertain;
- material contradiction exists.

INSUFFICIENT findings must not be presented as validated external relationships.

CAM CORROBORATION

When the requested relationship already exists in CAM:

classify external result as one of:

CAM_CORROBORATION
CONFLICT_REVIEW_REQUIRED
NO_EXTERNAL_CORROBORATION

External evidence does not modify CAM automatically.

NEW EXTERNAL RELATIONSHIPS

When external research finds a relationship not present in CAM:

classify it as:

EXTERNAL_PROPOSAL_PENDING_REVIEW

Never classify an externally discovered relationship as CAM-confirmed.

HIDDEN / INDIRECT RELATIONSHIPS

A hidden relationship requires a complete evidence-backed path.

Example:

A → B → C

A → B must have explicit acceptable evidence.
B → C must have explicit acceptable evidence.

For every hop provide:
- subject
- related entity
- relationship type
- source
- source tier
- evidence excerpt
- evidence strength

If any hop is INSUFFICIENT:

do not validate A → C as a hidden relationship.

Overall hidden-path strength cannot exceed the weakest hop.

RESEARCH DISCIPLINE

Prefer precision over breadth.

Do not attempt to discover every conceivable connection.

Focus on:
- material corporate relationships
- ownership
- parent/subsidiary
- investors/sponsors
- guarantees
- lenders/financing
- customers
- suppliers
- strategic partners
- material technology dependencies
- infrastructure dependencies
- joint ventures
- acquisitions
- significant contractual relationships

Return fewer strong findings rather than many speculative findings.

Always respect the requested AsOfDate.

SOURCE CHANNELS

If SourceChannels = R2D2_WEB:
use Web research only.

If SourceChannels = SEC_FILING:
use SEC filing research only.

If both are supplied:
use both and distinguish the evidence channel for every finding.

Do not substitute one channel for another silently.
