You now have the current working Step-1 HTML/frontend, the relevant Python backend files, and the three approved enhancement prompts.

Your task is to IMPLEMENT the enhancement feature end-to-end against the REAL uploaded codebase.

Do not produce another design document. Do not only explain what should change. MODIFY/CREATE THE ACTUAL FILES and make every resulting file downloadable.

## Objective

Implement this workflow for BOTH Trigger 1 Market Scanner and Trigger 2 User Narrative:

**Existing run → analyse result quality → if a concrete fixable weakness exists, recommend enhancement → show recommendation to user → user may accept/edit/reject → consolidate approved feedback → rescan/re-enrich → display improved result.**

The feature must GUIDE the user. It must NEVER silently rewrite the master production prompt and must NEVER automatically start a rescan.

---

## 1. Preserve the existing application

Use the uploaded Step-1 HTML as the authoritative UI.

Preserve:

* current Citi/RPR layout and styling
* Trigger 1 / Trigger 2 tabs
* existing event and 8-section displays
* existing inline editing
* existing Confirm functionality
* existing feedback area/icon at the bottom
* existing backend calls wherever possible

Do NOT redesign Step 1.

Add the enhancement capability naturally around the existing feedback area.

---

## 2. Use the THREE approved prompts exactly

Use the uploaded approved prompt files as runtime prompts:

1. `trigger1_market_scanner`
2. `enhancement_diagnosis`
3. `feedback_consolidation`

Do not rewrite their business logic.

If the current backend stores a production prompt in Python, such as `R2D2_PROMPT` in `r2d2_prompt.py`, integrate appropriately rather than pretending it is loaded from a `.txt` file.

---

## 3. Trigger 1 integration

Use the real existing implementation in `market_event_scout.py`.

Existing flow includes:

* `MarketEventScout.fetch_events()`
* `MarketEventScout.refine_event()`
* `_build_query()`
* `MarketEventParser`

Modify it minimally so the application can retain enough execution metadata for enhancement diagnosis.

Capture, where available:

* theme
* event id
* generated search query
* queries actually executed
* retrieval outcome
* resulting 8 sections
* missing/limited evidence indicators

Do NOT invent UUID IDs if the real implementation uses integer event IDs.

Use the real IDs/types used by the backend.

`MarketEventScout.refine_event()` should remain the Trigger-1 rescan/refinement hook unless the actual uploaded code proves another path is correct.

---

## 4. Trigger 2 integration

Determine from the uploaded code which Trigger-2 path the Step-1 application ACTUALLY calls:

* `narrative_enricher.enrich_narrative()`
  or
* `RPRService.enrich_narrative()`

Trace the real route/call chain.

Integrate the enhancement feature into the ACTIVE path.

Do not maintain two unnecessary implementations.

Trigger 2 must retain:

* original user narrative
* generated 8 sections
* retrieval/search result where applicable
* evidence/retrieval quality information required by enhancement diagnosis.

---

## 5. Evidence and retrieval metadata

The enhancement diagnosis requires evidence quality and retrieval status.

Implement these as structured backend metadata rather than merely decorative text where practical.

For every report section expose enough information to distinguish:

* evidence sufficient
* evidence limited
* no relevant evidence found
* retrieval/search failed technically
* retrieval not assessed

Do not incorrectly treat a technical retrieval failure as “no evidence exists.”

Do not fabricate evidence.

If the approved prompt requires textual tags such as:

`[EVIDENCE_TIER: ...]`
`[RETRIEVAL_STATUS: ...]`

support them consistently, while also keeping structured values in the backend where appropriate.

---

## 6. Enhancement diagnosis

After a Trigger-1 or Trigger-2 result has been produced, run the approved `enhancement_diagnosis` prompt.

Pass it the actual report/result and the available retrieval/evidence metadata.

Expected behaviour:

### NOT_RECOMMENDED

If there is no concrete, fixable search/report weakness:

* do not bother the user with unnecessary suggestions
* keep the normal existing feedback experience.

### RECOMMENDED

If a concrete improvement opportunity exists:
show an enhancement suggestion near/in the existing feedback panel.

Display:

