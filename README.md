LENDING RELATIONSHIP INTELLIGENCE
PROMPT 4A — EXECUTIVE INTELLIGENCE HOME + PRODUCT SHELL

Work only in the CURRENT Lending repository.

Prompt 3C is complete.

Read first:

LENDING_FOUNDATION_AUDIT.md
LENDING_CANONICAL_RELATIONSHIP_CONTRACT_REPORT.md
LENDING_PROMPT3_ACCEPTANCE_REPORT.md
LENDING_PROMPT3C_REMEDIATION_REPORT.md

Treat the Prompt 3C conclusion READY FOR PROMPT 4 as the authoritative
foundation.

Also inspect the CURRENT frontend before changing anything.

IMPORTANT:

This is Lending only.

Do not touch CCR.
Do not use Customer_latest.parquet.
Do not redesign backend authority rules.
Do not rewrite CAM/V3.
Do not call SEC.
Do not call web.
Do not call Stylus.
Do not perform live external research.
Do not build the advanced relationship graph yet.
Do not build final AI orchestration yet.

This prompt establishes the new product shell and executive home experience.

==================================================
BUSINESS VISION
==================================================

The Lending application is evolving from a collection of analytical pages
into a senior-user Relationship Intelligence platform.

The target users include:

- senior credit officers
- portfolio managers
- relationship managers
- senior risk managers
- management stakeholders

These users should NOT need to understand:

- database lanes
- V2/V3 internals
- normalized stores
- candidate stores
- API contracts
- extraction internals
- taxonomy implementation details

The product must translate those technical foundations into an intuitive,
high-confidence analytical experience.

The first screen must answer immediately:

1. What matters in my lending portfolio?
2. Where is our largest exposure?
3. What relationships could transmit risk?
4. What has changed or deserves attention?
5. Which clients should I investigate?
6. Why is the system showing me this?
7. What can I ask the AI next?

This is not merely a dashboard.

It should feel like an intelligence workstation.

==================================================
1. PRESERVE THE DATA CONTRACT
==================================================

All portfolio relationship reads must use the common governed Lending
relationship contract established in Prompt 3.

Do not create another relationship universe.

Distinguish clearly:

- assertions
- semantic relationships
- endpoint pairs
- connected entities

Do not display 808 assertions as though they are 808 unique counterparties
or 808 unique endpoint pairs.

The current trusted-read metrics are approximately:

808 assertions
808 semantic groups
376 endpoint pairs
255 connected entities
28 review-required assertions
3 conflict assertions

Use live API results when available instead of hard-coding these values.

Every displayed metric must have a defined denominator and semantic meaning.

==================================================
2. FRONTEND TECHNICAL DIRECTION
==================================================

Inspect the current frontend stack first.

If the application already uses React/TypeScript, preserve and improve it.

Do NOT introduce a second frontend framework.

Build reusable components rather than page-specific duplicated components.

Prefer:

- React
- TypeScript
- existing routing conventions
- existing API client conventions
- reusable hooks
- reusable cards/panels
- reusable filter controls
- responsive CSS/layout primitives

Use the existing design system where practical but materially improve the
visual experience.

Avoid unnecessary new dependencies.

If a new library is required, document why before adding it.

==================================================
3. DESIGN LANGUAGE
==================================================

The application should become:

LIGHT
PREMIUM
INSTITUTIONAL
CALM
INFORMATION-DENSE
INTERACTIVE

Do not use a dark cyberpunk aesthetic.

Use a primarily light canvas with:

- white / near-white surfaces
- restrained grey borders
- subtle depth
- generous spacing
- dark navy/charcoal typography
- controlled use of teal / blue / green
- amber for review attention
- red only for genuine conflicts/severe attention

The interface should feel credible for institutional credit professionals.

Avoid:

- excessive gradients
- excessive glowing
- decorative animations
- meaningless gauges
- excessive rounded cards
- visual noise

Use motion only to communicate:

- selection
- filtering
- relationship activation
- AI analysis
- drill-down
- new attention signals

==================================================
4. NEW PRODUCT SHELL
==================================================

Redesign the Lending application shell while keeping existing routes working.

Create a clearer navigation hierarchy.

Recommended top-level information architecture:

HOME
PORTFOLIO
NETWORK
RELATIONSHIPS
INTELLIGENCE
REVIEW

Do not expose technical implementation terminology in primary navigation.

Existing routes may remain underneath these labels.

Provide an unobtrusive product identity:

LENDING
Relationship Intelligence

Top navigation should also provide:

- global client/entity search
- AI entry point
- data/source status indicator
- review attention count
- current analytical scope

Do not fake functionality.

If an action is not yet implemented, visually indicate that it is coming
later or do not expose it.

==================================================
5. GLOBAL INTELLIGENCE COMMAND BAR
==================================================

Create a prominent but elegant global command/search interaction.

