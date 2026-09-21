SubjectEntity: COREWEAVE INC
RelatedEntity: NVIDIA CORP
RelationshipScope: technology_dependency,supplier
SourceChannels: R2D2_WEB,SEC_FILING
ResearchInstruction:
Validate whether CoreWeave has an explicit supplier and/or material technology dependency relationship with NVIDIA. Use only strong authoritative or high-quality sources. Return separate atomic findings for each supported relationship type. Do not infer from co-mention. Identify conflicts or insufficient evidence explicitly.

AsOfDate: your current analysis date.


RELATIONSHIP CONSOLIDATION AND PRECISION RULES

ONE SEMANTIC RELATIONSHIP PER FINDING

For the same:
- subject entity
- related entity
- relationship type
- direction

return ONE finding only.

Do NOT create separate relationship findings merely because the same
relationship was found through both SEC and Web.

Instead aggregate all supporting sources inside the finding's evidence[] array.

Example:

CoreWeave -> NVIDIA -> technology_dependency

If SEC and Web both support it:

findings count = 1
evidence count = 2 or more

Do not return one SEC finding and one Web finding for the same semantic
relationship.

SOURCE CHANNEL CLASSIFICATION

Classify evidence according to the actual underlying source.

If R2D2 Web retrieves an SEC filing, official regulatory filing, or company
filing, classify the evidence as SEC_FILING when the underlying evidence is
the filing itself.

Use R2D2_WEB for genuine Web/news/company-site evidence that is not being
treated as SEC filing evidence.

Do not duplicate the same filing under both source channels.

DIRECTION SEMANTICS

Direction must follow the actual relationship meaning.

Examples:

NVIDIA supplies CoreWeave:
NVIDIA -> CoreWeave
If SubjectEntity = CoreWeave and RelatedEntity = NVIDIA:
direction = B_TO_A

CoreWeave depends on NVIDIA technology:
CoreWeave -> NVIDIA
If SubjectEntity = CoreWeave and RelatedEntity = NVIDIA:
direction = A_TO_B

Do not automatically reuse the same direction across different
relationship types for the same entity pair.

EXACT EVIDENCE REQUIREMENT

For HIGH confidence, exact_excerpt must contain enough contiguous source
text to directly establish:
- the relevant entities, or an unambiguous entity reference established
  by immediately adjacent context;
- the relationship semantics;
- the claimed relationship type.

A generic sentence taken from the correct filing is not sufficient.

If the exact evidence cannot directly substantiate the claimed relationship:
downgrade to MEDIUM or INSUFFICIENT as appropriate.

SOURCE REFERENCE PRECISION

For SEC filings, provide the most precise available EDGAR filing/document
reference.

Do not treat a generic EDGAR search page, broad archive path, or approximate
reference as fully validated filing provenance.

If a precise filing reference cannot be established:
flag it in unresolved_items and do not assign HIGH source-quality solely
from that reference.
