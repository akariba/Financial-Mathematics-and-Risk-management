You do not have access to the internal RPR repository and cannot modify or inspect the real application. Do not claim that you searched internal files, found endpoints or completed the integration.

Using the three attached approved documents, generate a self-contained, integration-ready implementation package that an internal developer or coding agent can later connect to the real application.

Attached documents:

1. `trigger1_market_scanner_prompt_final.docx`
2. `enhancement_diagnosis_prompt_final.docx`
3. `feedback_consolidation_prompt_final.docx`

## Objective

Create modular code and runtime prompt files for the AI-assisted search-enhancement workflow.

The package must:

* Support Trigger 1 immediately.
* Support Trigger 2 at the shared backend/UI level.
* Not invent the missing Trigger 2 report-generator prompt.
* Clearly identify where the real Trigger 2 prompt must later be connected.
* Never pretend that internal endpoints or repository files already exist.
* Avoid large schemas and unnecessary architecture.

## Generate this package

```text
rpr_enhancement_package/
├── README_INTEGRATION.md
├── prompts/
│   ├── trigger1_market_scanner.txt
│   ├── enhancement_diagnosis.txt
│   └── feedback_consolidation.txt
├── backend/
│   └── rpr_enhancement.py
├── frontend/
│   ├── rpr-enhancement-card.js
│   ├── rpr-enhancement-card.css
│   └── rpr-enhancement-demo.html
├── tests/
│   └── test_rpr_enhancement.py
└── TRIGGER2_INTEGRATION.md
```

Return the individual files and one ZIP archive containing the complete package.

## Runtime prompt files

Extract the approved prompt text faithfully from the three attached Word documents.

Do not simplify, rewrite or reinterpret the approved wording.

Create:

* `trigger1_market_scanner.txt`
* `enhancement_diagnosis.txt`
* `feedback_consolidation.txt`

The application must load plain-text prompt files at runtime. Do not load `.docx` files in production.

Do not create `trigger2_narrative_scanner.txt`, because the actual Trigger 2 source was not provided.

## Backend module

Create a framework-neutral Python 3.11 module named:

```text
backend/rpr_enhancement.py
```

Use the standard library only. Do not require Flask, FastAPI, Django or an external LLM library.

Implement:

### Enums

```text
EvidenceTier:
SUFFICIENT
LIMITED
NONE
NOT_ASSESSED

RetrievalStatus:
SUCCESS
PARTIAL_TECHNICAL_FAILURE
TECHNICAL_FAILURE

EnhancementDecision:
RECOMMENDED
NOT_RECOMMENDED
```

### Data structures

Create typed dataclasses for:

* Scope information.
* Section result.
* Diagnosis request.
* Diagnosis response.
* User-approved feedback item.
* Consolidation request.

Scope must support:

```text
scope_type: trigger1 | trigger2
theme_id
theme_name
event_id
event_name
narrative_segment_id
narrative_segment_name
```

IDs must be supplied by the host application. The AI must never generate them.

### Required functions

Implement clearly documented functions equivalent to:

```python
should_run_diagnosis(...)
build_diagnosis_payload(...)
validate_diagnosis_response(...)
should_display_card(...)
register_attempted_refinement(...)
has_refinement_been_attempted(...)
can_offer_another_refinement(...)
build_consolidation_payload(...)
format_copyable_feedback(...)
```

Required rules:

* Do not run diagnosis for `SUFFICIENT`.
* Do not recommend enhancement for technical failure.
* Do not treat technical failure as `NONE`.
* Require a real executed-query log.
* Return no recommendation when the query log is absent.
* Allow at most one recommendation per completed scope.
* Prevent an identical refinement from being proposed twice.
* Maximum two enhancement-assisted rescans per scope.
* Keep Trigger 1 and Trigger 2 feedback allocated separately.
* Nothing automatically submits feedback or initiates a rescan.

Do not implement a real LLM call. Define a small callable/protocol boundary where the internal application can connect its approved AI client.

Do not hardcode or invent internal API endpoints.

## Frontend component

Create a standalone, dependency-free HTML/CSS/JavaScript implementation.

The JavaScript component must be reusable inside an existing page and must not assume React, Angular or another framework.

Use scoped class names beginning with:

