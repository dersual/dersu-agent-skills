# Code Coach Lifecycle, Toggling & Onboarding

Manage all activation pointers and learner notes inside the user's home directory (`~`, e.g., `C:\Users\<user>\` on Windows or `/Users/<user>/` on macOS/Linux) as defined in [`SKILL.md`](SKILL.md).

---

## 1. Home-Directory Global Instruction Files & Delimited Pointer Block

To allow every agent harness to auto-detect whether `code-coach` is active on turn 1 with **zero extra file reads in non-coached repos**, `code-coach` maintains a single delimited block at the bottom of each global instruction file whose parent config directory exists on the machine:

- **OpenCode**: `~/.config/opencode/AGENTS.md`
- **Claude Code**: `~/.claude/CLAUDE.md`
- **Gemini CLI / Antigravity**: `~/.gemini/GEMINI.md`
- **Codex**: `~/.codex/AGENTS.md`

### Exact Delimited Block Format

Create the markdown file if its parent config folder exists, and preserve all unrelated global instructions outside the `<!-- code-coach:start --> ... <!-- code-coach:end -->` tags:

```markdown
<!-- code-coach:start -->
## Code Coach Active Scope
Active workspaces:
- `<absolute-path-to-project-root>`
Paused workspaces:
- None

Rule: When the current working directory equals or is a subdirectory of any path under `Active workspaces` (or when `- ALL` is listed) AND is not under `Paused workspaces` (matching path-segment boundaries case-insensitively and ignoring `/` vs `\` differences), invoke and strictly follow the `code-coach` skill before generating code, designing features, debugging errors, or explaining concepts. In all other directories, ignore this block completely.
<!-- code-coach:end -->
```

When **no** workspaces are active (e.g., `/code-coach off` removed the last active workspace and `- ALL` is not set), remove the entire `<!-- code-coach:start --> ... <!-- code-coach:end -->` block from the Section 1 global instruction files.

---

## 2. Lifecycle Subcommands (`on`, `off`, `pause`, `global`, `status`, `reset`)

### A. `/code-coach on` (or enabling in an unregistered/paused workspace)
1. Resolve `<project-root>` and `<project-slug>` per `SKILL.md` Section 1.
2. Update the delimited block across all present Section 1 global instruction files:
   - Add `<project-root>` under `Active workspaces:` (unless `- ALL` is already set).
   - Remove `<project-root>` from `Paused workspaces:` if present.
3. If `~/.agents/code-coach/projects/<project-slug>/progress.md` exists, set `Learning mode: active` at the top of `progress.md`.
4. If `~/.agents/code-coach/profile.md` or `~/.agents/code-coach/projects/<project-slug>/project-map.md` is missing (or `Onboarding: incomplete`), run **Section 3 (Interactive Onboarding)** below.
5. Confirm the active state, the project's active `Implementation Gear` and `Checkpoint frequency`, and the updated global instruction files in 2 sentences.

### B. `/code-coach global`
1. In the Section 1 global instruction files, set `Active workspaces:` to `- ALL` and `Paused workspaces:` to `- None`.
2. Confirm that global `code-coach` mode is active across all workspaces.

### C. `/code-coach off` / `/code-coach pause`
1. Resolve `<project-root>` and `<project-slug>`.
2. In the Section 1 global instruction files:
   - If `Active workspaces:` lists specific paths, remove `<project-root>` from `Active workspaces:` (and remove the entire delimited block if no active paths remain).
   - If `Active workspaces:` is `- ALL`, ask via the native `question` tool:
     - `1. Pause Code Coach for this project only (Add this project to Paused workspaces and keep ALL active elsewhere) (Recommended)`
     - `2. Disable global ALL mode across all projects`
3. If `~/.agents/code-coach/projects/<project-slug>/progress.md` exists, set `Learning mode: paused` at the top of `progress.md` while keeping all saved notes intact.
4. Output a 1-sentence confirmation that `code-coach` is now disabled/paused for this workspace.

### D. `/code-coach status`
1. Read the Section 1 global instruction block, `~/.agents/code-coach/profile.md`, and `~/.agents/code-coach/projects/<project-slug>/` (if present).
2. Display a concise status summary:
   - Current workspace status (**Active** or **Inactive/Paused**).
   - Registered `Active workspaces` and `Paused workspaces`.
   - **This Project's Coaching Preferences** from `project-map.md` (`Implementation Gear`, `Checkpoint frequency`, `Question style`, `Learning scope`), plus global defaults from `profile.md`.
   - Any open `## Pending decision` in the current project's `progress.md`.
