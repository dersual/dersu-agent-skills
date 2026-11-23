# Code Coach Home-Directory State Templates

Maintain these Markdown files inside `~/.agents/code-coach/` as specified in [`SKILL.md`](SKILL.md).

```text
~/.agents/code-coach/
├── profile.md                              # Global experience, default preferences & cross-project concept mastery
└── projects/
    └── <project-slug>/
        ├── project-map.md                  # Per-project coaching preferences, architecture map, test commands & unknowns
        ├── progress.md                     # Pending decision + project decision log & evidenced reasoning
        └── backups/                        # Timestamped snapshots created before /code-coach reset
```

---

## 1. `~/.agents/code-coach/profile.md` (Global Developer Profile)

Keep `profile.md` a compact snapshot of cross-project experience, global default preferences, and evidenced mastery across repositories.

```markdown
# Developer Coaching Profile

Onboarding: complete

## Experience
Overall programming: [Beginner / Intermediate / Advanced]
Stack familiarity across languages: [e.g., TypeScript: Intermediate, Python: Intermediate, Rust: Beginner]

## Global Default Preferences (Inherited by new projects unless overridden in project-map.md)
Default Implementation Gear: [Guided Pair / Architect / Hands-On]
Default Checkpoint frequency: [Normal / Light / Frequent]
Default Question style: [Open-ended / Mixed / Multiple choice]

## Strong Concepts (Evidenced Across Projects)
- None recorded yet.

## Developing Concepts
- None recorded yet.

## Revisit (Weak Spots & Past Failure Modes)
- None recorded yet.
```

---

## 2. `~/.agents/code-coach/projects/<project-slug>/project-map.md` (Per-Project Preferences & Architecture Map)

Each project stores its own active coaching preferences (`Implementation Gear`, `Checkpoint frequency`, `Question style`, `Stack familiarity`, `Learning scope`) so a fast side-project can run `Architect` + `Light` while a core learning repo runs `Guided Pair` or `Hands-On` + `Normal`/`Frequent`.

```markdown
# Project Map: <project-name>

Workspace path: `<absolute-path-to-repo>`
Situation: [New project / Existing repo]

## Project Coaching Preferences (Active for This Repository)
Stack familiarity for this project: [Beginner / Intermediate / Advanced]
Learning scope: [Whole system / Modules we touch]
Active Implementation Gear: [Guided Pair / Architect / Hands-On]
Checkpoint frequency: [Normal / Light / Frequent]
Question style: [Open-ended / Mixed / Multiple choice]
Verification Audit: Active

## Purpose & Requirements
- [What the software does and user constraints.]

## Components & Seams
- [Component name (`path/to/file`) — Status: Implemented | Chosen | Proposed — Responsibility]

## Main Flow
```text
[Compact diagram with labeled arrows; mark undecided or unverified links with ?]
```

## Data, Concurrency & Trust Boundaries
- [Storage model, ownership, auth, external network/API boundaries, race/timeout risks; mark Unknown when unverified.]

## Verification & Test Commands
- Unit / Integration test runner: `[exact command, or Unknown]`
- E2E / System check: `[exact command, or Unknown]`
- Typecheck / Linter: `[exact command, or Unknown]`

## Open Architectural Unknowns
- [Unresolved technical choices that still require a Build Checkpoint before implementation.]
```

---

## 3. `~/.agents/code-coach/projects/<project-slug>/progress.md` (Project Progress & Pending Checkpoint)

While waiting on any checkpoint, maintain `## Pending decision` at the top so session restarts or context compaction resume at that exact gate.

```markdown
# Learning & Engineering Progress: <project-name>

Learning mode: active

## Pending decision
None.
<!-- When a checkpoint is awaiting a response, replace "None." with:
Checkpoint: [Build checkpoint | Design checkpoint | Implementation checkpoint | Debug checkpoint | Verification Audit]
Decision name: [title]
Stage: [awaiting open-ended reasoning | awaiting design confirmation | awaiting gear & implementation approval | awaiting bug diagnosis | awaiting diff audit]
Proposed scope / context: [1-2 sentences on what is being decided]
-->

## Decision & Verification Log
<!-- Record concrete architectural decisions, alternatives rejected, and how each slice was verified. -->
- None recorded yet.

## Evidenced Concept Mastery
<!-- Group by ## Topic with bullets under:
- Introduced / Explained by AI (Toy Examples & Concepts)
- Demonstrated by Developer (reasoning, bug diagnosis, Hands-On / Guided Pair code, or Verification Audit findings)
- Needs Reinforcement (missed boundary conditions, race conditions, or skipped checks) -->
```