```text
rpr-enhancement-
```

Do not modify global HTML element styles.

Use CSS variables so the internal application can map its design tokens. Default appearance should follow:

* Dark navy headings.
* Existing blue workflow accent.
* White content cards.
* Restrained amber suggestion state.
* Professional banking/risk-tool appearance.

The component must display:

* “AI Suggested Search Enhancement”.
* Affected section or sections.
* Concise “Why” diagnosis.
* Editable suggested enhancement.
* Accept/Use Suggestion action.
* Modify action.
* Dismiss action.
* Final-feedback preview.
* Copy button.

Required behaviour:

1. The host application supplies a diagnosis response.
2. No card is rendered for `NOT_RECOMMENDED`.
3. One card is rendered for `RECOMMENDED`.
4. The user may accept, edit or dismiss.
5. Accepted/edited items can be consolidated.
6. Final feedback is displayed for copying.
7. Copying does not insert it into the real feedback panel.
8. Nothing automatically submits or starts a rescan.

Expose integration callbacks or custom events for:

```text
suggestion accepted
suggestion edited
suggestion dismissed
consolidation requested
feedback copied
```

Do not call a fixed URL. Provide an adapter interface that the internal application can connect to its actual backend.

## Standalone demo

Create:

```text
frontend/rpr-enhancement-demo.html
```

It must run locally without a server and demonstrate:

1. A sufficient-evidence section with no enhancement card.
2. A genuine no-evidence result with no card.
3. A fixable Credit Market Impact gap with one amber card.
4. Editing and accepting the suggestion.
5. Producing final copyable feedback.
6. Dismissing a suggestion.
7. A technical failure that produces no enhancement card.

Use mock data clearly labelled as demonstration data. Do not present mock market figures as real evidence.

## Trigger 2 integration document

Create a short `TRIGGER2_INTEGRATION.md`.

It must explain that the actual Trigger 2 report-generator prompt was not provided and therefore was not recreated.

Document only the minimal changes that must later be applied to the real Trigger 2 prompt:

* Treat the narrative as unverified user input.
* Verify material claims independently.
* Use per-section evidence handling.
* Keep evidence tier separate from retrieval status.
* Use `NOT_ASSESSED` for technical failure.
* Require per-claim URLs.
* Preserve existing field labels and parsing structure.
* Connect the shared diagnosis and consolidation workflow using `scope_type="trigger2"`.

Do not fabricate Trigger 2’s original fields, demonstration or wording.

## Tests

Create standard-library `unittest` tests covering:

* Sufficient evidence does not trigger diagnosis.
* Genuine `NONE` may be evaluated but defaults to no card unless the adviser recommends a specific fixable cause.
* Technical failure never generates an enhancement card.
* Missing query log prevents diagnosis.
* Valid `RECOMMENDED` response passes validation.
* Invalid response fails safely.
* Duplicate refinement is rejected.
* Third enhancement-assisted attempt is rejected.
* Trigger 1 allocation is preserved.
* Trigger 2 allocation is preserved.
* Consolidated feedback is formatted correctly.
* No function automatically submits feedback or rescans.

Run the tests before delivery.

## Integration guide

Keep `README_INTEGRATION.md` practical and concise.

Identify the exact host-application connection points without inventing their filenames:

1. Load the three runtime prompt text files.
2. Supply actual query-execution logs.
3. Call diagnosis after a scope completes.
4. Pass the response to the frontend component.
5. Connect the consolidation request to the approved AI client.
6. Mount the component in the existing result card.
7. Connect copied feedback to the existing manual user workflow.
8. Apply the documented Trigger 2 prompt changes once its real source is available.

Clearly label all adapter points as requiring internal integration.

## Validation

Before delivery:

* Confirm the three `.txt` files match the attached approved documents.
* Run all Python unit tests.
* Open the standalone HTML demo and test every interaction.
* Check that JavaScript produces no console errors.
* Confirm no code uses invented internal endpoints.
* Confirm no code automatically submits feedback or rescans.
* Confirm no Trigger 2 prompt was fabricated.

Return:

1. `rpr_enhancement_package.zip`
2. The individual generated files.
3. A short test result summary.

Do not provide a long design explanation. Generate the actual package and working standalone code.
