Yes — this is now much cleaner. Luna has successfully separated the Lending relationship-research contract from the RPR business contract.

The important results in your screenshot are all PASS:

RPR contract unchanged
Lending six-input adapter validated
Lending Runner routing uses the separate contract
Lending knowledge files contain no old RPR keys
Python compilation/diagnostics passed

And the six correct Lending inputs are now:

SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate
What to do in Stylus now

Because you uploaded the knowledge files before Luna corrected them, replace them. Safest approach: remove all five from the preset and upload the current five files again from lending_relationship_research_knowledge. That guarantees you aren't mixing old RPR-oriented knowledge with the corrected version.

Then click ADD FIELD six times and create exactly these fields, case-sensitive, in this order:

SubjectEntity
RelatedEntity
RelationshipScope
SourceChannels
ResearchInstruction
AsOfDate

Do not add the old CompanyConte, ScenarioCont, EventDrivenE, etc.

Then replace the Prompt box with the new PRESET PROMPT TO COPY INTO STYLUS from the updated:

04_EXAMPLES_GUARDRAILS_AND_RESEARCH_BEHAVIOR.md

That prompt should now reference only:

{{SubjectEntity}}
{{RelatedEntity}}
{{RelationshipScope}}
{{SourceChannels}}
{{ResearchInstruction}}
{{AsOfDate}}
Integrations

For this preset, enable:

☑ Web Search
☑ SEC filings

Leave the other integrations off for now.

What each field means

SubjectEntity is the Lending client you are researching, e.g. CoreWeave.

RelatedEntity is optional and is used for pair research, e.g. NVIDIA.

RelationshipScope tells it whether to search ALL relationships or only selected relationship types.

SourceChannels tells it to use R2D2_WEB, SEC_FILING, or both.

ResearchInstruction is the actual analyst question, e.g. “Determine all defensible relationships between CoreWeave and NVIDIA and cross-check the evidence.”

AsOfDate controls the evidence cutoff date.

For example, one run could effectively receive:

SubjectEntity:
CoreWeave, Inc.

RelatedEntity:
NVIDIA Corporation

RelationshipScope:
ALL

SourceChannels:
R2D2_WEB,SEC_FILING

ResearchInstruction:
Find and classify all defensible credit-relevant relationships
between the two entities. Cross-check the evidence and identify
whether each relationship is direct or indirect, current,
historical or emerging.

AsOfDate:
2026-09-19

This is now actually aligned with the Lending relationship use case.

One final point from Luna's output: the preset itself is still correctly reported as not configured, because only you can finish it manually in Stylus. Once you re-upload the corrected five files, add these six fields, paste the corrected prompt, and enable Web + SEC, then you can move to Preview and test one pair before we connect the live application.