The user should be able to enter things such as:

CoreWeave
NVIDIA
Show my largest AI infrastructure exposures
Which clients depend on NVIDIA?
Show relationships requiring review
Where are my largest concentrations?
Explain this relationship

For Prompt 4A:

DO NOT connect these natural-language commands to a live LLM.

Implement the visual shell and deterministic routing/search behavior only
where existing application data permits it.

Provide a clean placeholder for the future AI orchestration contract.

Suggested prompt chips may include deterministic routes such as:

Largest exposures
Relationship concentrations
Review required
Explore network
Clients without CAM coverage

Clearly mark future AI-generated actions separately from existing
deterministic analytics.

==================================================
6. EXECUTIVE HOME
==================================================

Transform the current Overview into an Executive Intelligence Home.

It should tell a coherent story rather than displaying unrelated widgets.

Recommended page structure:

A. EXECUTIVE HEADER

Title:
Portfolio Intelligence

Subtitle:
A short institutional description of exposure, relationships, concentration,
and emerging attention.

Provide context such as:

portfolio population
reported exposure
CAM coverage
relationship coverage
review attention

Do not overfill this area.

--------------------------------------------------
B. ATTENTION STRIP
--------------------------------------------------

Create an executive attention strip immediately below the header.

This should surface a small number of deterministic signals.

Examples based on existing data:

Largest exposure concentration
Largest sector concentration
Clients with review-required relationships
Relationship conflicts
High-exposure clients without CAM
High-exposure clients without relationship intelligence

Each signal should be clickable.

Do not infer unsupported credit risk conclusions.

Use language such as:

Attention
Coverage gap
Relationship review
Concentration
Data conflict

not:

Danger
Critical risk
Likely default

unless source data explicitly supports such a conclusion.

--------------------------------------------------
C. PORTFOLIO EXPOSURE
--------------------------------------------------

Provide a strong visual portfolio exposure module.

Include existing deterministic measures such as:

total reported exposure
top clients
top 10 share
top 20 share
sector concentration
country concentration

Allow drilling into clients.

Exposure remains a portfolio measure.

Do not convert exposure into a relationship-risk score.

--------------------------------------------------
D. RELATIONSHIP INTELLIGENCE
--------------------------------------------------

Create a dedicated relationship intelligence module showing:

semantic relationships
connected entities
endpoint pairs
review-required relationships
conflicts

Also surface:

top relationship families
largest connected client ecosystems
clients with highest relationship counts

Only use metrics supported by existing APIs.

Label exactly what is being counted.

Do not show assertion count under the label “relationships” without
qualification.

--------------------------------------------------
E. NETWORK PREVIEW
--------------------------------------------------

Retain a visually compelling network preview on the home page.

Prompt 4A should NOT build the advanced network engine yet.

Use the current bounded graph capability but restyle its container and
interaction shell.

The preview should show:

selected/high-exposure ecosystem
a small relationship neighborhood
relationship family
source authority
review/conflict state

Provide:

Open Network

to transition to the future advanced Network workspace.

Do not render all 808 assertions at once.

--------------------------------------------------
F. GEOGRAPHIC INTELLIGENCE
--------------------------------------------------

Retain geography because senior users find it visually intuitive.

Improve the layout around the current portfolio map.

The map should communicate primarily:

exposure geography

and secondarily:

relationship overlay availability

Do not imply that map intensity is a credit-risk score.

Provide toggles such as:

Exposure
Client count
CAM coverage
Relationship coverage

Only show a layer if its data actually exists.

--------------------------------------------------
G. COVERAGE & DATA CONFIDENCE
--------------------------------------------------

Create a compact but meaningful coverage panel.

Possible deterministic metrics:

CAM coverage
relationship coverage
external-intelligence coverage if genuinely available
review-required count
conflict count

Explain denominator on hover or drill-down.

Avoid meaningless generic “confidence scores.”

--------------------------------------------------
H. SUGGESTED INVESTIGATIONS
--------------------------------------------------

Create an important new section:

Suggested Investigations

For Prompt 4A this must be generated deterministically from existing data,
NOT by an LLM.

Examples:

High exposure / limited relationship coverage
High exposure / no CAM coverage
Many relationships requiring review
Relationship conflict present
Large concentration in one sector/country
Highly connected client ecosystem

Each card should explain:

WHY THIS IS SHOWN

using explicit deterministic facts.

Example:

“$5B reported exposure and no governed relationship records.”

not:

“This client is risky.”

Each investigation links into an existing client/network/relationship view.

==================================================
7. GLOBAL SEARCH
==================================================

Improve global search.

It should support at minimum:

client name
CAGID where applicable
connected entity name where supported

Search results should distinguish:

Portfolio Client
Connected Entity

Do not assume every connected entity has portfolio exposure.

Selecting:

Portfolio Client
→ Client Detail

Connected Entity
→ relationship/network context if supported

