LENDING RELATIONSHIP INTELLIGENCE
PROMPT 3 — CANONICAL RELATIONSHIP CONTRACT + UNIFIED LINEAGE FOUNDATION

Continue in the CURRENT Lending repository and use the completed:

- Common Operating Contract
- Prompt 1 final architecture and lineage audit
- Prompt 2 outputs
- LENDING_FOUNDATION_AUDIT.md

as the authoritative baseline.

IMPORTANT SCOPE

This is LENDING ONLY.

Do NOT use, inspect, migrate, join, reference, or design around:

- Customer_latest.parquet
- the ~3.67M customer population
- CCR customer-master logic
- CCR exposure populations
- CCR databases
- CCR entity models
- CCR routes
- any non-Lending customer-master concept

Customer_latest.parquet belongs exclusively to CCR.

Do not re-open that question.

==================================================
OBJECTIVE
==================================================

The current Lending application exposes several legitimate but separate
relationship universes:

1. CAM / V3
2. conditional V2 fallback
3. normalized governed workbench
4. external research / V3-aware external overlay
5. published AI relationship instances

The architecture audit established that these currently have:

- different IDs
- different entity representations
- different review states
- different quality semantics
- different publication rules
- different API projections
- incomplete cross-lane lineage

DO NOT solve this by flattening all stores into one physical table.

DO NOT make every source equal authority.

Instead, implement the COMMON CONTRACT that allows every relationship-like
object to participate in one governed Lending intelligence experience while
preserving:

- source lane
- authority
- provenance
- quality
- review state
- lifecycle
- publication state
- evidence
- lineage

The resulting architecture should support the future user experience:

PORTFOLIO
    ↓
CLIENT / ENTITY
    ↓
RELATIONSHIP
    ↓
EVIDENCE
    ↓
WHY IT EXISTS
    ↓
WHAT SOURCE SUPPORTS IT
    ↓
WHAT THE SYSTEM DID WITH IT
    ↓
CURRENT TRUST / REVIEW STATE

==================================================
1. READ BEFORE MODIFYING
==================================================

Read and reconcile at minimum:

- LENDING_FOUNDATION_AUDIT.md

Backend modules identified by the audit for:

- Lending portfolio APIs
- V3 relationship projection
- V2 fallback
- normalized relationship database
- entity handling
- external research
- V3-aware external overlay
- AI relationship definitions / instances
- review queue
- relationship explorer
- network projection

Frontend files identified by the audit for:

- Portfolio Analytics
- Client Detail
- Network
- Relationship Explorer
- External Research
- Review Queue
- AI Create Relationship
- Lending workbench / intelligence views

Inspect existing database schemas before adding anything.

Reuse existing structures where possible.

Do not duplicate tables merely because names differ.

==================================================
2. DEFINE THE CANONICAL RELATIONSHIP CONTRACT
==================================================

Create one explicit backend contract representing a relationship exposed
to the Lending intelligence layer.

The contract must support at least:

relationship_id
stable_relationship_key if deterministically available

source_lane
source_system
authority_class

subject_entity_id
subject_cagid where applicable
subject_display_name

related_entity_id
related_cagid where applicable
related_display_name

relationship_type
relationship_family
relationship_label

direction
direction_basis

connectivity

state
state_basis

quality_status
review_status
publication_status

confidence
confidence_basis

evidence_count
source_count
independent_source_count

discovery_origin
discovery_basis

source_document_ids
evidence_ids
supporting_relationship_ids

exact_excerpt / representative_claim where contractually available

source_location
source_subject

amount
currency
percentage
materiality_context
only where supported

valid_from
valid_to
as_of_date
observed_at
created_at
updated_at
where available

entity_resolution_status

taxonomy_resolution_status

conflict_status

lineage_status

The contract must clearly distinguish:

FACTS PERSISTED FROM SOURCE

from

SYSTEM / AI INTERPRETATIONS

from

UI-DERIVED DISPLAY VALUES.

Do not silently convert one into another.

==================================================
3. SOURCE-LANE ENUMERATION
==================================================

Implement an explicit source-lane vocabulary.

At minimum support:

CAM_V3
V2_FALLBACK
NORMALIZED_CAM
EXTERNAL_RESEARCH
EXTERNAL_OVERLAY
AI_PUBLISHED

If actual existing implementation requires additional sublanes, preserve
them but map them into this common contract.

Every relationship returned to a unified reader must identify its lane.

==================================================
4. AUTHORITY MODEL
==================================================

Implement an explicit authority model.

CAM/V3 remains authoritative for the CAM relationship layer.

Do NOT allow:

- external findings
- AI-published relationships
- normalized workbench review actions

to silently rewrite the frozen CAM/V3 source artifact.

Represent authority explicitly.

Suggested semantics:

AUTHORITATIVE_CAM
GOVERNED_DERIVED
SUPPLEMENTAL_EXTERNAL
GOVERNED_AI
COMPATIBILITY_FALLBACK

Use the repository's existing semantics where stronger names already exist.

Do not invent false equivalence between sources.

