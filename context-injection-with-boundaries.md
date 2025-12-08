Context Injection with Boundaries

Anthropic engineers inject massive context but set clear boundaries on what matters.

Template:

[CONTEXT]
[paste your documentation, code, research paper]

[FOCUS]
Only use information from CONTEXT to answer. If the answer isn't in CONTEXT, say "Insufficient information in provided context."

[TASK]
[your specific question]

[CONSTRAINTS]
- Cite specific sections when referencing CONTEXT
- Do not use general knowledge outside CONTEXT
- If multiple interpretations exist, list all

---

Example:

[CONTEXT]
[paste your company's 50-page API documentation]

[FOCUS]
Only use information from CONTEXT to answer. If the answer isn't in CONTEXT, say "Insufficient information in provided context."

[TASK]
How do I implement rate limiting with retry logic for the /users endpoint?

[CONSTRAINTS]
- Cite specific sections when referencing CONTEXT
- Do not use general knowledge outside CONTEXT
- If multiple interpretations exist, list all

---

Eliminates hallucinations when working with proprietary systems.