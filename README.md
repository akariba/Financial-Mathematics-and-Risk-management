Continue from the current working Lending implementation.

ABSOLUTE SCOPE

This task is LENDING ONLY.

Do not modify, merge, reuse business logic from, or visually mix with:

CCR
RPR
trading
counterparty-risk workflows
SA-CCR / PFE / EE / XVA
any CCR client population or CCR page

The Lending page must remain a completely separate business experience.

EXISTING COMPONENTS THAT ARE ALREADY WORKING AND MUST NOT BE BROKEN

Preserve all of the following exactly:

frozen internal CAM Lending baseline;
validated/canonical CAM relationships;
current Lending database;
current Lending relationship taxonomy;
current six-input Lending Stylus preset contract;
manually created Stylus preset;
working R2D2 Web integration;
working SEC integration;
current authentication/Runner transport;
R2D2 on-demand execution;
Web-only research mode;
Web + SEC deep-validation mode;
current result caching;
CAM reconciliation;
external evidence persistence;
analyst-review workflow;
evidence provenance;
RPR implementation;
CCR implementation.

Do not change the working preset prompt.

Do not change its six runtime inputs.

Do not rebuild or regenerate the CAM baseline.

Do not modify CAM automatically.

Do not create a new relationship taxonomy.

Do not run R2D2 automatically.

Do not trigger Runner on:

page load;
entity selection;
node click;
filter change;
refresh;
reconnect;
browser reload.

R2D2 must remain explicit analyst-triggered research only.

OBJECTIVE

Transform the current Lending page from a dense technical relationship database view into a decision-oriented Lending Relationship Intelligence platform suitable for senior credit/risk management.

The design must answer five questions immediately:

What changed?
What matters?
Which Lending clients/entities require attention?
Why does it matter for credit?
What action or review is required?

The senior-management homepage must NOT expose every technical detail at once.

Use progressive disclosure:

Executive signal → affected clients/entities → relationship → exact evidence/provenance.

The existing detailed relationship database remains accessible, but must not dominate the landing page.

CORE UX PRINCIPLE

Do not build another packed dashboard.

Organize the product into four conceptual levels:

Level 1 — Executive prioritization

What requires attention?

Level 2 — Theme exploration

Where is concentration/dependency/risk building?

Level 3 — Client/entity investigation

What relationships explain the issue?

Level 4 — Evidence and governance

What exact CAM/Web/SEC evidence supports the conclusion and what review action is required?

The interface should progressively reveal detail instead of displaying everything simultaneously.

REQUIRED PRODUCT STRUCTURE

Implement these four Lending views inside the existing Lending application.

VIEW 1 — SENIOR MANAGEMENT

This becomes the default Lending landing page.

Suggested navigation:

Senior Management
Relationships
Network
Themes
News & Intelligence
Review & Governance

Do not add CCR navigation.

Do not expose technical source inventory or raw database internals on the Senior Management page.

SENIOR MANAGEMENT PAGE
A. HEADER

Display:

Lending Relationship Intelligence — Senior Management View

Subtitle:

Validated CAM relationships with governed external corroboration, relationship proposals and emerging Lending intelligence.

Include:

As-of date
search
compact filters
current baseline status

Example baseline indicator:

CAM baseline — authoritative

External layer indicator:

External intelligence — governed

Do not imply external evidence becomes CAM automatically.

B. EXECUTIVE FILTER BAR

Keep filters compact.

Use only the most decision-relevant filters initially:

Region
Sector
Relationship family/type
Materiality
Evidence status
Relationship state
Portfolio clients only
Highly connected only

Add:

More filters

for advanced filtering rather than showing everything at once.

All widgets below must react consistently to the same filter state.

C. EXECUTIVE KPI STRIP

Maximum approximately 6 primary KPIs.

Recommended primary cards:

1. Lending Clients

Number of confirmed Lending portfolio clients.

2. Material Relationships

Count of relationships classified:

MATERIAL
POTENTIALLY_MATERIAL

where such classification genuinely exists.

