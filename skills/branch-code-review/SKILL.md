---
name: branch-code-review
description: skeptical code-review workflow for AI coding agents reviewing local git changes, pull requests, or a specified number/range of commits. use when asked to review current changes, uncommitted changes, a branch relative to origin/main or another base, recent commits, or a PR diff. prioritize correctness, regressions, edge cases, security, performance, missing tests, API compatibility, and maintainability. if a solid skill is available in the environment, load and follow it first, then apply this review workflow.
---

# Branch Code Review

## Primary directive

Act like a skeptical PR reviewer. Do not assume the implementation is correct. Review only evidence visible in the repository, diff, tests, and referenced files. Prefer `no issues found` over speculative or praise-only comments.

If a SOLID skill is available, read and follow it before applying this skill. Common local paths include:

- `file:///c%3A/Users/dsual/.agents/skills/solid/SKILL.md`
- `C:\Users\dsual\.agents\skills\solid\SKILL.md`
- `~/.agents/skills/solid/SKILL.md`

Do not silently skip this. If the SOLID skill cannot be accessed, say so briefly in the review setup and continue with this skill.

## Inputs to accept

Accept any of these review scopes:

- Current working tree changes.
- Staged changes only.
- All changes on the current branch relative to `origin/main`.
- All changes relative to a user-provided base branch, tag, or commit.
- The last `N` commits.
- A specific commit range.
- A PR branch or checked-out PR diff visible to the agent.

If no scope is specified, default to reviewing all changes on the current branch relative to `origin/main`. If the repository has no `origin/main`, use the best available default branch such as `origin/master`, `main`, or `master`, and state the assumption.

## Review setup

1. Identify the repository root and current branch.
2. Determine the base and review range.
3. Inspect the changed file list before reading hunks.
4. Inspect the full diff with enough context to understand control flow and API changes.
5. Open surrounding source files when a changed hunk depends on definitions, call sites, imports, config, or tests outside the diff.
6. Check whether relevant tests changed or are missing.
7. Run focused tests, type checks, linters, or builds when available and practical. Do not invent test results; report commands that were run and their outcomes.

Useful git commands, adapting the base/range as needed:

```bash
# branch relative to origin/main
git merge-base HEAD origin/main
git diff --stat origin/main...HEAD
git diff --name-status origin/main...HEAD
git diff --find-renames --find-copies origin/main...HEAD

# working tree
git diff --stat
git diff --name-status
git diff --find-renames --find-copies

# staged only
git diff --cached --stat
git diff --cached --name-status
git diff --cached --find-renames --find-copies

# last N commits
git diff --stat HEAD~N..HEAD
git diff --name-status HEAD~N..HEAD
git diff --find-renames --find-copies HEAD~N..HEAD
```

Prefer three-dot comparison for branch reviews (`base...HEAD`) so the review covers changes since the branch diverged from base.

## What to look for

Prioritize real defects that could affect users, production, developers, data, security, or compatibility.

Review for:

- Correctness: broken logic, incorrect assumptions, race conditions, bad state transitions, off-by-one errors, null/undefined handling, time/date mistakes, serialization issues, retry/idempotency bugs.
- Regressions: changed behavior not accounted for by callers, config, migrations, feature flags, or existing tests.
- Edge cases: empty input, large input, duplicate input, missing optional fields, time zones, partial failures, network failures, permission failures.
- Security: injection, authz/authn bypass, path traversal, SSRF, unsafe deserialization, secret exposure, weak crypto, overly broad permissions, unsafe logging, dependency risks introduced by the diff.
- Performance: avoidable N+1 queries, quadratic loops, large memory use, blocking I/O in hot paths, cache invalidation mistakes, excessive logging, unnecessary rebuilds.
- Tests: missing tests for changed behavior, weak assertions, tests that do not fail before the fix, snapshot churn hiding behavior, missing migration/rollback coverage.
- API compatibility: public contract changes, schema changes, migrations, response-shape changes, backward/forward compatibility, versioning, caller impact.
- Maintainability: overly complex code, unclear ownership, duplicated business logic, misleading names, hidden coupling, brittle abstractions.

Avoid:

- Praise-only comments.
- Style-only comments unless they materially affect maintainability or correctness.
- Speculation without a plausible failure mode tied to changed code.
- Comments on unchanged code unless the diff introduces or exposes the issue.

## Output format

Start with a short review scope summary:

```markdown
Reviewed: <scope/range>
Base: <base or assumption>
SOLID skill: <loaded / not available: reason>
Checks run: <commands and outcomes, or "not run">
```

Then provide findings in descending severity. For every finding include all fields exactly:

```markdown
### <severity>: <short issue title>
- file/path: `<path>`
- approximate line or changed hunk: <line number, function, or hunk description>
- why this is a real issue: <specific failure mode and impact>
- how to verify it: <manual reproduction, focused test, command, or assertion that would fail>
- suggested fix: <concrete code-level or design-level fix>
```

Severity definitions:

- `blocker`: likely production breakage, data loss/corruption, security vulnerability, broken build, broken migration, or unusable core flow.
- `major`: real user-visible bug, meaningful regression, significant missing test for risky behavior, compatibility break, or serious maintainability/performance issue.
- `minor`: localized correctness, edge case, test, or maintainability issue with limited blast radius.
- `nit`: small but concrete issue worth fixing, not mere preference.

If there are no findings, output:

```markdown
Reviewed: <scope/range>
Base: <base or assumption>
SOLID skill: <loaded / not available: reason>
Checks run: <commands and outcomes, or "not run">

No issues found.
```

## Verification discipline

For each potential issue, ask:

1. Is the issue introduced or materially exposed by this diff?
2. Is there a concrete runtime, security, data, compatibility, or maintenance failure mode?
3. Can a reviewer verify it with a command, test, input, or code path?
4. Is the suggested fix actionable?

Only include the finding if the answer to all four is yes.

## Example user prompts

```text
Follow instructions in [SKILL.md](file:///c%3A/Users/dsual/.agents/skills/branch-code-review/SKILL.md).
Review all changes on this branch relative to origin/main.
```

```text
Use the branch-code-review skill. Review my current uncommitted changes as a skeptical PR reviewer.
```

```text
Use the branch-code-review skill. Review the last 4 commits and focus on correctness, regressions, missing tests, and API compatibility.
```
