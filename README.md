The Lending Relationship Research preset is now created manually in Stylus.

Do not recreate or modify the preset business prompt in code.

Wire the Lending application to the preset and use exactly these six runtime inputs:

1. SubjectEntity
2. RelatedEntity
3. RelationshipScope
4. SourceChannels
5. ResearchInstruction
6. AsOfDate

Requirements:

- Lending only.
- Preserve the RPR path unchanged.
- Use the existing RPR-compatible Runner/authentication pattern only for transport.
- Do not reuse RPR business inputs or RPR business logic.
- Send the six Lending inputs to the Lending preset.
- Parse the returned strict JSON contract.
- Preserve Web and SEC provenance separately.
- CAM remains authoritative.
- External findings may only become corroboration, proposal, conflict, mention-only, or no-evidence outcomes.
- Never mutate CAM automatically.
- Persist external evidence separately from the internal CAM baseline.
- Fail closed if the preset output is malformed or incomplete.
- No loops or automatic reruns.
- Run one bounded smoke test after wiring is complete.

Return only:
- preset connection PASS/FAIL
- six-input contract PASS/FAIL
- Runner/auth PASS/FAIL
- Web channel PASS/FAIL
- SEC channel PASS/FAIL
- JSON parsing PASS/FAIL
- CAM baseline unchanged PASS/FAIL
- smoke test PASS/FAIL

Then STOP.
