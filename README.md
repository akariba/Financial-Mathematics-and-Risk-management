SubjectEntity: COREWEAVE INC
RelatedEntity: NVIDIA CORP
RelationshipScope: technology_dependency,supplier
SourceChannels: R2D2_WEB,SEC_FILING
ResearchInstruction:
Validate whether CoreWeave has an explicit supplier and/or material technology dependency relationship with NVIDIA. Use only strong authoritative or high-quality sources. Return separate atomic findings for each supported relationship type. Do not infer from co-mention. Identify conflicts or insufficient evidence explicitly.

AsOfDate: your current analysis date.


FINAL EVIDENCE NORMALIZATION RULES

SOURCE CHANNEL MUST REPRESENT THE UNDERLYING SOURCE

source_channel describes the actual evidence source, not the tool used to retrieve it.

If R2D2_WEB discovers an SEC filing:
source_channel = SEC_FILING

Do not label an SEC 10-K, 10-Q, 8-K, S-1, proxy, exhibit, or other SEC filing
as R2D2_WEB merely because R2D2 retrieved it.

Do not duplicate the same filing once as SEC_FILING and again as R2D2_WEB.

R2D2_WEB should represent genuine non-SEC Web evidence such as:
- official company web disclosures
- Reuters
- Bloomberg
- Financial Times
- other permitted reputable Web sources.

EVIDENCE OBJECT ADMISSIBILITY

Every evidence object with evidence_role SUPPORTING or CORROBORATING must
itself materially support the specific relationship_type of that finding.

Do not include generic statements merely because they come from the correct
company or filing.

For example, generic statements about:
- advanced hardware
- future collaborations
- growth strategy
- infrastructure expansion
- market conditions

must NOT be used as SUPPORTING evidence for NVIDIA technology_dependency
unless the excerpt itself, together with immediately adjacent unambiguous
context, establishes the NVIDIA relationship.

For HIGH-confidence evidence, require:
- explicit entity identification or unambiguous immediate context;
- explicit relationship semantics;
- direct relevance to the claimed relationship_type.

If an excerpt does not independently satisfy this requirement:
exclude it from evidence[].

Do not keep weak excerpts merely to increase the number of sources.

Prefer the 1–3 strongest evidence objects rather than many weaker objects.

SEC REFERENCE QUALITY

For SEC evidence, use the most precise filing/document reference available.

If a precise filing accession/document reference or direct filing reference
cannot be established:
- do not invent one;
- use null or the precise reference actually available;
- do not assign HIGH source_quality solely on the basis of an imprecise
  generic EDGAR reference.