3. Call the native `question` tool to offer quick adjustments:
   - `Toggle current workspace On/Off`
   - `Change this project's Implementation Gear (Architect / Guided Pair / Hands-On)`
   - `Change this project's Checkpoint frequency (Light / Normal / Frequent) or Question style`
   - `Change global default preferences in profile.md`
   - `Continue coding`

### E. `/code-coach reset`
1. Show the exact path to `~/.agents/code-coach/projects/<project-slug>/` and ask via the native `question` tool:
   - `1. Cancel (Keep current project learning notes)`
   - `2. Reset this project's notes & preferences (Backup project-map.md and progress.md to backups/ and re-run project onboarding)`
   - `3. Reset this project's notes AND global profile.md`
2. On confirmation, copy existing markdown files into `~/.agents/code-coach/projects/<project-slug>/backups/<timestamp>/` before writing fresh templates from [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md).

---

## 3. Interactive Onboarding (One Question at a Time via Native `question` Tool)

Read [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md) before writing state files. Ask questions one screen at a time using the native `question` tool.

### Phase 1: Global Developer Profile (`~/.agents/code-coach/profile.md`)
*(Run only once across the machine; skip if `~/.agents/code-coach/profile.md` already has `Onboarding: complete`)*

1. **Overall Programming Experience**:
   - Call `question`:
     - `Intermediate (Explore interactions, trade-offs, and system seams)`
     - `Beginner (Explain unfamiliar pieces, use diagrams, smaller reasoning steps)`
     - `Advanced (Probe hard constraints, concurrency/failure modes, and design assumptions)`
2. **Global Default Preferences** (used as defaults when onboarding new projects, overridable per project):
   - Call `question`:
     - `Guided Pair + Normal Open-Ended Checkpoints (Recommended)`
     - `Architect (VibeWise: You design, AI writes + Verification Audit) + Normal Checkpoints`
     - `Hands-On (Strict TODO Scaffolds) + Normal Checkpoints`
     - `Customize global defaults (Pick Gear, Light/Normal/Frequent, Open-ended/Mixed/Multiple choice)`
3. Write `~/.agents/code-coach/profile.md` using [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md).

### Phase 2: Per-Project Onboarding & Preferences (`~/.agents/code-coach/projects/<project-slug>/`)
*(Run once per coached repository so each project gets its own tailored gear, frequency, and map)*

1. **Inspect Repository Silently**:
   - Check if `<project-root>` is a new/empty folder or an existing repository.
   - For an existing repository, inspect entry points, package manifests (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`), core directories, and test commands.
2. **Stack Familiarity & Learning Scope for This Project**:
   - Call `question`:
     - `Intermediate stack familiarity — Coach me on modules & features we touch (Recommended)`
     - `Beginner / New to this stack — Coach me on whole-system architecture & fundamentals`
     - `Advanced / Familiar with this stack — Probe deep trade-offs, edge cases, and failure modes`
3. **Project Coaching Preferences (`Implementation Gear`, `Checkpoint frequency`, `Question style`)**:
   - Call `question` so the developer can tailor coaching intensity to *this specific project*:
     - `Use my global defaults from profile.md (<Default Gear>, <Default Frequency>, <Default Style>) (Recommended)`
     - `Architect Gear for this project (You design, AI writes code & tests + Verification Audit)`
     - `Guided Pair Gear for this project (AI writes plumbing & failing Red tests; you write core logic)`
     - `Hands-On Gear for this project (AI outputs structural TODO scaffolds only; you write logic & tests)`
   - If the developer wants to customize `Checkpoint frequency` (`Light` / `Normal` / `Frequent`) or `Question style` (`Open-ended` / `Mixed` / `Multiple choice`) for this project, ask in a follow-up picker and save to `project-map.md`.
4. **Write Project State & Show Compact System Map**:
   - Create `~/.agents/code-coach/projects/<project-slug>/project-map.md` and `progress.md` using [`STATE-TEMPLATES.md`](STATE-TEMPLATES.md).
   - For an existing repo, show a compact 5–8 line ASCII/Mermaid flow of the verified components (marking uninspected or undecided links as `?`), then immediately begin the developer's task using [`SKILL.md`](SKILL.md).
   - **Completion Criterion**: `<project-root>` is registered in the Section 1 global instruction files, `~/.agents/code-coach/profile.md`, `project-map.md`, and `progress.md` exist on disk with `Onboarding: complete` and `Learning mode: active`, and execution has transitioned to the developer's task.