3. Hidden / Indirect Relationships

Evidence-backed indirect relationships only.

Do not infer indirectness.

4. Pending Review

External proposals / conflicts / review-required relationships.

5. Adverse / Emerging Signals

Recent external signals requiring attention.

Only display this if real evidence exists.

6. Stale CAM Coverage

Clients with old internal CAM evidence/review dates if dates genuinely exist.

If reliable CAM freshness cannot be calculated, display:

Not available

rather than inventing a figure.

D. CHANGE INDICATORS

Each KPI should show change only when comparable historical snapshots genuinely exist.

Examples:

+12 since previous snapshot
+6%
4 newly identified
3 moved into review

Never create fake trend history.

If previous-state data does not exist:

hide the trend.

E. EXECUTIVE RISK PRIORITIES

Create a prominent panel:

Executive Risk Priorities

This is one of the most important components.

Show approximately the top 5 active issues.

Examples of issue families:

Concentration to common owners / sponsors

Many Lending clients connected to the same owner/sponsor.

Hidden / indirect dependency

Material indirect supplier, technology, infrastructure, ownership or support chains.

Guarantor / credit-support concentration

Multiple Lending clients depending on the same support entity.

Customer / supplier concentration

Material dependency on a small number of customers, suppliers or infrastructure providers.

Adverse external developments

Credible recent Web/SEC evidence affecting important connected entities.

CAM freshness

Important clients whose CAM source evidence appears stale.

Evidence conflict

External evidence conflicts with an existing CAM relationship/state.

Review backlog

High-materiality proposals awaiting analyst decision.

Each priority must display:

issue title;
short explanation;
number of affected clients;
severity or materiality;
latest change/date when known;
drill-down action.

Do not generate speculative management conclusions.

Priorities must be derived from actual application data.

F. WHAT CHANGED

Create a dedicated component:

What Changed

Prioritize changes over static totals.

Possible categories:

new material relationship;
new external proposal;
new CAM corroboration;
newly identified indirect dependency;
new adverse external evidence;
evidence conflict;
relationship state changed;
materiality changed;
CAM evidence became stale;
proposal approved/rejected.

Only show changes supported by real before/after data.

Do not invent historical changes.

Allow time filters if data supports them:

since last review
7 days
30 days
custom period
G. GLOBAL RELATIONSHIP FOOTPRINT

Add a world map as a management lens, not decorative geography.

Title:

Global Relationship Footprint

Purpose:

Show geographic concentration of important Lending relationships and connected entities.

Use actual available country/geography data only.

Do not geocode or assign countries based purely on company names if geography is unavailable.

Where no geography exists:

do not place the entity on the map.

Map should support:

region clustering;
material relationships;
emerging issues;
adverse external signals;
AI ecosystem relationships;
mention-only signals;
concentration hubs.

Suggested visual semantics:

blue = trusted/material Lending relationships
orange = emerging issue
yellow = mention-only/context signal
red = adverse/conflict signal
outlined cluster = AI ecosystem cluster

Clicking a region or bubble should filter the rest of the management view.

Do not automatically invoke R2D2.

H. AI ECOSYSTEM LENS / “AI BUBBLE”

Add a specific management lens for AI ecosystem concentration.

It should identify clusters such as:

AI model developers
hyperscalers/cloud
GPU/chip suppliers
data center/infrastructure providers
major enterprise AI customers
investors/sponsors
financing/support entities

BUT:

Only classify entities when the underlying data or explicit relationship evidence supports the category.

Do not infer company role from model pre-training.

The UI can show labels such as:

AI Ecosystem — High Concentration

or:

AI Ecosystem — Growing Cluster

only when actual data supports the condition.

Clicking the AI ecosystem bubble should drill into:

affected Lending clients;
connected entities;
relationship type;
materiality;
direct/indirect path;
supporting evidence;
external developments.
I. NEWS / INTELLIGENCE SIGNALS

Add a governed external-intelligence layer.

This must remain clearly separate from CAM.

Examples:

