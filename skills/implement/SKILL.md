---
name: implement
description: "Implement a piece of work based on a spec or set of tickets."
disable-model-invocation: true
---

Implement the work described by the user in the spec or tickets.

If the user passes a ticket reference, fetch it from the issue tracker and state its title before starting. If the reference is ambiguous, ask.

Call the Skill tool with "tdd" where possible, at pre-agreed seams.

Run typechecking regularly, single test files regularly, and the full test suite once at the end.

Once done, call the Skill tool with "code-review" to review the work.

Commit your work to the current branch.

## Arena Execution Mode

When invoked with `--arena`, `/arena`, or for tasks with high architectural uncertainty, call the `arena` skill to spawn 2 parallel candidates in isolated Git worktrees, cross-judge them against a concrete rubric, pick the strongest base, and graft the best parts before finalizing.

## Prove-it-works (Lauren Tan)

Before declaring any ticket or implementation complete, capture and display unedited terminal execution output proving that the code compiled, executed, and passed tests in the real environment without tautological mocks.

## Anti-Rationalization Table (Addy Osmani)

Left to themselves, models seek the path of least resistance. The following shortcuts are **STRICTLY FORBIDDEN**:

| Agent Rationalization / Shortcut | Mandated System Rebuttal |
| :--- | :--- |
| *"I mocked this dependency because running the real service is slow or complex."* | **REJECTED.** Tautological mocks that do not reflect runtime reality cause outages. Tests must verify against the real observable boundary. |
| *"The test executed without throwing an error, so the feature works."* | **REJECTED.** Execution without asserting output values, ANSI sequences, or state changes is a false positive. You must assert actual output. |
| *"I will write the implementation now and add tests later."* | **REJECTED.** Untested code is unverified debt. Write the failing test first (Red-Green-Refactor). |
| *"I added optional chaining `?.` or a try/catch to silence the undefined error."* | **REJECTED.** Fix root causes. Never mask upstream contract corruption with defensive guards. |
| *"I removed this assertion or linter rule because it was failing."* | **REJECTED (Chesterton’s Fence).** Document why the constraint was added before altering it. |
