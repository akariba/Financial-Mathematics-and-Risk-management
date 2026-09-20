SubjectEntity: CoreWeave
RelatedEntity: NVIDIA
RelationshipScope: ALL
SourceChannels: R2D2_WEB,SEC_FILING
ResearchInstruction: Find explicit credit-relevant relationships between the two entities.
AsOfDate: 2026-09-20


The manually created Lending Stylus preset is now producing a successful live JSON artifact.

Do not modify the preset.

Wire the Lending application to consume this exact returned JSON.

After parsing each finding:

1. Resolve SubjectEntity and RelatedEntity against the existing Lending/CAM entity database using exact canonical name, aliases and CAGID where available.

2. Compare the returned entity pair + relationship_type against the validated CAM relationships.

3. If exact pair/type exists in CAM:
   classify as CAM_CORROBORATION and attach the external Web/SEC evidence to that CAM relationship without modifying CAM.

4. If the pair/type does not exist:
   keep it as EXTERNAL_PROPOSAL_PENDING_REVIEW.

5. If external evidence explicitly contradicts CAM:
   classify as CONFLICT_REVIEW_REQUIRED.

6. Preserve Web and SEC evidence separately.

7. Never modify, replace, reclassify or delete CAM records.

8. Do not require Stylus to provide internal CAGIDs or entity IDs. Resolve those locally after the response.

Run ONE bounded live test using the existing CoreWeave ↔ NVIDIA case.

Return only:

- preset JSON parse PASS/FAIL
- entity resolution PASS/FAIL
- CAM reconciliation PASS/FAIL
- Web evidence persistence PASS/FAIL
- SEC evidence persistence PASS/FAIL
- CAM baseline unchanged PASS/FAIL
- end-to-end Lending test PASS/FAIL

Then STOP.
