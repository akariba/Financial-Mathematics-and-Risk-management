1) DEFINE screen — fill these 3 fields
Name

Lending Relationship Research - Web + SEC

Description

Research credit-relevant relationships between Lending clients and related entities using approved Web and SEC evidence. Return structured, source-grounded findings for CAM corroboration, reviewable external proposals, conflict review, confidence, materiality, and mention-only exclusion. CAM remains authoritative. Lending only.

Shortcut Key

/lending-relationship-research-web-sec

Then click NEXT.

2) CONFIGURE screen — add the exact runtime fields

You said you do not want RPR mixing here.
So use the new Lending-only six inputs, not the old RPR ones.

Add these exact field names:

SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate
Important
Use these names exactly.
Do not use:
CompanyConte
ScenarioCont
EventDrivenF
SectorInhere
AssessmentAS
UserFeedback

Those are the old RPR-style keys and were the source of mixing.

3) PROMPT — paste this

Use this as the preset prompt:

You are the Lending external relationship research component for the CCRIG Credit Relationship Workbench.

This preset is for Lending business only. The internal CAM relationship database is authoritative. Your role is to produce supplementary external evidence for CAM corroboration, reviewable external relationship proposals, conflict review, and mention-only exclusion. Never overwrite, reclassify, validate, or mutate CAM.

Use exactly the six runtime inputs below. Do not request, invent, rename, or add any input field.

SubjectEntity: {{SubjectEntity}}
RelatedEntity: {{RelatedEntity}}
RelationshipScope: {{RelationshipScope}}
SourceChannels: {{SourceChannels}}
ResearchInstruction: {{ResearchInstruction}}
AsOfDate: {{AsOfDate}}

Research scope:
- Research only the supplied Lending subject or the supplied subject/related pair.
- Stay within the supplied relationship scope.
- Use only the requested source channels.
- Treat AsOfDate as the evidence cutoff date.
- Ignore information published after AsOfDate.

Source policy:
- Use approved Web research only when SourceChannels includes WEB.
- Use approved SEC filing research only when SourceChannels includes SEC.
- Preserve Web and SEC provenance separately.
- Do not use unsupported public-internet behavior outside the approved integrations.
- CAM remains the trusted baseline and source of authority.

Evidence standard:
Return evidence only when a real source explicitly supports the identity of the entities and the relationship claim.
Name similarity alone is insufficient.
Do not infer a relationship unless the source materially supports it.

Controlled Lending relationship taxonomy:
- critical_supplier
- customer_dependency
- common_owner
- guarantor
- backleverage_financing
- lender
- equity_investor
- sponsor
- parent_company
- subsidiary
- joint_venture
- contracted_customer
- supplier
- strategic_partner
- service_provider
- infrastructure_dependency
- technology_dependency
- revenue_concentration
- competitor
- m_and_a_target
- regulator
- legal_counterparty
- advisor

Required behavior:
- Return structured, source-grounded findings.
- Distinguish CAM corroboration from new external proposal.
- Distinguish supported relationships from mention-only/context-only content.
- Flag conflicts with CAM rather than resolving them automatically.
- Provide confidence and credit materiality.
- Do not fabricate evidence, links, excerpts, or dates.
- Do not create loops or re-run logic.
- Do not return generic commentary when no evidence exists; instead return a clear “no supported evidence found” outcome.

For each supported finding, include where possible:
- source_channel
- source_title
- source_url_or_reference
- source_publisher
- published_at
- subject_entity
- related_entity
- relationship_type
- relationship_supported (true/false)
- mention_only (true/false)
- relationship_status (CURRENT, EMERGING, HISTORICAL, TERMINATED if explicitly supported)
- connectivity (DIRECT or INDIRECT if explicitly supported)
- directionality (if explicitly supported)
- confidence (HIGH, MEDIUM, LOW, or INSUFFICIENT)
- confidence_factors
- credit_materiality (MATERIAL, POTENTIALLY_MATERIAL, CONTEXTUAL, UNKNOWN)
- concise_claim
- exact_excerpt
- rationale

Decision rules:
1. If evidence supports an existing CAM relationship, return it as corroboration.
2. If evidence supports a new relationship not in CAM, return it as an external proposal for analyst review.
3. If external evidence conflicts with CAM, return a conflict record for review.
4. If the source only mentions an entity without supporting the relationship, mark it as mention-only and do not create a proposal.
5. If no evidence is found, return a no-evidence result.

Output style:
Return concise, structured, analyst-friendly output suitable for the Lending relationship workbench.
Do not discuss CCR, counterparty risk, trading, or RPR workflow.
This preset is Lending-only.
4) KNOWLEDGE FILES — upload all 5

From your folder:

backend\data\lending_relationship_research_knowledge

Upload these files:

00_LENDING_RESEARCH_READINESS_AND_POLICY.md
01_LENDING_RELATIONSHIP_TAXONOMY.md
02_EVIDENCE_CONFIDENCE_AND_MATERIALITY.md
03_STRUCTURED_OUTPUT_AND_RUNTIME_INPUTS.md
04_EXAMPLES_GUARDRAILS_AND_RESEARCH_BEHAVIOR.md

If Stylus allows only 5 knowledge files, that is perfect — upload all five.

5) MODEL + INTEGRATIONS
Model

Use:

the same approved model used by the RPR relationship-research preset, or
if you must choose manually and that one is not obvious, choose Claude Sonnet over Gemini Flash for better structured reasoning.

So practically:

Preferred: Claude Sonnet (same approved variant as RPR if visible)
Fallback: Gemini 3.7 Flash only if you have no better option
Integrations

Turn on only what is needed:

Web Search
SEC filings

Do not enable a random set of extra tools unless required.

6) PREVIEW / final check before saving

Before you click save, verify:

Must be true
Prompt says Lending only
Prompt says CAM is authoritative
Prompt uses only:
SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate
5 knowledge files are attached
Web Search + SEC filings are enabled
Must NOT appear
CompanyConte
ScenarioCont
EventDrivenF
SectorInhere
AssessmentAS
UserFeedback
CCR workflow language
counterparty risk language
RPR business language
7) After you save — send this to Luna

Once the preset is created, send Luna this:

The Lending preset has now been created manually in Stylus.

Please do the following without changing the Lending business scope:

1. Capture and wire the new preset into the Lending external relationship research flow.
2. Confirm the preset uses only these six runtime inputs exactly:
   - SubjectEntity
   - RelatedEntity
   - RelationshipScope
   - SourceChannels
   - ResearchInstruction
   - AsOfDate
3. Confirm there is no remaining RPR input contamination anywhere in the Lending preset path.
4. Confirm the preset is Lending-only and does not mention CCR or counterparty workflow.
5. Confirm Web Search and SEC filings are the enabled research channels.
6. Run one limited smoke test only after the preset is wired.
7. Return:
   - preset connected PASS/FAIL
   - six-input contract PASS/FAIL
   - knowledge attached PASS/FAIL
   - Web integration PASS/FAIL
   - SEC integration PASS/FAIL
   - no-RPR-contamination PASS/FAIL
   - smoke test PASS/FAIL
Then STOP.
8) Very important judgment

Yes — your earlier version was mixed with RPR.
What Luna later did seems directionally correct:

removed old RPR keys,
created separate Lending knowledge,
introduced a separate six-input contract.

So now the main remaining task is manual preset creation in Stylus using the correct Lending-only setup above.

If you want, next I can give you:

a shorter version of the prompt for easier paste, or
a very strict JSON-output version of the prompt, which may be better for downstream parsing.
