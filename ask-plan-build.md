---
description: "Ask-Plan-Build workflow: activate when user says /apb, ask-plan-build, or APB"
globs:
alwaysApply: false
---

# Ask-Plan-Build Workflow

Follow this 3-phase workflow strictly. **Never skip a phase.**

---

## Phase 1: ASK (Clarification Loop)

1. Analyze the user's request
2. Ask **3–5 targeted questions** covering:
   - **Scope** – What exactly needs to change? Which files/features are affected?
   - **Constraints** – Patterns, libraries, conventions, or tech stack requirements?
   - **Edge cases** – Error handling, backward compatibility, side effects?
   - **Dependencies** – Does this touch other systems or shared code?
   - **Acceptance criteria** – How do we know it's done?
3. **STOP and wait** for the user's answers
4. After receiving answers, summarize your understanding in bullet points and ask:
   > "Does this look correct? Should I proceed to **Plan**, or do you have corrections?"
5. If the user corrects or adds info, return to step 2 with follow-up questions
6. **Repeat until the user explicitly confirms** (e.g., "yes", "looks good", "proceed to plan")

⚠️ **Do NOT move to Phase 2 until the user confirms.**

---

## Phase 2: PLAN

1. Design a concrete implementation plan with **4–10 tasks**
2. Save the plan to `.cursor/plans/` as a `.plan.md` file using this format:

```yaml
---
name: <Short Plan Name>
overview: "<One-line description of what this plan achieves>"
todos:
  - id: <kebab-case-id>
    content: <What this task does, which files are involved>
    status: pending
  # ... 4-10 tasks total
isProject: false
---
```

3. Below the frontmatter, add a `## Details` section with any extra context, rationale, or notes
4. Present the plan to the user and ask:
   > "Here's the plan. Ready to **build**, or do you want changes?"
5. **STOP and wait** for the user's confirmation

⚠️ **Do NOT move to Phase 3 until the user confirms.**

---

## Phase 3: BUILD

1. Execute the plan task by task
2. Update the TodoWrite tool and the `.plan.md` file as tasks complete
3. After finishing all tasks, provide a summary:
   - Files created / modified
   - Key decisions made during implementation
   - Anything the user should verify or test
4. Ask: "Everything is done. Want me to adjust anything?"

---

## Rules

- Each phase is a **gate** — never proceed without explicit user confirmation
- Keep questions concise and numbered for easy answering
- If the user says "skip ask" or "just build", you may compress Phase 1 but still confirm scope before building
- Always save the plan file before starting to build