adverse Web development;
SEC filing update;
corporate transaction;
customer/supplier development;
sponsor change;
technology dependency event;
regulatory/legal development.

Every signal must show:

affected Lending client;
related entity;
signal date;
source;
relationship relevance;
whether it is:
corroborating;
proposed;
conflict;
mention-only;
no supported relationship.

Mention-only evidence must never automatically create a relationship.

Do not label sentiment as negative unless the external structured evidence actually supports that classification or the application has a real governed rule for it.

J. RELATIONSHIP CONCENTRATION

Include one simple management-level relationship concentration visualization.

Possible display:

Relationship Type Mix

Use relationship families such as:

Ownership / Sponsor
Credit Support
Supplier / Infrastructure
Customer / Revenue
Technology / AI ecosystem
Regulatory / Legal
Other

Avoid showing all atomic types on the executive page.

Atomic relationship types remain available deeper in the application.

K. CONCENTRATION BY REGION

Show:

Top Regions by Concentration

Only if geography is available.

Rank regions using actual relationship/entity counts or material relationships.

Do not invent exposure amounts.

If financial exposure is unavailable, label the metric clearly as:

Relationship concentration

not:

Credit exposure.

L. REVIEW / ESCALATION WATCHLIST

Create:

Review Queue / Escalation Watchlist

Examples:

high materiality + pending review
evidence conflict
stale CAM
newly adverse external evidence
highly connected entity
AI ecosystem concentration
regulatory/legal development
new external relationship proposal

Each row should provide:

affected client/entity;
reason;
materiality;
evidence status;
age;
action.
M. R2D2 ASSIST — EXECUTIVE VERSION

Keep R2D2 Assist but simplify its role on the management page.

It should answer questions using existing governed data and cached research first.

Suggested questions:

Show material indirect dependencies.
Which clients share common owners or sponsors?
Where is AI ecosystem concentration highest?
Which entities connect several Lending clients?
Which relationships have conflicting evidence?
Which clients have recent external developments?
Which CAM evidence looks stale?
Which external proposals need review?

The Assistant must not silently mutate CAM.

Research calls remain explicit.

VIEW 2 — THEMES

Create a dedicated Theme Explorer.

Tabs:

Concentration

Identify entities shared across multiple Lending clients.

Ownership / Sponsor Chains

Parents, sponsors, common owners, investment structures.

Guarantor / Credit Support

Guarantors, backleverage, lenders and support structures.

Customer / Supplier Dependency

Critical suppliers, customer dependency, contracted customers.

Technology / Infrastructure

Technology dependency and infrastructure dependency.

AI Ecosystem

AI-specific relationships and clusters supported by evidence.

News / Regulatory

External developments, regulator/legal relationships and conflicts.

CAM Freshness

Old/stale source evidence.

Review Queue

External proposals and conflict-review cases.

Each theme page should contain:

key metrics;
affected clients;
connected entities;
simple visualization;
trend/change if available;
drill-down into individual relationships.
VIEW 3 — CLIENT / ENTITY PROFILE

When a user selects a Lending client or related entity, open a dedicated profile.

Do not overload the executive homepage with this information.

Profile should contain:

Executive summary
client/entity name;
CAGID/entity ID where known;
portfolio-client status;
entity category;
geography where known;
number of connected entities;
number of material relationships;
number direct/indirect;
current/historical/emerging;
CAM-confirmed;
externally corroborated;
proposals;
conflicts;
CAM freshness.
RELATIONSHIP NETWORK

The detailed network belongs here.

Network should:

center selected entity;
display validated CAM relationships by default;
allow external overlay;
differentiate direct/indirect;
differentiate relationship families;
differentiate current/emerging/historical;
allow node pivoting;
allow edge selection;
avoid loading hundreds of irrelevant nodes initially;
allow expansion progressively.

Never trigger Runner when clicking nodes.

Cached data only until explicit research action.

NETWORK VISUAL SEMANTICS

Use consistent edge styles:

solid = direct
dashed = indirect
dotted = historical/context
highlighted red/orange = conflict/review state
separate external overlay = externally sourced

