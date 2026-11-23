# Code Coach Home-Directory State Templates

Create and maintain these Markdown files inside `~/.agents/code-coach/`. Never write them inside the project repository unless the developer explicitly asks to export a decision log or ADR into the repo.

```text
~/.agents/code-coach/
├── profile.md                              # Shared across all projects on this machine
└── projects/
    └── <project-slug>/
        ├── project-map.md                  # Architecture, components, verification commands, unknowns
        ├── progress.md                     # Pending decision + evidenced engineering reasoning & decision log
        └── backups/                        # Timestamped snapshots created before /code-coach reset
```

---

## 1. `~/.agents/code-coach/profile.md`

Keep `profile.md` a compact snapshot of current preferences and cross-project mastery. Update existing entries in place rather than appending endless history.

```markdown
# Developer Coaching Profile

Onboarding: complete

## Experience
Overall programming: [Beginner / Intermediate / Advanced]
Stack familiarity: [e.g., TypeScript: Intermediate, Python: Intermediate, Rust: Beginner]

## Coaching Preferences
Default Implementation Gear: [Guided Pair / Architect / Hands-On]
Checkpoint frequency: [Normal / Light / Frequent]
Question style: [Open-ended / Mixed / Multiple choice]
Verification Audit: [Active]

## Strong Concepts (Evidenced Across Projects)
- None recorded yet.

## Developing Concepts
- None recorded yet.

## Revisit (Weak Spots & Past Failure Modes)
- None recorded yet.
```

---

## 2. `~/.agents/code-coach/projects/<project-slug>/project-map.md`

Distinguish **Proposed**, **Chosen**, **Implemented**, and **Unknown (`?`)** components. Never fill in unagreed architecture silently.

```markdown
# Project Map: <project-name>

Workspace path: `<absolute-path-to-repo>`
Situation: [New project / Existing repo]
Learning scope: [Whole system / Modules we touch]

## Purpose & Requirements
- [What the software does and user constraints. Requirements do not automatically settle technical design.]

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

## 3. `~/.agents/code-coach/projects/<project-slug>/progress.md`

While waiting on any checkpoint, maintain `## Pending decision` at the top so session restarts or context compaction never bypass an open design or implementation gate. Remove `## Pending decision` once resolved and record the outcome in the Decision & Reasoning Log below.

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
<!-- Group by ## Topic. Distinguish:
- Introduced / Explained by AI (Toy Examples & Concepts)
- Demonstrated by Developer (open-ended reasoning, bug diagnosis, Hands-On / Guided Pair code, or Verification Audit findings)
- Needs Reinforcement (missed boundary conditions, race conditions, or skipped checks)
Never record button clicks or product wishes as demonstrated engineering mastery. -->
```
