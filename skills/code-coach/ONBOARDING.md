# Code Coach Lifecycle, Toggling & Onboarding

All activation pointers and learner notes live inside the user's home directory (`~`, e.g., `C:\Users\dersu\` on Windows or `/Users/<user>/` on macOS/Linux). Never modify the project repository's tracked `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, or `.gitignore`.

---

## 1. Global Instruction Files & Delimited Pointer Block

To allow every agent harness to auto-detect whether `code-coach` is active on turn 1 with **zero extra file reads in non-coached repos**, `code-coach` manages a single delimited block inside the user's home-directory global instruction files:

- **OpenCode**: `~/.config/opencode/AGENTS.md`
- **Claude Code**: `~/.claude/CLAUDE.md`
- **Gemini CLI / Antigravity**: `~/.gemini/GEMINI.md`
- **Codex**: `~/.codex/AGENTS.md`

### Exact Delimited Block Format

When `code-coach` has one or more active project roots (or `ALL`), maintain this exact block at the bottom of each global instruction file whose parent directory exists on the machine (create the markdown file if its parent config folder exists, preserving any unrelated global instructions outside the tags):

```markdown
<!-- code-coach:start -->
## Code Coach Active Scope
Active workspaces:
- `C:\Users\dersu\Code Stuff\my-learning-project`

Rule: When the current working directory is inside any path listed under `Active workspaces` above (or when `ALL` is listed), invoke and strictly follow the `code-coach` skill before generating code, designing features, debugging errors, or explaining concepts. In all other directories, ignore this block completely.
<!-- code-coach:end -->
```

When **no** workspaces are active (or `/code-coach off` removed the last workspace), remove the `<!-- code-coach:start --> ... <!-- code-coach:end -->` block cleanly from the global instruction files.

---

## 2. Lifecycle Subcommands (`on`, `off`, `pause`, `global`, `status`, `reset`)

### A. `/code-coach on` (or `/code-coach` in an unregistered workspace)
1. Resolve the current project root path (nearest `.git` root, or current working directory).
2. Add the project root path to the `Active workspaces` list inside the `<!-- code-coach:start --> ... <!-- code-coach:end -->` block across all present home-directory harness instruction files (`~/.config/opencode/AGENTS.md`, `~/.claude/CLAUDE.md`, `~/.gemini/GEMINI.md`, `~/.codex/AGENTS.md`).
3. If `~/.agents/code-coach/profile.md` or `~/.agents/code-coach/projects/<project-slug>/project-map.md` does not exist yet, run **Section 3 (Interactive Onboarding)** below.
4. Confirm the active state, active `Implementation Gear`, and updated global instruction paths in 2 sentences.

### B. `/code-coach global`
1. Set `Active workspaces:` to `- ALL` in the delimited block across the home-directory global instruction files so `code-coach` is active across every project on the machine.
2. Confirm that global `code-coach` mode is active.

### C. `/code-coach off` / `/code-coach pause`
1. Remove the current project root path from `Active workspaces` in the home-directory global instruction files (or if `ALL` was set, ask via the native `question` tool whether to disable for *this workspace only* or *all workspaces*).
2. If `~/.agents/code-coach/projects/<project-slug>/progress.md` exists, set `Learning mode: paused` at the top of `progress.md` while keeping all saved notes intact.
3. Output a 1-sentence confirmation that `code-coach` is now disabled for this workspace.

### D. `/code-coach status`
1. Read the home-directory global instruction block, `~/.agents/code-coach/profile.md`, and `~/.agents/code-coach/projects/<project-slug>/` (if present).
2. Display a concise status summary:
   - Whether the current workspace is **Active** or **Inactive**.
   - All currently registered `Active workspaces`.
   - Current defaults from `profile.md` (`Implementation Gear`, `Checkpoint frequency`, `Question style`).
   - Any open `## Pending decision` in the current project's `progress.md`.
3. Use the native `question` tool to offer quick actions:
   - `Toggle current workspace On/Off`
   - `Change default Implementation Gear (Architect / Guided Pair / Hands-On)`
   - `Change Checkpoint frequency (Light / Normal / Frequent)`
   - `Continue coding`

### E. `/code-coach reset`
1. Show the exact path to `~/.agents/code-coach/projects/<project-slug>/` and ask via the native `question` tool:
   - `1. Cancel (Keep current project learning notes)`
   - `2. Reset project notes (Backup existing project-map.md and progress.md to backups/ and restart project onboarding)`
   - `3. Reset project notes AND global profile.md`
2. On confirmation, copy the existing markdown files into `~/.agents/code-coach/projects/<project-slug>/backups/<timestamp>/` before writing fresh templates from [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md).

---

## 3. Interactive Onboarding (One Question at a Time via Native `question` Tool)

Read [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md) before writing state files. Never dump a multi-question text wall. Use the native `question` tool one screen at a time, skipping any question already answered in `~/.agents/code-coach/profile.md`.

### Phase 1: Global Developer Profile (`~/.agents/code-coach/profile.md`)
*(Run only once across the whole machine; skip if `~/.agents/code-coach/profile.md` already has `Onboarding: complete`)*

1. **Overall Programming Experience**:
   - Call `question` with options:
     - `Intermediate (Explore interactions, trade-offs, and system seams)`
     - `Beginner (Explain unfamiliar pieces, use diagrams, smaller reasoning steps)`
     - `Advanced (Probe hard constraints, concurrency/failure modes, and design assumptions)`
2. **Default `Implementation Gear`** (Who writes the code after you pass the Build/Design checkpoint?):
   - Call `question` with options:
     - `Guided Pair (Recommended) — AI writes plumbing & failing Red tests; you write the core business/algorithmic logic`
     - `Architect (VibeWise) — You reason & design first; AI writes the code & tests, then runs a Verification Audit`
     - `Hands-On (Strict Scaffold) — AI outputs signatures & TODO contracts only; you write all production code & tests`
3. **Checkpoint Preferences**:
   - Call `question` with options:
     - `Use defaults (Recommended) — Normal checkpoint frequency, open-ended reasoning questions, Two-Layer Verification Audit ON`
     - `Customize — Pick Light/Normal/Frequent checkpoints or Open-ended/Mixed/Multiple-choice style`
   - If the developer selects `Customize`, ask frequency (`Normal` / `Light` / `Frequent`) and reasoning style (`Open-ended` / `Mixed` / `Multiple choice`).
4. Save `~/.agents/code-coach/profile.md` using [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md).

### Phase 2: Project Map Initialization (`~/.agents/code-coach/projects/<project-slug>/`)
*(Run once per coached repository)*

1. **Inspect Repository Silently**:
   - Check if the workspace is an empty/new folder or an existing repository.
   - For an existing repository, inspect entry points, package manifests (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`), core directories, and test commands.
2. **Project Situation & Stack Familiarity**:
   - Call `question` to ask the developer's familiarity with this project's stack (`Beginner` / `Intermediate` / `Advanced`) and learning focus (`Whole system architecture & verification` / `Only the features and modules we touch`).
3. **Write Initial State & Show Compact System Map**:
   - Create `~/.agents/code-coach/projects/<project-slug>/project-map.md` and `progress.md` using [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md).
   - For an existing repo, show a compact 5–8 line ASCII/Mermaid flow of the verified components (marking uninspected or undecided links as `?`), then immediately transition to the developer's build or debugging task using `SKILL.md`.