Use relationship-family node/edge categories rather than dozens of arbitrary colors.

Always provide a legend.

Avoid visual clutter.

RELATIONSHIP TABLE

Keep a detailed relationship table in the client/entity view.

Suggested columns:

Related entity
Relationship
Relationship family
Direction
Connectivity
State
Materiality
Confidence
Evidence status
Source count
Last evidence date
Why it matters

Allow:

sorting;
filtering;
search;
expandable rows.

Do not show hundreds of rows by default.

Use pagination or virtualized loading.

RIGHT-SIDE EXPLAINABILITY DRAWER

This is essential.

Clicking any:

executive priority;
KPI item;
map bubble;
graph edge;
table row;
news signal

should open a consistent right-hand panel.

Panel should answer:

What is the relationship?

Atomic relationship type.

Why was it surfaced?

Short evidence-grounded explanation.

Why does it matter for Lending credit?

Use the existing credit relevance rule.

Is it trusted?

Display clearly:

CAM Confirmed
Web Corroborated
SEC Corroborated
External Proposal
Conflict Review
Mention Only
Relationship state

Current / Emerging / Historical / Terminated / Unknown.

Connectivity

Direct / Indirect / Unknown.

Materiality

Material / Potentially Material / Contextual / Unknown.

Confidence

High / Medium / Low / Insufficient.

Evidence

Show actual supporting excerpts.

Sources

Separate:

CAM
Web
SEC

Never merge provenance.

Review

Show:

pending;
approved;
rejected;
conflict;
analyst notes where available.
VIEW 4 — REVIEW & GOVERNANCE

Create a dedicated governance workspace.

This page handles:

external proposals;
conflict review;
mention-only findings;
CAM corroborations;
stale CAM alerts;
rejected findings;
analyst decisions.

Columns:

client;
related entity;
relationship type;
finding type;
materiality;
confidence;
source;
created date;
reviewer;
status.

Actions only where already supported:

approve proposal;
reject proposal;
mark reviewed;
open evidence;
add analyst note.

Never auto-approve.

Never automatically promote external evidence into CAM.

EVIDENCE STATUS VISUAL LANGUAGE

Use one consistent system throughout Lending.

CAM Confirmed

Trusted internal baseline.

Web Corroborated

External Web evidence supports CAM.

SEC Corroborated

SEC evidence supports CAM.

External Proposal

Supported externally but not present in canonical CAM.

Conflict Review

External evidence contradicts CAM or supplied state.

Mention Only

Entities co-mentioned but relationship not established.

Use consistent badges everywhere.

COLOR SEMANTICS

Keep colors semantic and restrained.

Suggested:

green = trusted / CAM-confirmed
blue = corroborated / informational
amber = pending review / emerging
red = conflict / adverse priority
gray = mention-only / contextual / unavailable

Do not use color alone.

Always include text labels/icons.

DO NOT CALL EVERYTHING “RISK”

Use precise language.

Examples:

Use:

relationship concentration
connected-entity concentration
material dependency
governance backlog
emerging external signal
evidence conflict

Do not claim:

exposure
expected loss
loss amount
financial impact
probability of default
stress loss

unless such data actually exists.

NO FAKE DATA

This is critical.

Do not populate attractive widgets with mock numbers.

If the backend does not contain the required field:

display:

Not available

or hide the widget.

Examples:

geography unavailable → do not plot it;
no previous snapshot → no trend;
no adverse-news classifier → do not fabricate one;
no financial exposure → use relationship count, not dollar exposure;
no industry → do not guess industry;
no materiality → show Unknown.
SOURCE INVENTORY

Move the large source inventory away from the Senior Management homepage.

Place it under:

Review & Governance → Data Provenance

or a collapsible audit section.

Keep full auditability but remove visual clutter from the management experience.

PROGRESSIVE DISCLOSURE

Required interaction pattern:

Management signal

↓

Affected clients/entities

↓

Relationship

↓

Evidence

↓

