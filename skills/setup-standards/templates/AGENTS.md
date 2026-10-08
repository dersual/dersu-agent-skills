# AGENTS.md — Repository Operating Manual

## 1. Technical English & Communication (ASD-STE100)

- Write short, direct sentences with one main action per sentence.
- Use active voice and consistent technical terms. Avoid conversational filler.
- Format code and file references as clickable links (`file:///path#L10-L20`).
- **Surface Ambiguity**: If multiple interpretations or simpler approaches exist, state them explicitly before implementing.

## 2. Autonomous Discovery & Environment Truth

- Inspect files, read type definitions, check `--help`, and review git history immediately without asking permission.
- Derive API contracts from source code, config files, installed types, or official documentation.
- When library behavior is unverified, write a small runnable probe rather than guessing.
- Do not invent speculative abstractions, single-use wrapper layers, or features beyond what was requested.

## 3. Surgical Edits

- Confine edits strictly to the symbols and files required for the task.
- Match existing codebase formatting, naming conventions, and local idioms.
- Remove imports, variables, and temporary files that your changes make unused. Mention unrelated dead code rather than deleting it.
- **Isolate Refactorings**: Keep structural cleanup strictly separate from functional feature additions.

## 4. Goal-Driven Execution & Verification

- **Small Incremental Slices**: Deliver complex tasks in small, verifiable increments rather than massive unverified diffs.
- **Pin Before Refactoring**: When altering existing logic, ensure characterization tests verify current behavior before modifying it.
- **Verify Before Claiming**: Run the repository's test, lint, or build commands before declaring success. Never claim completion without verification.
- **Fail Fast**: Surface errors and inspect stderr; never silently swallow failures.
- **Verify Wire-Up**: On end-to-end features, confirm new logic is connected to the application.
- **State Gaps**: State any unverified edge cases or platforms before finishing.
- **Safety**: Obtain approval before executing git commits, pushes, or destructive actions.

## 5. Pointers

- **Code Standards**: See `CODING_STANDARDS.md` (read during review).
- **Issue Tracker**: See `docs/agents/issue-tracker.md`.
- **Domain Terms**: See `docs/agents/domain.md` and `GLOSSARY.md`.
