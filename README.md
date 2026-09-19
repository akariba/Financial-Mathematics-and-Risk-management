The Stylus Preset Builder Configure screen is open.

IMPORTANT:
Stylus currently allows only a small number of uploaded knowledge files, so consolidate the relationship-research knowledge package into EXACTLY FIVE Markdown files.

Do NOT configure Stylus.
Do NOT create the preset.
Do NOT change application code unless required only to inspect the existing expected runtime schema.

FIRST inspect the current Lending implementation and return the EXACT runtime input field names expected by:
- the Runner adapter
- stylus_preset.py
- R2D2 Assist backend
- structured response parser

Do not invent input names.

Create these five files:

1. 00_LENDING_RESEARCH_READINESS_AND_POLICY.md

Must contain exactly:
relationship_research_ready: true

Also consolidate:
- CAM authority rule
- external evidence policy
- corroboration vs proposal
- conflict handling
- review governance
- no CAM overwrite
- mention-only exclusion

2. 01_LENDING_RELATIONSHIP_TAXONOMY.md

Consolidate the complete EXISTING Lending controlled taxonomy from the application.

For every supported relationship type include:
- relationship family
- definition
- inclusion criteria
- exclusion criteria
- directionality
- typical evidence language
- credit relevance

Do not invent a new taxonomy.

3. 02_EVIDENCE_CONFIDENCE_AND_MATERIALITY.md

Consolidate:
- source hierarchy
- R2D2 Web evidence rules
- SEC evidence rules
- exact excerpt requirements
- cross-checking rules
- confidence factors
- HIGH / MEDIUM / LOW / INSUFFICIENT
- credit materiality rules
- MATERIAL / POTENTIALLY_MATERIAL / CONTEXTUAL / UNKNOWN
- contradiction handling
- entity resolution rules

Make it explicit that confidence and materiality are separate.

4. 03_STRUCTURED_OUTPUT_AND_RUNTIME_INPUTS.md

THIS FILE MUST MATCH THE CURRENT CODE EXACTLY.

Document:
- exact structured output schema expected by the Lending backend
- exact enum/value names
- exact runtime input keys expected by the preset
- which are required vs optional
- example value for each
- which are supplied by the application

Do NOT invent fields.

At the top include a clearly visible section:

EXACT RUNTIME INPUT KEYS

and list them in order.

5. 04_EXAMPLES_GUARDRAILS_AND_RESEARCH_BEHAVIOR.md

Consolidate examples for:
- CAM corroboration
- new external proposal
- SEC corroboration
- Web corroboration
- conflict
- mention-only
- direct relationship
- indirect relationship
- current
- historical
- emerging

Also include strict guardrails:
- no fabricated sources
- no fabricated excerpts
- no pretrained-model knowledge used as evidence
- no co-mention classified as relationship
- no ambiguous entity merge
- no automatic CAM mutation
- no automatic validation of external proposals
- no unsupported SEC claim

Include the complete recommended production preset instruction at the bottom under:

PRESET PROMPT TO COPY INTO STYLUS

The prompt must be ready for me to copy/paste directly into the Stylus Prompt field and must reference the exact runtime input fields expected by the existing application.

Also inspect the proven RPR preset configuration and report:

- recommended model
- required tools/integrations
- whether Web is required
- whether SEC filing integration is required
- any other required integration

Do NOT use placeholders such as TODO.
Do NOT leave pending knowledge.
Do NOT run R2D2.

Final response must contain only:

1. Folder path
2. Five filenames created
3. Exact runtime input keys, in order
4. Exact prompt text location/file
5. Recommended model from proven RPR setup
6. Required tools/integrations
7. Knowledge readiness PASS/FAIL

STOP.
