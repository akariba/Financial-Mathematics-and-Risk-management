Review only the Python files I have already uploaded.

Do not:

* Ask me to upload additional files.
* Generate new files or artifacts.
* Modify any code.
* Produce implementation code.
* Invent missing architecture, filenames, functions or endpoints.

Your task is only to understand and explain the existing backend design represented by the uploaded Python files.

Please analyze:

1. The purpose of each uploaded Python file.
2. The responsibility of every important class and function.
3. The actual application entry point.
4. How Trigger 1 and Trigger 2 are currently initiated.
5. How prompts are stored, loaded and passed to the AI.
6. How web searches or external retrieval are executed.
7. How search results are collected and transformed.
8. Whether executed search queries are currently recorded.
9. How AI responses are parsed and validated.
10. How theme, event and narrative scopes are represented.
11. How results are returned to the HTML/frontend.
12. Existing routes, endpoints or server actions.
13. Existing feedback and rescan behaviour visible in the uploaded code.
14. Current state-management approach.
15. Current timeout, retry and error-handling behaviour.
16. Whether processing is synchronous or asynchronous.
17. Relationships and call flow between the uploaded files.
18. Which exact existing functions would likely participate in the proposed enhancement workflow.
19. Where the generated `rpr_enhancement.py` design aligns or conflicts with the real uploaded backend.
20. Any risks or unknowns visible from the uploaded files.

For every conclusion:

* Cite the exact uploaded filename.
* Cite the actual class or function name.
* Clearly distinguish confirmed behaviour from inference.
* If something cannot be determined, write `Not visible in the uploaded files`; do not request more files.

End with:

* A concise end-to-end backend flow based only on what is visible.
* A list of likely integration points using exact existing filenames and function names.
* A short list of design questions that remain unresolved—but do not ask me to provide anything else yet.

Respond directly in the chat. Do not create or modify artifacts.