Do not fabricate a client profile for an external-only entity.

==================================================
8. CLIENT CARD STANDARD
==================================================

Create a reusable client summary component for use throughout the
application.

It may expose:

client name
CAGID
sector
country
reported exposure
portfolio share
CAM coverage
relationship count
review count
conflict indicator

Only display fields supported by the current data contract.

This component should become reusable in later prompts.

==================================================
9. RELATIONSHIP ATTENTION STANDARD
==================================================

Create shared visual semantics for relationship states.

Examples:

Governed / confirmed
Review required
Conflict
External support
AI published

These are NOT equivalent authority states.

Do not flatten them into one generic status.

CAM/V3 authority must remain distinguishable.

Supplemental evidence must remain distinguishable.

AI-published relationships must remain distinguishable.

==================================================
10. EXPLAINABILITY ENTRY POINT
==================================================

Every relationship-oriented card or metric that can be drilled into should
have a consistent future explainability affordance:

Why am I seeing this?

Prompt 4A does not need to build the full explainability drawer.

But establish the component/interface contract required by Prompt 4B.

The future drawer will expose:

relationship type
entities
direction
state
authority
source lanes
evidence
source documents
exact excerpts
review status
conflicts
lineage

Do not create placeholder fake evidence.

==================================================
11. REVIEW ATTENTION
==================================================

The Review entry point should clearly expose the count of items that actually
require attention.

Do not combine unrelated review universes into one number without explanation.

If multiple queues exist, the UI should allow a future breakdown.

For now show the governed portfolio review semantics supported by the common
contract.

==================================================
12. RESPONSIVENESS
==================================================

The application is primarily designed for desktop institutional users.

Optimize first for:

1920×1080
large enterprise monitors
standard laptop widths

Avoid very tall cards requiring excessive scrolling.

Use responsive grid behavior.

Make key executive signals visible within the initial viewport where
possible.

==================================================
13. ACCESSIBILITY
==================================================

Maintain:

keyboard navigation
visible focus states
sufficient contrast
semantic headings
accessible button labels
tooltips that are not mouse-only

Do not encode status exclusively through color.

==================================================
14. PERFORMANCE
==================================================

Do not render large network datasets on initial home-page load.

Reuse current portfolio endpoints efficiently.

Avoid duplicate API calls where data is already present.

Use memoization/caching where appropriate within the existing frontend
architecture.

No premature architectural rewrite.

==================================================
15. REMOVE OR DOWNPLAY TECHNICAL CLUTTER
==================================================

The current portfolio UI exposes several implementation-oriented concepts.

Do not delete backend capabilities.

But primary senior-user screens should avoid prominently showing terms such
as:

V2 fallback
V3 candidate
normalized store
candidate database
overlay store
AI instance store

These concepts can remain available in:

advanced provenance
explainability
admin/governance
debug/developer context

The executive interface should instead use business semantics.

==================================================
16. DO NOT YET IMPLEMENT
==================================================

Do NOT yet implement:

advanced force-directed graph redesign
relationship edge animation
community detection redesign
news/event ingestion
interest-rate shock propagation
stress simulation
live Stylus calls
live SEC calls
live web calls
automatic external fallback
full AI chat
AI relationship configuration redesign
natural-language query execution
relationship preset redesign

These belong to later Prompt 4 stages.

Do prepare reusable UI contracts for them.

==================================================
17. TESTING
==================================================

Add frontend tests covering at minimum:

Executive Home renders from current APIs.

Portfolio metrics preserve current values.

Relationship count semantics distinguish:

assertions
semantic relationships
endpoint pairs
connected entities.

Review-required and conflict states display distinctly.

Suggested Investigations use deterministic rules only.

Global search distinguishes clients from connected entities where supported.

No external provider is called on normal page load.

No AI generation endpoint is called on normal page load.

Existing Lending routes continue to work.

Prompt 3 benchmark/backend tests remain passing.

==================================================
18. VISUAL ACCEPTANCE
==================================================

Manually inspect the following screens after implementation:

Executive Home
Clients
Client Detail
Network
Relationship Explorer
External Research
Review

The new shell should make them feel like one coherent product even before
later Prompt 4 redesigns.

Do not fully redesign all subordinate pages in this prompt.

==================================================
19. REPORT
==================================================

Create:

LENDING_PROMPT4A_EXECUTIVE_HOME_REPORT.md

Document:

frontend stack
files changed
new component architecture
navigation structure
Executive Home sections
API endpoints consumed
count semantics
Suggested Investigation rules
search behavior
relationship status semantics
explainability interface contract
performance considerations
tests
remaining work for 4B–4H

Include screenshots if the existing project workflow supports them.

Conclude with exactly one:

READY FOR PROMPT 4B

or

NOT READY FOR PROMPT 4B

STOP when complete.

Do not begin Prompt 4B.