* concise diagnosis/reason
* suggested feedback/instruction
* affected section if available

The user must have explicit choices:

* Apply / use suggestion
* Edit suggestion
* Dismiss

Nothing should auto-submit.

---

## 7. Feedback consolidation

When the user accepts or edits the recommendation:

Run the approved `feedback_consolidation` prompt.

Its purpose is to combine:

* original intent
* diagnosed weakness
* user-approved/edited feedback

into a precise refinement instruction.

Do not introduce a new search idea that the user did not approve.

---

## 8. Rescan / re-enrichment

Only after explicit user action:

### Trigger 1

use the existing Trigger-1 refinement/rescan mechanism, preferably:
`MarketEventScout.refine_event(...)`

### Trigger 2

rerun the active Trigger-2 enrichment path with the approved consolidated refinement.

Do not permanently alter the base/master production prompts.

This is per-run runtime guidance.

Show the new result in the SAME existing Step-1 UI.

---

## 9. UI behaviour

Integrate this with the feedback area already present at the bottom of the uploaded main/Step-1 HTML.

When enhancement is recommended, show a compact card such as:

**Potential improvement detected**

Reason:
[short diagnosis]

Suggested refinement:
[editable text]

Buttons:
`Apply & Rescan`
`Edit`
`Dismiss`

Follow the existing Citi visual language.

Do not create a separate page or modal unless technically required.

Do not auto-populate and immediately submit the existing feedback control.

The user remains in control.

---

## 10. State / repeated recommendations

Prevent the application from repeatedly recommending exactly the same enhancement for the same event/narrative during the same Step-1 session.

A lightweight frontend/backend session mechanism is acceptable.

Do not create unnecessary database infrastructure.

---

## 11. Fix obvious integration risks while implementing

Where relevant to the uploaded code:

* Do not pass literal `"None"` to Claude as if it were valid retrieved web evidence.
* Distinguish retrieval failure from empty evidence.
* Add sensible AI-call timeout/error handling if it can be done without changing infrastructure.
* Preserve existing retry behaviour.
* Do not break current static/demo mode unnecessarily.
* Avoid large architectural rewrites.
* Avoid adding unnecessary dependencies.

---

## 12. API / frontend integration

Trace the current Step-1 HTML JavaScript calls.

Implement the smallest set of backend endpoints/functions needed for:

1. run enhancement diagnosis
2. submit accepted/edited enhancement
3. perform refinement/rescan
4. return updated report

If route/server files are uploaded, modify those actual files.

If a required route file is genuinely absent:

* create the smallest clearly named integration file needed,
* clearly identify exactly where it must be registered,
* do NOT fabricate modifications to an unseen file.

---

## 13. Deliverables — IMPORTANT

I want actual usable files, not snippets.

For EVERY file that must change:

* generate the COMPLETE final file
* retain all existing unrelated functionality
* make the file individually downloadable

For every new file:

* generate its complete contents
* make it individually downloadable

Also create:

`IMPLEMENTATION_SUMMARY.md`

containing only:

* files changed
* files added
* what each change does
* any genuinely unresolved integration dependency
* exact run/test command

Also create:

`rpr_step1_enhancement_complete.zip`

containing ALL changed/new files in the correct directory structure.

---

## 14. Validate before delivering

Before presenting the files:

* syntax-check Python
* check JavaScript for obvious syntax errors
* verify imports
* verify filenames/functions against the uploaded source
* verify frontend callback/API names match backend
* verify both Trigger 1 and Trigger 2 paths
* verify NOT_RECOMMENDED behaviour
* verify RECOMMENDED → edit/accept → consolidation → rescan behaviour
* verify Dismiss performs no rescan
* verify no action automatically modifies a master prompt
* run available tests
* add focused tests for the new workflow where possible

Do not claim something was tested if it could not actually be tested.

---

## 15. Final response

Do NOT respond with another long architecture analysis.

Your final response should contain:

1. a very short implementation status
2. downloadable links/cards for every modified/new file
3. the downloadable ZIP
4. test results
5. only genuinely unresolved blockers, if any

Start implementation now using the uploaded files as the source of truth.
