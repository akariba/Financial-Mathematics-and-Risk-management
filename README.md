Continue the Lending relationship solution from the now-working R2D2 Web + SEC integration.

LENDING ONLY.

Do not modify:
- the frozen CAM/internal Lending baseline;
- the manually created Stylus preset;
- the six-input preset contract;
- the RPR implementation.

GOAL

Turn the working external research integration into a practical analyst workflow.

Implement the following:

1. ON-DEMAND RESEARCH ONLY
R2D2 research must run only after an explicit analyst action.
Never run automatically on:
- page load;
- entity selection;
- graph click;
- reconnect;
- refresh.

2. RESEARCH MODES

Provide:
- Web Research — R2D2_WEB only
- Deep Validation — R2D2_WEB + SEC_FILING

Default to Web Research.

SEC must not run unless explicitly selected by the analyst.

3. CACHE RESULTS

Persist successful research results.

Before calling Runner, check whether the same research already exists for:

- SubjectEntity
- RelatedEntity
- RelationshipScope
- SourceChannels
- AsOfDate

If a valid completed result exists, load it immediately instead of executing R2D2 again.

Provide an explicit “Refresh research” action if the analyst wants a new run.

Never silently refresh cached evidence.

4. RECONCILIATION

For every external finding:

- resolve the related entity locally;
- compare entity pair + relationship_type with CAM;
- exact CAM match → CAM_CORROBORATION;
- new supported relationship → EXTERNAL_PROPOSAL_PENDING_REVIEW;
- explicit contradiction → CONFLICT_REVIEW_REQUIRED;
- mention without relationship support → MENTION_ONLY.

CAM remains unchanged.

5. ANALYST REVIEW

External proposals must have review states:

PENDING_REVIEW
APPROVED_EXTERNAL
REJECTED
CONFLICT_REVIEW_REQUIRED

Approval must NOT modify the frozen CAM database.

Approved external relationships remain a separate reviewed external layer.

6. UI

For the selected Lending client show a compact External Research panel with:

- Research Web
- Deep Validation (Web + SEC)
- last researched timestamp
- cached/live indicator
- research status
- number of corroborations
- number of new proposals
- conflicts
- mention-only findings

For each finding show:

relationship type
related entity
confidence
credit materiality
Web / SEC source badges
exact source excerpt
source link/reference
review state

7. GRAPH

CAM relationships remain the trusted graph.

Reviewed external proposals may be shown as a visually distinct overlay.

Pending proposals must never look identical to CAM-confirmed relationships.

8. PERFORMANCE / SAFETY

- no automatic reruns;
- no loops;
- no polling loops;
- bounded Runner timeout;
- failed/partial Runner responses must not be persisted as successful research;
- preserve Web and SEC evidence separately;
- do not rerun an identical completed request unless Refresh research is explicitly selected.

Do not redesign unrelated parts of the Lending application.

TEST ONCE

Use CoreWeave ↔ NVIDIA.

Verify:
1. first Web research can execute live;
2. repeating the identical request returns cached results without Runner execution;
3. Deep Validation can separately invoke Web + SEC;
4. findings reconcile against CAM correctly;
5. external proposals remain separate from CAM;
6. CAM baseline hash/count remains unchanged.

Return only:

- on-demand execution PASS/FAIL
- Web-only mode PASS/FAIL
- Web+SEC mode PASS/FAIL
- caching PASS/FAIL
- CAM reconciliation PASS/FAIL
- review workflow PASS/FAIL
- external graph overlay PASS/FAIL
- CAM baseline unchanged PASS/FAIL

Then STOP.