==================================================
5. COMMON ENTITY ENDPOINT CONTRACT
==================================================

Relationships must use explicit endpoint identity.

Create/reuse a common endpoint structure that supports:

- internal entity ID where available
- CAGID where available
- legal/display name
- aliases if available
- entity-resolution status
- original extracted name
- canonical resolved name
- source of resolution

Do NOT require every related entity to have a CAGID.

External entities must remain representable.

Do NOT collapse distinct legal entities merely because names are similar.

Preserve unresolved endpoints explicitly.

==================================================
6. RELATIONSHIP IDENTITY
==================================================

Define and implement rules for:

A. source relationship identity
B. cross-source semantic identity
C. display grouping identity

These are NOT necessarily the same thing.

For example:

Lambda → NVIDIA / strategic_partner
Lambda → NVIDIA / supplier

must remain distinct relationship assertions even when they have the
same entity pair.

Likewise:

same pair + different direction
same pair + different state
same pair + different source
same pair + different type

must not be blindly deduplicated.

Document the deterministic key strategy.

==================================================
7. TAXONOMY PRESERVATION
==================================================

Do NOT collapse relationship semantics into broad generic families.

The audit demonstrated cases such as:

- supplier vs strategic partner
- guarantor vs backleverage financing
- customer vs internal affiliate
- parent vs M&A target

Implement:

relationship_type
relationship_family

as separate concepts.

Preserve the atomic semantic type.

Family exists for portfolio analysis and grouping.

Type exists for meaning.

Add explicit taxonomy mapping metadata when one representation is mapped
to another.

A mapped/substituted taxonomy must be visible as a substitution, not
presented as if it were the original extracted type.

==================================================
8. LINEAGE LEDGER
==================================================

This is CRITICAL.

Create/reuse a persisted lineage mechanism allowing the system to explain:

SOURCE OBSERVATION
    ↓
EVIDENCE
    ↓
CANDIDATE
    ↓
ENTITY RESOLUTION
    ↓
TAXONOMY RESOLUTION
    ↓
QUALITY / EVIDENCE GATE
    ↓
STATE / DIRECTION GATE
    ↓
DEDUP / RECONCILIATION
    ↓
SCOPE / PUBLICATION
    ↓
FINAL REPRESENTATION

Do not fabricate historical transitions that were never persisted.

For old records where the intermediate history does not exist, report:

LINEAGE_INCOMPLETE

or equivalent.

Do not infer a causal history merely from current-state tables.

New processing going forward must persist sufficient transition data.

Each transition should support, where applicable:

- event ID
- relationship/candidate ID
- previous representation
- resulting representation
- stage
- decision
- reason code
- rule/policy
- actor/process
- timestamp
- supporting evidence IDs
- source lane
- version

==================================================
9. REASON-CODE MODEL
==================================================

Preserve structured reasons.

Do not compress all failures into "rejected."

Support distinctions such as:

ENTITY_RESOLUTION
TAXONOMY_SUBSTITUTION
EVIDENCE_GATE
CONFIDENCE_GATE
STATE_DIRECTION
DEDUPLICATION
SCOPE_POLICY
API_PUBLICATION
MALFORMED_REPRESENTATION
INSUFFICIENT_EVIDENCE

Use existing repository reason codes where available.

Create a mapping layer rather than renaming historical data destructively.

==================================================
10. REVIEW STATE
==================================================

Do not pretend the application already has one universal Review Queue.

Create one common review-state contract capable of representing:

- CAM V3 review-required
- normalized workbench review
- external proposal review
- external conflict
- entity-match review
- insufficient-evidence review
- AI definition governance

But preserve the action semantics of each lane.

The common contract should allow the UI eventually to show:

WHY THIS NEEDS ATTENTION

without implying that every review item can be approved through the same
mutation endpoint.

==================================================
11. EXTERNAL RESEARCH CONTRACT
==================================================

Preserve external research as supplemental.

Its findings must expose:

- research run ID
- subject
- related entity
- relationship type
- channel
- source URL/reference
- source date
- evidence
- entity match state
- corroboration/proposal/conflict status
- confidence where legitimately available

External research must NEVER silently become a CAM fact.

It may:

CORROBORATE
PROPOSE
CONFLICT
SUPPLY ADDITIONAL EVIDENCE
RETURN INSUFFICIENT EVIDENCE

==================================================
12. AI RELATIONSHIP CONTRACT
==================================================

Preserve the existing:

DESCRIBE
→ CONFIGURE
→ DRAFT
→ PREVIEW
→ APPROVE
→ PUBLISH

governance lifecycle.

Published AI instances must use the common relationship contract for
read/display purposes.

But preserve:

source_lane = AI_PUBLISHED

and the definition/version that produced the instance.

Persist/expose:

AI definition ID
definition version
publication event
supporting relationship IDs
supporting evidence IDs
AI inference fields
deterministic rule fields

Never make an AI-published instance indistinguishable from CAM.

==================================================
13. UNIFIED READ MODEL
==================================================

Build a READ MODEL / SERVICE, not a destructive merge.