Governance action

Do not expose all five levels simultaneously.

PERFORMANCE

The management homepage should load from the existing database/cache.

It must NOT wait for R2D2.

Runner calls can take approximately minutes and must remain separate from normal browsing.

Cached external research should display immediately.

Explicit actions:

Research Web

R2D2_WEB only.

Deep Validation

R2D2_WEB + SEC_FILING.

The UI should clearly indicate:

cached;
running;
completed;
failed;
review required.
RESEARCH RESULTS

After successful R2D2 execution:

parse strict JSON;
resolve entities locally;
compare against CAM;
classify as:
CAM_CORROBORATION
EXTERNAL_PROPOSAL_PENDING_REVIEW
CONFLICT_REVIEW_REQUIRED
MENTION_ONLY
NO_EVIDENCE
preserve Web/SEC separately;
persist external evidence separately;
refresh only the affected UI components;
never rebuild or mutate CAM.
SAVED VIEWS

If feasible using the existing architecture, allow users to save filter configurations such as:

AI ecosystem
high materiality
indirect dependencies
pending review
stale CAM
guarantor chains
sponsor concentration

Do not build a large new framework if simple local/persisted configuration is sufficient.

POC-level implementation is acceptable.

DESIGN EXPECTATION

Use the reference senior-management dashboard concept only as an inspiration.

Do NOT blindly reproduce every panel.

The result should be:

less crowded;
more hierarchical;
easier to interpret;
suitable for senior management;
visibly Lending-specific;
explainable;
auditable;
governed;
actionable.

Prioritize clarity over showing maximum data.

IMPLEMENTATION RULES

Proceed autonomously.

Do not stop for approval during implementation.

Inspect the existing code and reuse working components where possible.

Do not perform broad refactoring.

Do not introduce unnecessary architecture.

Do not redesign unrelated pages.

Do not change the frozen CAM pipeline.

Do not modify CCR.

Do not modify RPR.

Do not modify the Stylus preset.

Do not modify the six-input contract.

Do not rebuild the Lending database unless strictly required for a real bug.

Do not create loops.

Do not repeatedly rerun tests.

Make one implementation pass and one validation pass.

ACCEPTANCE TEST

After implementation, perform one bounded validation cycle.

Validate:

Lending Senior Management page loads.
Existing CAM baseline count remains unchanged.
Existing canonical relationships remain unchanged.
Executive KPIs use actual Lending data only.
Executive priorities use actual data only.
Management filters work consistently.
Client drill-down works.
Network node pivot works.
Relationship table works.
Evidence drawer works.
CAM/Web/SEC provenance remains separate.
External proposals remain separate from CAM.
Mention-only findings do not become relationships.
R2D2 does not run automatically.
Web Research remains explicit.
Deep Validation remains explicit.
Cached results load without Runner.
Review workflow remains functional.
World map only uses genuine geography.
AI ecosystem lens only uses supported classifications.
No fabricated metrics/data appear.
CCR remains unchanged.
RPR remains unchanged.
CAM baseline remains unchanged.
FINAL RESPONSE FORMAT

Return only:

Senior Management View: PASS/FAIL
Executive priorities: PASS/FAIL
What Changed: PASS/FAIL
Global map: PASS/FAIL
AI ecosystem lens: PASS/FAIL
News/intelligence layer: PASS/FAIL
Theme Explorer: PASS/FAIL
Client/entity profile: PASS/FAIL
Network drill-down: PASS/FAIL
Relationship table: PASS/FAIL
Explainability drawer: PASS/FAIL
Review & Governance: PASS/FAIL
R2D2 on-demand only: PASS/FAIL
Web/SEC provenance separation: PASS/FAIL
No fabricated data: PASS/FAIL
CAM baseline unchanged: PASS/FAIL
CCR unchanged: PASS/FAIL
RPR unchanged: PASS/FAIL

If any item cannot be implemented because the underlying real data does not exist, state:

NOT AVAILABLE — underlying data absent

Do not fabricate a substitute.

Then STOP.
