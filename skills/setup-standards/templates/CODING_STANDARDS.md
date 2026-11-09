# Coding Standards

Engineering conventions and quality standards for this codebase. Evaluated during `/code-review` and architectural planning. Automated linters handle syntax; this document defines structure, boundaries, error handling, and slop prevention.

## 1. Structure & Simplicity (Code Judo)

- **Structural Simplification (Code Judo)**: Be ambitious about code structure. Look for opportunities to reframe changes so that whole branches, helpers, modes, conditionals, or layers disappear entirely. Prefer solutions that make code feel inevitable in hindsight. If there is a path to delete complexity rather than rearrange it, take that path.
- **Zero Useless Indirection**: Inline single-use helpers, identity wrappers, and pass-through classes. Inline until genuine reuse emerges (Rule of Three). Flag thin abstractions that add indirection without buying clarity.
- **No Random Spaghetti Growth**: Do not allow ad-hoc conditionals, scattered special cases, or one-off branches inserted into unrelated flows. If a change adds "weird if statements in random places", push logic into a dedicated abstraction, state machine, policy object, or separate module.
- **Flat Control Flow**: Prefer early returns, guard clauses, and pattern matching. Avoid deep nesting (> 2 levels).
- **The 1,000-Line File Threshold**: Do not let a change push a file from under 1k lines to over 1k lines without a very strong reason. Prefer extracting subcomponents, cohesive helpers, or colocated modules instead of letting files sprawl.
- **Canonical Layering & Reuse**: Keep business logic in domain/service layers; keep UI, routing, and presentation components lean. Prefer existing canonical utilities over bespoke one-offs.
- **Contract & Alias Stability**: Do not delete backwards-compatibility aliases or public exports that protect existing callers without an explicit deprecation plan.
- **Do Not Rubber-Stamp "It Works"**: If behavior can stay the same while the structure becomes meaningfully cleaner, demand the cleaner version. Avoid implementations that technically work but leave the codebase messier.

## 2. Types & Boundary Invariants

- **No Type Escapes**: Never use `any`, forced casts, or loose type assertions to silence compiler errors. Fix types at the source.
- **Parse at the Perimeter**: Validate untrusted external data (network, disk, CLI, environment) at the boundary into typed domain models. Keep internal trusted paths direct.
- **Direct, Boring Data Shapes**: Default to plain objects/interfaces and pure functions over complex class inheritance hierarchies. Be skeptical of generic mechanisms that hide simple data-shape assumptions.

## 3. Anti-Slop (Clean AI Output)

- **Explain Why, Not What**: Never write comments explaining *what* code does (e.g., `// return response` or `// increment counter`). Comment only non-obvious *why* (business constraints, algorithmic subtleties, workarounds).
- **Preserve Navigation Banners**: Structural section headers (e.g., `// ── DOM BINDINGS ──` or block labels) that aid visual scanning in large files are welcome. Only strip redundant syntax narration.
- **Natural, Humanized Prose**: Keep PR descriptions, commit messages, and markdown documentation concise, direct, and free of chatbot filler, inflated claims, or marketing fluff.
- **Fail Fast over Silent Fallbacks**: Catch expected errors at system boundaries. Do not wrap internal logic in defensive `try/catch` blocks that silently mask failures or return fake fallbacks. Let errors bubble to real boundary handlers.
- **Preserve Local Idioms**: Match existing codebase style, naming conventions, and patterns rather than introducing foreign paradigms or unnecessary third-party dependencies.

## 4. Tests & Seams

- **Public Seams & Invariants**: Test observable public behavior and contracts, not private internal mechanics.
- **No Tautological Tests**: Avoid tests that merely re-assert mocks or mirror implementation details.
- **Avoid Excessive Mocking**: Prefer fast, deterministic integration and unit tests over heavy mock graphs. Never mock the primary integration boundary (IPC, disk, child process).

## 5. Five-Axis Quality Contract & Verification Invariants

Evaluated during `/code-review` across five mandatory dimensions:

1. **Correctness:** Logic satisfies all acceptance criteria under nominal and boundary inputs. Tests assert actual output values, not just that code executed without throwing.
2. **Security:** Inputs parsed at perimeter; credentials kept out of git; IPC channels validated.
3. **Architecture:** Respects deep module boundaries; avoids circular dependencies; maintains layer separation.
4. **Performance:** Optimal algorithms; no premature allocation or memory leaks.
5. **Readability:** Clean, idiomatic, self-documenting code free of AI conversational slop.

### Mandatory Anti-Rationalization Table

| Prohibited Agent Rationalization | Mandatory System Rebuttal |
| :--- | :--- |
| *"I mocked this dependency because running the real service is slow or complex."* | **REJECTED.** Tautological mocks that do not reflect runtime reality cause outages. Tests must verify against the real observable boundary (Electron IPC, real disk, real subprocesses). |
| *"The test executed without throwing an error, so the feature works."* | **REJECTED.** Execution without asserting output values, ANSI sequences, or state changes is a false positive. You must assert actual output. |
| *"I will write the implementation now and add tests later."* | **REJECTED.** Untested code is unverified debt. Write the failing test first (Red-Green-Refactor). |
| *"I added optional chaining `?.` or a try/catch to silence the undefined error."* | **REJECTED.** Fix root causes. Never mask upstream contract corruption with defensive guards. |
| *"I removed this assertion or linter rule because it was failing."* | **REJECTED (Chesterton’s Fence).** Document why the constraint was added before altering it. |