Create a backend service capable of returning relationships across
selected lanes through the common contract.

Example conceptual API:

GET /api/lending/intelligence/relationships

Filters should support at least:

subject/entity
related entity
CAGID
relationship type
relationship family
source lane
authority class
state
review status
quality status
connectivity
country/region where supported
sector where supported
minimum evidence
minimum confidence where meaningful
as-of date
publication state

Default behavior must be explicit and safe.

Do not silently include V2 noisy candidates.

Do not silently promote rejected normalized rows.

Do not silently include unpublished AI drafts.

Define the default trusted read.

==================================================
14. RELATIONSHIP DETAIL / EXPLAINABILITY API
==================================================

Create a relationship-detail API capable of powering a future:

"Why am I seeing this?"

panel.

For one relationship, return:

- canonical common-contract record
- endpoint identities
- source lane
- authority
- exact relationship semantic
- family
- direction
- state
- evidence summary
- source summary
- representative evidence
- review/quality state
- taxonomy mapping
- entity-resolution information
- conflict information
- lineage events
- supporting relationships
- supporting AI definition/version if applicable
- external corroboration/proposals if applicable

Do not require the frontend to reconstruct this explanation by joining
multiple unrelated APIs.

==================================================
15. DATA QUALITY / PROVENANCE FLAGS
==================================================

Expose explicit flags for incomplete information.

Examples:

identity_complete
taxonomy_complete
direction_complete
state_complete
evidence_complete
lineage_complete
source_location_complete

Do not fill unknown values with guesses.

UNKNOWN must remain a valid state.

==================================================
16. NO UI REDESIGN IN THIS PROMPT
==================================================

Do NOT perform the major new visual redesign yet.

Do not rebuild the map.

Do not add animation.

Do not build the executive AI assistant yet.

Do not redesign Overview.

Do not redesign Client Detail.

This prompt establishes the data contract required for those screens.

Minimal developer/debug surfaces are acceptable if needed for validation.

==================================================
17. MIGRATION SAFETY
==================================================

Before schema modification:

- inspect existing tables
- reuse tables where possible
- make migrations additive
- preserve current IDs
- preserve current V3 artifacts
- preserve normalized history
- preserve external research history
- preserve AI history

No destructive migrations.

No replacement of source artifacts.

Back up SQLite files before migration if any persistent SQLite schema is
modified.

==================================================
18. TESTS
==================================================

Add automated tests covering at minimum:

A. same entity pair, different relationship type remains distinct

B. same semantic relationship from multiple sources can be grouped without
losing source assertions

C. non-CAGID external endpoint remains valid

D. unresolved endpoint remains explicit

E. taxonomy substitution remains visible

F. CAM authority is not overwritten by external research

G. AI publication remains a separate source lane

H. review-required CAM rows remain visible according to the declared
trusted-read policy

I. normalized rejected rows are not silently promoted

J. V2 fallback remains conditional and does not become a global source

K. relationship-detail response contains source/evidence/explainability data

L. incomplete historical lineage is reported as incomplete rather than
invented

==================================================
19. BENCHMARK REGRESSION
==================================================

Use the previously established benchmark relationships as regression
fixtures where available, including examples involving:

- Lambda / NVIDIA
- Project Indigo / CoreWeave
- Applied Digital / CoreWeave
- Serverfarm / Meta
- BO Westover / Blue Owl
- OpenAI relationships
- Hut 8 relationships
- Cavalry / CyrusOne

Do NOT alter expected source facts merely to make tests pass.

The point is to verify representation.

==================================================
20. DELIVERABLE REPORT
==================================================

Create:

LENDING_CANONICAL_RELATIONSHIP_CONTRACT_REPORT.md

Report:

1. files changed
2. schemas/tables added or reused
3. migrations performed
4. common relationship contract
5. source-lane model
6. authority model
7. endpoint identity model
8. relationship identity/key model
9. taxonomy model
10. lineage model
11. reason-code model
12. review-state model
13. external contract
14. AI contract
15. unified read API
16. relationship explainability API
17. default trusted-read policy
18. test results
19. benchmark results
20. unresolved limitations
21. exact next implementation step

==================================================
21. ACCEPTANCE CRITERIA
==================================================

Prompt 3 is complete only when:

- Lending has one documented relationship contract
- all active relationship lanes can map into it
- authority remains explicit
- source lane remains explicit
- entity endpoints are explicit
- relationship semantics remain atomic
- taxonomy substitutions remain visible
- review semantics are not falsely collapsed
- external research remains supplemental
- AI remains separately governed
- a unified read service exists
- a relationship explainability/detail service exists
- new processing can persist lineage
- historical missing lineage is explicitly marked incomplete
- no CCR dependency was introduced
- no Customer_latest.parquet dependency exists
- tests pass
- existing Lending behavior is not silently broken

At the end, STOP.

Do not begin the portfolio UI redesign.
Do not begin the new network visualization.
Do not begin the AI executive assistant.
Do not begin automated SEC/web expansion.

Return the implementation report and wait for the next prompt.
