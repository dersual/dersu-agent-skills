# Stateful Code Coach with Home-Directory Scope & Three Implementation Gears

Status: accepted

We upgrade `skills/code-coach` into a stateful, learning-first engineering coach combining open-ended `Build / Design / Implementation Checkpoints`, three selectable `Implementation Gears` (`Architect`, `Guided Pair`, `Hands-On`), Socratic debugging, `Toy Example` concept grounding, and two-layer `Verification Audits`. We store all activation rules and learner/project state in the user's home directory (`~/.agents/code-coach/` and global harness instruction files), keep `skills/code-tutor` as a standalone stateless code/concept walkthrough skill, and move `skills/toggle-code-coach` to `deprecated/toggle-code-coach`.

## Context and Problem

1. **Workspace Pollution from `toggle-code-coach`**: `skills/toggle-code-coach` previously toggled `code-coach` by editing the active repository's tracked `CLAUDE.md`, `GEMINI.md`, or `AGENTS.md`. This dirtied `git status` in project repositories and required a separate always-loaded skill description.
2. **One-Gear Rigidity vs. Passive Vibe Coding**:
   - The original `code-coach` was stateless and only supported manual `Scaffold` stubs (`TODO` placeholders). It had no architecture design checkpoints, no memory of demonstrated mastery, and no option to let the agent write boilerplate once the developer proved they owned the design.
   - Conversely, pure "You build, AI writes" plugins (`nykooi1/vibe-wise`) train architectural reasoning via open-ended checkpoints and `.vibe-wise/` notes, but default to AI writing all code (risking hands-on coding atrophy), pollute project roots with `.vibe-wise/` folders, and lack structured post-code **Verification Audits** (training the developer to verify diffs, failure modes, and E2E/test coverage rather than passively reading an AI summary).

## Considered Options

1. **Install `nykooi1/vibe-wise` directly alongside old `code-coach` and `toggle-code-coach`**: Rejected because it creates `.vibe-wise/` folders inside target repositories, depends on Python hooks outside our pure-Markdown portability invariant, lacks `Hands-On` (`Scaffold`) and `Guided Pair` (red-test + core logic stub) gears, and splits coaching across multiple colliding skills.
2. **Deprecate both `toggle-code-coach` and `code-tutor`**: Rejected because `code-tutor` remains valuable as a lightweight, stateless, standalone skill for explaining a specific code snippet or concept step-by-step outside a stateful coaching project.
3. **Consolidate toggling, onboarding, VibeWise checkpoints, 3 Implementation Gears, and Verification Audits into `skills/code-coach/` backed by `~/.agents/code-coach/` and home-directory global instruction files; move `toggle-code-coach` to `deprecated/`**: Accepted.

## Decision

1. **Zero-Workspace-Pollution Home-Directory State & Scoped Global Pointer**:
   - All learner state lives under `~/.agents/code-coach/`:
     - `~/.agents/code-coach/profile.md`: Global developer profile (experience level, stack familiarity, checkpoint frequency, question style, default `Implementation Gear`, and evidenced `Strong / Developing / Revisit` concepts).
     - `~/.agents/code-coach/projects/<project-slug>/project-map.md` and `progress.md`: Per-project system map (distinguishing `Proposed`, `Chosen`, `Implemented`, and `Unknown (?)` components), decision log, and `## Pending decision`.
   - Running `/code-coach` with `on | off | pause | global | status | reset` manages a delimited `<!-- code-coach:start --> ... <!-- code-coach:end -->` pointer block inside the user's home-directory global instruction files (`~/.config/opencode/AGENTS.md`, `~/.claude/CLAUDE.md`, `~/.gemini/GEMINI.md`, `~/.codex/AGENTS.md`).
   - The global pointer lists the exact active project paths inline (or `ALL`). In any directory not listed in that pointer, the agent sees the path mismatch immediately with zero extra file reads and applies zero `code-coach` rules.
2. **Four-Part Coaching Loop with Three `Implementation Gears` and Two-Layer `Verification Audit`**:
   - **Reasoning First (`✦ Build checkpoint` -> `✦ Design checkpoint`)**: Requires the developer to propose the approach, data representation, trade-offs, and verification plan in plain English in chat before offering solutions. Separates any agent-suggested details into a `Proposed additions` table (`Detail | Proposal | Why it matters`).
   - **Gated Execution (`✦ Implementation checkpoint`)**: Uses the native `question` tool to confirm coding scope and select/override the `Implementation Gear`:
     1. `Architect` (Full VibeWise: agent writes agreed code + tests, then delivers an `✦ Implementation report` + `Verification Audit`).
     2. `Guided Pair` (Hybrid TDD: agent writes plumbing + failing Red tests and leaves a `Scaffold` `TODO` for the core business/algorithmic function).
     3. `Hands-On` (Strict Scaffold: agent outputs only signatures, docstrings, `TODO` contracts, and empty placeholders; developer writes code and tests).
   - **Two-Layer `Verification Audit`**: Combines pipeline verification (explicitly separating *Tests Written* from *Checks Executed* and E2E/edge-case coverage, optionally chaining into `/code-review`) with human diff auditing (one targeted question asking the developer to inspect a specific generated seam for edge cases, race conditions, or failure modes).
   - **Socratic Debugging (`✦ Debug checkpoint`) & Grounding (`✦ Concept` / `✦ Why this matters` + `Toy Example`)**: Preserves zero-diff root-cause diagnosis on errors and unrelated-domain `Toy Examples` connected to primary documentation.
3. **Keep `skills/code-tutor` Standalone; Deprecate `skills/toggle-code-coach`**:
   - Move `skills/toggle-code-coach` to `deprecated/toggle-code-coach` (`disable-model-invocation: true`).
   - Tighten `skills/code-tutor/SKILL.md` so its pointer description does not collide with `code-coach` and its steps connect syntax to underlying fundamentals and primary docs.
