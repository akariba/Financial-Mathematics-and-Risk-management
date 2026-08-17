Before generating or changing any more code, perform a design-discovery review of the implementation package you already created.

You do not have access to the internal RPR repository. Do not guess its filenames, frameworks, endpoints or architecture.

Your purpose is to explain precisely how your generated package is designed and identify the minimum real application files that must be supplied before an end-to-end integration patch can be designed.

Create one artifact only:

```text
INTEGRATION_DISCOVERY.md
```

## 1. Generated backend design

Inspect your actual generated file:

```text
backend/rpr_enhancement.py
```

Document every public:

* Enum.
* Dataclass.
* Function.
* Protocol/callback.
* State structure.

For every function, provide:

```text
Function:
Purpose:
Inputs:
Return value:
Caller:
When it runs:
Side effects:
Host application dependency:
```

Use the real function signatures from the generated code. Do not describe functions that do not exist.

Explain where and how the following are stored:

* Evidence tier.
* Retrieval status.
* Actual executed-query log.
* Theme/event/narrative identifiers.
* Previous attempted refinements.
* Enhancement-assisted attempt count.
* Accepted/edited/dismissed state.
* Consolidated feedback.

State clearly whether the generated module stores this state only in memory and what persistence the host application would need.

## 2. Complete execution flow

Describe the actual proposed runtime sequence from beginning to end:

1. Trigger 1 or Trigger 2 scan begins.
2. Search queries execute.
3. Search results and technical failures are recorded.
4. One scope finishes.
5. Section evidence/retrieval statuses become available.
6. Diagnosis eligibility is evaluated.
7. Diagnosis prompt is called.
8. Response is validated.
9. Amber card is rendered or suppressed.
10. User accepts, edits or dismisses.
11. Consolidation prompt is called.
12. Final feedback is copied.
13. User manually pastes feedback and presses Enter.
14. Existing application performs a rescan.
15. Duplicate and retry-limit state is checked.

For every step state:

* Generated component responsible.
* Required host-application component.
* Data entering the step.
* Data leaving the step.
* Whether it already exists in the package or still requires integration.

## 3. AI/LLM adapter contract

Explain exactly what the internal application must implement to connect its approved AI client.

For both diagnosis and consolidation, provide:

* Prompt-file path.
* Input payload.
* Expected output.
* Validation behaviour.
* Timeout/error behaviour.
* Technical-failure behaviour.
* Example invocation using a generic callable only.

Do not invent an internal AI endpoint.

## 4. Frontend design

Inspect the actual generated:

```text
frontend/rpr-enhancement-card.js
frontend/rpr-enhancement-card.css
frontend/rpr-enhancement-demo.html
```

Document:

* JavaScript class/function used to create the component.
* Constructor/options.
* Public methods.
* Required HTML mount point.
* Events or callbacks emitted.
* Expected diagnosis-response object.
* Accepted/edited/dismissed state handling.
* Consolidation invocation.
* Copy behaviour.
* Whether any action automatically submits or rescans.
* CSS variables and class-name scope.
* How more than one theme/event card is handled.
* How the component should work while the overall scan is still running.

Use the real generated JavaScript interfaces—not proposed interfaces.

## 5. Missing integration points

Produce a table:

| Integration Point | Generated Package Provides | Real Application Must Provide | Required Source File Type |
| ----------------- | -------------------------- | ----------------------------- | ------------------------- |

Include at minimum:

* Trigger 1 prompt loading.
* Trigger 2 prompt loading.
* Search-query execution log.
* Section status extraction.
* Scope-completion signal.
* AI call.
* Backend route or server action.
* Results-page mounting location.
* Existing feedback panel.
* Existing Enter/rescan handler.
* Retry-state persistence.
* Success-banner calculation.

## 6. Minimum internal files required

List the minimum real application files I must upload for a proper integration design.

Do not invent filenames. Describe them by purpose, for example:

```text
Required:
- Python file that runs Trigger 1 scanning.
- Python file that runs Trigger 2 scanning.
- Python file that invokes the AI model or agent.
- Main server/API route file.
- Trigger 1 results-page HTML.
- Trigger 2 results-page HTML.
- Shared JavaScript used by those pages.
- Existing feedback/rescan implementation.
- Runtime prompt source files.
- Relevant tests or fixtures.
```

For every requested file, explain:

* Why it is needed.
* What functions or sections must be visible.
* Whether a partial excerpt is sufficient.
* What sensitive content may be removed before upload.

Also specify which files are optional.

## 7. Known limitations and risks

Review your generated solution critically and identify:

* Anything that is demonstration-only.
* Anything held only in browser memory.
* Anything held only in Python process memory.
* Any missing concurrency handling.
* Risk of duplicate cards.
* Risk of stale cards after rescan.
* Risk of incorrect theme/event allocation.
* Risk of prompt-output parsing failure.
* Risk of multiple users sharing state.
* Any assumptions about synchronous versus asynchronous scanning.
* Anything that cannot be validated without the real application.

Do not claim the package is production-ready if these remain unresolved.

## 8. Recommended integration sequence

Provide a minimal implementation sequence, divided into:

```text
Phase 1 — Prompt and status contract
Phase 2 — Backend diagnosis call
Phase 3 — Single Trigger 1 card
Phase 4 — Feedback consolidation
Phase 5 — Rescan and loop control
Phase 6 — Trigger 2
Phase 7 — Testing and hardening
```

For every phase, state:

* Required application files.
* Expected code changes.
* Testable outcome.
* Rollback point.

## Output restrictions

* Generate only `INTEGRATION_DISCOVERY.md`.
* Do not generate new application code.
* Do not modify the existing package.
* Do not claim access to the internal repository.
* Do not use hypothetical internal filenames as confirmed facts.
* Keep the report technical but practical.
* Base every statement about the package on the actual generated artifacts.
