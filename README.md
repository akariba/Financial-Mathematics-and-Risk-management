SubjectEntity: COREWEAVE INC
RelatedEntity: NVIDIA CORP
RelationshipScope: technology_dependency,supplier
SourceChannels: R2D2_WEB,SEC_FILING
ResearchInstruction:
Validate whether CoreWeave has an explicit supplier and/or material technology dependency relationship with NVIDIA. Use only strong authoritative or high-quality sources. Return separate atomic findings for each supported relationship type. Do not infer from co-mention. Identify conflicts or insufficient evidence explicitly.

AsOfDate: your current analysis date.


FINAL ADMISSIBILITY GATE

Before returning each finding, perform a final evidence-object validation.

For every evidence[] item ask:

"Would this excerpt, standing on its own together with only immediately
adjacent unambiguous context, allow an analyst to identify BOTH the relevant
entities and the claimed relationship semantics?"

If NO:
REMOVE that evidence object.

Do not retain generic statements about:
- suppliers generally;
- advanced hardware generally;
- collaborations generally;
- strategic alliances generally;
- semiconductor supply chains generally;
- infrastructure expansion generally.

An evidence object must specifically substantiate the relationship_type
being returned.

A finding may remain HIGH only when at least one retained evidence object
directly and explicitly supports that relationship.

If removing weak evidence leaves no admissible evidence:
downgrade the finding to MEDIUM or INSUFFICIENT as appropriate.

CROSS-SOURCE CORROBORATION

Set cross_source_corroboration = true only when admissible evidence comes
from at least two genuinely independent underlying sources.

Different excerpts from the same SEC filing are NOT cross-source
corroboration.

Different SEC filings from the same registrant may provide multiple-document
support but do not constitute Web + SEC cross-channel corroboration.

If R2D2_WEB merely returns or summarizes SEC filing content and no independent
Web source is retained in evidence[]:
cross_source_corroboration = false.

Do not count a search summary as independent evidence.
