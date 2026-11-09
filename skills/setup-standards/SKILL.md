---
name: setup-standards
description: Scaffolds or standardizes repository coding standards (CODING_STANDARDS.md) and agent behavioral guidelines (AGENTS.md). Use when initializing a new repository, auditing repo configuration, or standardizing code quality and anti-slop rules across projects.
---

# Setup Standards

Scaffolds or updates repository coding standards (`CODING_STANDARDS.md`) and agent behavioral guidelines (`AGENTS.md`).

## Process

### 1. Inspect Existing Workspace

Check the repository root for existing configuration files:
- `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md`
- `CODING_STANDARDS.md` or `CONTRIBUTING.md`
- `docs/agents/issue-tracker.md`

Detect the primary tech stack and tooling (e.g., TypeScript/Node, Python, Go, Rust, React) by inspecting `package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, etc.

### 2. Scaffold or Update `AGENTS.md`

If `AGENTS.md` does not exist:
- Copy the baseline from `templates/AGENTS.md`.

If `AGENTS.md` (or equivalent) already exists:
- Perform a non-destructive audit. Ensure the core pillars are present:
  1. **Think Before Coding** (state assumptions, ask when uncertain)
  2. **Simplicity First** (minimum code, no single-use speculative abstractions)
  3. **Surgical Changes** (touch only what you must, match local style, isolate refactors)
  4. **Epistemic Boundaries** (never guess unverified API contracts)
  5. **Goal-Driven Execution** (verifiable success criteria, small incremental slices)
- Preserve any project-specific rules already documented.

### 3. Scaffold or Update `CODING_STANDARDS.md`

If `CODING_STANDARDS.md` does not exist:
- Copy the template from `templates/CODING_STANDARDS.md`.
- Tailor language-specific notes if relevant (e.g., TS strict type notes or Python type hints), while preserving the core four sections:
  1. **Structure & Simplicity (Code Judo)** (no useless indirection, flat control flow, focused modules, contract/alias stability)
  2. **Types & Invariants** (no type escapes, parse at the boundary, simple data structures)
  3. **Anti-Slop** (no narration comments, preserve navigation banners, natural prose, no paranoia `try/catch`, match local idioms)
  4. **Tests** (public seams, avoid tautological tests and excessive mocks)

If `CODING_STANDARDS.md` already exists:
- Propose additions for missing anti-slop or structural simplicity rules while preserving existing team standards.

### 4. Verify `code-review` Integration

Confirm that `code-review` can locate the standards:
- Ensure `CODING_STANDARDS.md` is in the repository root.
- If `docs/agents/issue-tracker.md` is missing and the repo uses an issue tracker, suggest running `/setup-repo` or configure the issue tracker pointer.

### 5. Completion Summary

Report the files created or updated:
- Absolute or relative paths to modified files.
- Brief summary of the standards established.
