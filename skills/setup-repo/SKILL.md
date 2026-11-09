---
name: setup-repo
description: "Configure this repo for the engineering harness: set up its issue tracker, triage label vocabulary, domain doc layout (GLOSSARY.md & ADRs), and coding standards (CODING_STANDARDS.md) with anti-rationalization guards."
disable-model-invocation: true
---

# Setup Repo

Scaffold the per-repo configuration that the engineering skills assume:

- **Issue tracker**: where issues live (GitHub by default; local markdown is also supported out of the box).
- **Triage labels**: the strings used for the five canonical triage roles.
- **Domain docs**: where `GLOSSARY.md` and ADRs live, and the consumer rules for reading them.
- **Coding standards**: `CODING_STANDARDS.md` with the Five-Axis Quality Contract and Anti-Rationalization Table.
- **Agent steering**: `AGENTS.md` with clear pointers.

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists; don't assume:

- `git remote -v` and `.git/config`: is this a GitHub repo? Which one?
- `AGENTS.md` and `CLAUDE.md` at the repo root: does either exist? Is there already an `## Agent skills` section in either?
- `GLOSSARY.md` and `GLOSSARY-MAP.md` at the repo root, and any legacy `CONTEXT.md`. If a legacy file exists, offer to `git mv` it to `GLOSSARY.md`.
- `docs/adr/` and any architecture decision records.
- `CODING_STANDARDS.md` at the repo root.
- `docs/agents/`: does this skill's prior output already exist?
- `.scratch/`: a sign that a local-markdown issue tracker convention is already in use.
- Is the `triage` skill installed? This decides whether Section B runs.
- Monorepo signals: `pnpm-workspace.yaml`, `workspaces` in `package.json`, or populated `packages/*`.

### 2. Present findings and ask

Summarise what's present and what's missing. Then take the sections in order.

**Section A: Issue tracker.**
Default posture: these skills work cleanly with GitHub or Local Markdown:
- **GitHub**: issues live in the repo's GitHub Issues (uses `gh` CLI).
- **GitLab**: issues live in GitLab Issues (uses `glab` CLI).
- **Local markdown**: issues live as files under `.scratch/<feature>/issues/<NN>-<slug>.md` (ideal for local-first, offline, or solo projects).
- **Other** (Linear, Jira): record freeform prose in `docs/agents/issue-tracker.md`.

Record the choice in `docs/agents/issue-tracker.md`.

**Section B: Triage label vocabulary.**
Ask:
> Do you want to keep the default triage labels? (recommended: **yes**)

Defaults: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`.

**Section C: Domain docs.**
Default to single-context: one `GLOSSARY.md` at repo root + `docs/adr/`.
Offer multi-context only when monorepo signals are present.

**Section D: Coding standards.**
Check if `CODING_STANDARDS.md` exists. If not, copy the template from `skills/setup-standards/templates/CODING_STANDARDS.md` with:
- Structure & Simplicity (Code Judo)
- Types & Boundary Invariants
- Anti-Slop Guidelines
- Tests & Seams
- Five-Axis Quality Contract & Anti-Rationalization Table

### 3. Confirm and edit

Show the user a draft of:
- The `## Agent skills` block to add to `AGENTS.md` (or `CLAUDE.md`).
- The contents of `docs/agents/issue-tracker.md`, `docs/agents/domain.md`, and `docs/agents/triage-labels.md`.
- `CODING_STANDARDS.md` draft.

Let them edit before writing.

### 4. Write

Write the docs files using the seed templates:
- [issue-tracker-github.md](./issue-tracker-github.md): GitHub issue tracker
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md): GitLab issue tracker
- [issue-tracker-local.md](./issue-tracker-local.md): local-markdown issue tracker
- [triage-labels.md](./triage-labels.md): label mapping (only if `triage` is installed)
- [domain.md](./domain.md): domain doc consumer rules + layout

Append or update the `## Agent skills` block in `AGENTS.md` (or `CLAUDE.md`):

```markdown
## Agent skills

### Issue tracker
[one-line summary of where issues are tracked]. See `docs/agents/issue-tracker.md`.

### Triage labels
[one-line summary of the label vocabulary]. See `docs/agents/triage-labels.md`.

### Domain docs
[one-line summary of layout]. See `docs/agents/domain.md`.
```

### 5. Done

Report that repo setup is complete and engineering skills are wired up.
