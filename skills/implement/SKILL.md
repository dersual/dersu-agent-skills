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

Commit your work to the current branch. In the commit message body, record the verification command used: `Verified-by: <terminal-test-command>`.

## Arena Execution Mode

When invoked with `--arena`, `/arena`, when a ticket carries a `complexity:high`, `arena`, or `#arena` tag, or for tasks with high architectural uncertainty, call the `arena` skill to spawn parallel candidates in isolated Git worktrees, cross-judge them against a concrete rubric, pick the strongest base, and graft the best parts before finalizing.

## Prove-it-works (Lauren Tan)

Before declaring any ticket or implementation complete, capture and display unedited terminal execution output proving that the code compiled, executed, and passed tests in the real environment without tautological mocks. Self-attestation ("I have implemented and verified this") without accompanying terminal execution output is strictly rejected.

## Anti-Rationalization Principles & Catalog (Addy Osmani)

Left to themselves, models seek the path of least resistance. 

> [!IMPORTANT]
> **The Core Invariant:** Do not treat this table as a literal string filter. The core rule is: **Never substitute simulated, papered-over, or weakened verification for real runtime correctness.**  
> An agent must never adjust the test to accommodate buggy code, never claim something works without running it, and never assume an unexecuted code path is safe.

The following failure modes are **STRICTLY FORBIDDEN**:

| Agent Rationalization / Shortcut | Mandated System Rebuttal |
| :--- | :--- |
| *"I mocked this dependency because running the real service is slow or complex."* | **REJECTED.** Tautological mocks that do not reflect runtime reality cause outages. Tests must verify against the real observable boundary. |
| *"The test executed without throwing an error, so the feature works."* | **REJECTED.** Execution without asserting output values, ANSI sequences, or state changes is a false positive. You must assert actual output. |
| *"I will write the implementation now and add tests later."* | **REJECTED.** Untested code is unverified debt. Write the failing test first (Red-Green-Refactor). |
| *"I added optional chaining `?.` or a try/catch to silence the undefined error."* | **REJECTED.** Fix root causes. Never mask upstream contract corruption with defensive guards. |
| *"I removed this assertion or linter rule because it was failing."* | **REJECTED (Chesterton’s Fence).** Document why the constraint was added before altering it. |
| *"I verified this mentally / it compiles, so I don't need to run the test."* | **REJECTED.** Terminal execution with visible assertion pass is mandatory. Zero mental simulation. |
| *"I changed the test assertion or fixture to match what the code returned."* | **REJECTED.** Changing expected test values to match buggy code defeats the regression suite. The code must conform to the spec, not the spec to buggy code. |
| *"I wrote a unit test with fully mocked dependencies instead of testing the seam."* | **REJECTED.** A test asserting against mock return values only tests that your mock returns what you told it to return. Seam boundaries (IPC, CLI, HTTP, DB) must be exercised with realistic contracts. |
| *"This edge case won't happen in normal usage, so I skipped handling it."* | **REJECTED.** Edge cases are where production systems break. Handle boundary values, empty collections, error states, and disconnections explicitly. |
| *"I commented out or disabled a failing test to get a green build."* | **REJECTED.** Disabling tests masks regression. Fix the defect or document the removal with explicit user approval. |
