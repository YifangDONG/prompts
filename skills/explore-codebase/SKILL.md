---
name: explore-codebase
description: Explores an unfamiliar codebase or module using a structured reading methodology (functional purpose, entry points, decomposition, dependency graph, patterns, history, tests) and produces a written analysis report. Use when the user asks to analyze, explore, onboard, understand, read, map, or document an unknown module, package, or codebase, or when starting work on unfamiliar code before adding features, fixing bugs, or refactoring.
---

# Explore Codebase

Analyze an unknown module or codebase to recover the ~80% most important information a developer needs before modifying it. Do not dive into implementations; build a shallow, structural understanding first, then produce a report.

## Guiding principle

The larger the codebase, the shallower the first pass. The goal is **not** to understand every line, but to answer: *"What does this do, where does it start, and how does it decompose?"*

## Workflow

Copy this checklist and track progress as you analyze:

```
Analysis Progress:
- [ ] Step 1: Clarify scope
- [ ] Step 2: Functional description
- [ ] Step 3: Entry point(s)
- [ ] Step 4: Decomposition (packages / folders)
- [ ] Step 5: Dependency graph (via imports)
- [ ] Step 6: Interfaces, attributes, methods of boundary classes
- [ ] Step 7: Pattern recognition
- [ ] Step 8: Commit history spot-checks (only for anomalies)
- [ ] Step 9: Tests as executable documentation
- [ ] Step 10: Write the report
```

### Step 1 — Clarify scope

Before reading anything, confirm with the user (or infer from the request):

- Which module / folder / package is the target?
- What is the purpose of the analysis? (onboarding, bug hunt, refactor, feature addition)
- What depth is expected? (one-pager overview vs. deep dive on a submodule)

If the target is ambiguous, ask once, then proceed.

### Step 2 — Functional description

Do **not** read code yet. Figure out what the module is *for*.

- **UI module** → look at the screen/component it renders; describe what a user can do with it.
- **Domain module** → identify the business concept it represents (e.g. "billing", "scheduling").
- **Process module** → list the main steps of the process it orchestrates.
- **Library/infra module** → state the capability it provides to callers.

Sources to consult (in order): `README.md`, top-level docs, package-level docstrings/JSDoc, the folder name itself. If none exist, infer from public API names.

Output: a 2–4 sentence plain-English description.

### Step 3 — Find the entry point(s)

The entry point defines the boundary; everything inside is in scope, everything outside is not.

Typical entry points by project type:

| Project type | Likely entry point |
|---|---|
| CLI | `main`, `bin/*`, `cmd/*`, `if __name__ == "__main__"` |
| Web backend | route/controller registration, `app.ts`/`server.py`, router files |
| Web frontend | root component, route config, `index.tsx`/`main.ts` |
| Library | exports in `index.*`, `__init__.py`, `mod.rs`, public `package.json` `exports` |
| Module within project | public `index.*`, facade class, exported symbols |

Techniques: read `package.json` / `pyproject.toml` / `Cargo.toml` / `go.mod` for entry points; look for `export` statements in an index file; search for the module's name being imported elsewhere.

Output: list of entry files/classes with one line each on their role.

### Step 4 — Decomposition via package/folder structure

List the top-level folders inside the module. Package names hint at architecture:

- `models` / `views` / `controllers` → MVC
- `services` / `repositories` / `entities` / `domain` → layered / DDD
- `queues` / `aggregates` / `filters` / `handlers` → domain-specific; flag terms you don't recognize for later
- `utils` / `helpers` / `common` / `tools` → **skip on first pass**
- `test` / `__tests__` / `spec` → revisit in Step 9

If folder names are ambiguous or the structure is flat, fall back to class/module names.

Output: a tree diagram annotated with one-line roles.

### Step 5 — Dependency graph via imports

For each significant file in scope, look at its imports.

- **Internal imports** (within the module) → reveal internal structure and collaborators.
- **External imports** (other modules, third-party) → classify the file. A class with many external deps is usually a **boundary** (thin, orchestrating) and holds little logic; a class with few external deps is usually a **core** (rich logic).

Build the skeleton from boundary files inward. Do **not** try to draw the full graph — focus on directionality (who depends on whom) and prune aggressively. If tooling (language server, `madge`, IDE UML) is available, use it, but filter to one direction at a time to avoid arrow soup.

Output: an ASCII/mermaid diagram of 5–15 key nodes with arrows, labeled as boundary/core.

### Step 6 — Interfaces, attributes, methods

For each boundary/core component identified in Step 5:

- **Interfaces / public methods** → what the component does (the *function*).
- **Attributes / fields** → what state it encapsulates. Classify as read-only, write-only, or read/write; or group by lifecycle phase.
- **Private methods** → ignore unless needed.

If the module is small or procedural (no clear classes), decompose by function/method instead.

Output: a table per component with columns `name | kind | role`.

### Step 7 — Recognize patterns

Once you've seen 2–3 components, form hypotheses about the rest:

- "All handlers follow `validate → transform → persist → emit`"
- "Every service has a matching repository"
- "All React components in `views/` are pure + hooks-only"

Then **verify** the hypothesis by spot-checking a few more files rather than reading them line-by-line. Named design patterns (Factory, Observer, Strategy, Visitor, Middleware, Pipeline, etc.) are shortcuts — call them out explicitly when present.

Output: list of recognized patterns with 1–2 examples each, and any outliers.

### Step 8 — Commit history (only for anomalies)

Do **not** read the whole history. Use `git log` / `git blame` only when:

- A piece of code looks inconsistent with its context → check if it was added in the same commit as its neighbors or later.
- Code looks dead or duplicated → see when it was last touched.
- A naming convention breaks → check whether a different author introduced it.

Useful commands:

```bash
git log --oneline -n 20 -- path/to/file
git blame -L <start>,<end> path/to/file
git log -p -S "suspicious_symbol" -- path/
```

Output: note anomalies and, if relevant, the commit message explaining them.

### Step 9 — Tests as executable documentation

Tests often encode the *expected behavior* more clearly than code.

- **Unit tests** → understand a single class/function.
- **Integration / e2e tests** → understand a whole business flow.
- **Given-When-Then / BDD style** → read these first; they are documentation.

Look in `test/`, `__tests__/`, `spec/`, or sibling `*.test.*` / `*_test.*` files. Extract 2–5 representative test names as "the module, in examples".

Output: bullet list of the most illustrative test cases.

### Step 10 — Write the report

Use the template in [report-template.md](report-template.md). Keep it skimmable.

## Scope discipline

Repeat as a mantra during analysis:

- **Goal is decomposition, not implementation.**
- If a method body is more than a few lines, note its name and move on.
- Skip `utils`, `helpers`, generated code, and vendored dependencies unless the user asked about them.
- Stop when the report can answer: *what, where does it start, how does it split up, and what are the main collaborators.*

## Output location

Unless the user specifies otherwise, write the report to `docs/analysis/<module-name>.md` in the workspace. If `docs/analysis/` doesn't exist, ask the user where to put it (options: `docs/analysis/`, repo root, or print inline).

## Additional resources

- For the report template, see [report-template.md](report-template.md).
- For a worked example, see [example-report.md](example-report.md).
