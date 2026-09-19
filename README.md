STOP the current preset-input approach.

You have reused RPR BUSINESS INPUTS in the Lending relationship-research preset.

That is incorrect.

RPR is a different use case.

We reuse ONLY the proven RPR technical integration pattern:

- browser/Runner authentication
- token handling
- POST /runner-service/chat
- full preset definition inline
- SSE streaming
- bounded completion handling
- structured artifact parsing
- error handling

We MUST NOT reuse:

- RPR business prompt
- RPR scenario inputs
- EventDriven inputs
- SectorInherent inputs
- Step 2 / portfolio-review semantics
- RPR assessment schema

==================================================
NEW LENDING RELATIONSHIP PRESET INPUT CONTRACT
==================================================

Replace the inherited RPR six-input schema with a relationship-specific schema.

Use exactly these six case-sensitive preset inputs:

1. SubjectEntity
2. RelatedEntity
3. RelationshipScope
4. SourceChannels
5. ResearchInstruction
6. AsOfDate

Definitions:

SubjectEntity
Required.
The principal Lending client/entity being researched.
The application may serialize name, CAGID, internal entity ID and known aliases into this text field.

RelatedEntity
Optional.
A second entity when performing pair research.
Example:
NVIDIA Corporation
If omitted, research may discover relationships around SubjectEntity.

RelationshipScope
Required.
Defines which relationship types to research.

Allowed conceptual values:
ALL
or selected controlled Lending relationship type IDs.

Do not introduce RPR scenario types.

SourceChannels
Required.

Allowed:
R2D2_WEB
SEC_FILING
R2D2_WEB,SEC_FILING

ResearchInstruction
Required.

The analyst/application instruction describing the research objective.

Examples:

"Find all defensible credit-relevant relationships involving the subject."

"Determine the relationship between CoreWeave and NVIDIA."

"Research whether NVIDIA is a critical supplier or technology dependency."

AsOfDate
Required.

Evidence cutoff date in ISO format:
YYYY-MM-DD

==================================================
APPLICATION ADAPTER
==================================================

Update the Lending R2D2 adapter so it supplies these six relationship-specific inputs.

Do NOT force Lending data into the old RPR keys.

The existing RPR project must remain unchanged.

If stylus_preset.py currently validates the old RPR keys globally, separate the contracts cleanly:

RPR preset contract:
existing RPR inputs remain untouched

Lending relationship preset contract:
the six new inputs above

Do not create one shared business-input schema.

Reuse shared Runner/auth/streaming infrastructure only.

==================================================
KNOWLEDGE FILE CORRECTION
==================================================

Update:

03_STRUCTURED_OUTPUT_AND_RUNTIME_INPUTS.md

Replace the old RPR runtime keys entirely with:

SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate

Update:

04_EXAMPLES_GUARDRAILS_AND_RESEARCH_BEHAVIOR.md

Remove all references to:

CompanyConte
ScenarioCont
EventDrivenE
SectorInhere
AssessmentAS
UserFeedback

Remove any explanation that these are "compatibility inputs."

Rewrite PRESET PROMPT TO COPY INTO STYLUS so it uses ONLY the six Lending relationship inputs.

==================================================
PRESET PROMPT INTENT
==================================================

The new prompt should begin conceptually:

"You are the Lending external relationship research component for the Credit Relationship Workbench.

CAM/internal approved Lending evidence is authoritative.

Research the supplied SubjectEntity and optional RelatedEntity using only the requested SourceChannels.

Classify defensible relationships using the controlled Lending relationship taxonomy.

External evidence may corroborate CAM, identify a new reviewable relationship, identify a conflict, or result in insufficient evidence.

Never overwrite CAM."

Then reference:

{{SubjectEntity}}
{{RelatedEntity}}
{{RelationshipScope}}
{{SourceChannels}}
{{ResearchInstruction}}
{{AsOfDate}}

==================================================
IMPORTANT BUSINESS BEHAVIOR
==================================================

The preset must support BOTH:

PAIR RESEARCH

Example:
NVIDIA ↔ Anthropic

and:

ENTITY DISCOVERY

Example:
Find important relationships around CoreWeave.

It must support:

- direct relationships
- indirect relationships
- current
- emerging
- historical
- terminated where explicitly evidenced
- corroboration
- new relationship proposals
- conflicts
- mention-only exclusion
- exact source/excerpt/date
- confidence factors
- credit materiality

Do not introduce portfolio-review scenario analysis.

==================================================
DO NOT CHANGE
==================================================

Do not change:

- CAM internal baseline
- 767 validated relationships
- RPR project
- existing RPR preset contract
- external evidence governance
- review workflow

==================================================
VALIDATE ONCE
==================================================

After correcting:

1. Verify Lending code no longer references the six RPR business input keys.
2. Verify the new Lending adapter uses exactly the six relationship inputs.
3. Verify knowledge files contain exactly the same six inputs.
4. Verify preset prompt contains exactly the same six placeholders.
5. Verify RPR remains unchanged.
6. Do not run the live preset yet.

Report only:

- old keys removed
- new six keys
- files changed
- RPR unchanged PASS/FAIL
- Lending preset contract PASS/FAIL

Then STOP.
