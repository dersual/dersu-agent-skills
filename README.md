# dersu-agent-skills

A unified, self-contained suite of agent skills, engineering workflows, and behavioral rules.

All skills are maintained directly in `skills/` with zero external repository dependencies.

---

## 📋 Behavioral Rules & System Setup

- [AGENTS.md](AGENTS.md): Project-scoped rules and behavioral guidelines containing strategies to reduce common LLM coding mistakes, ensuring epistemic safety, goal-driven execution, and surgical edits.
- [PLUGINS-AND-MCP.md](PLUGINS-AND-MCP.md): Setup and reference guide for environment MCP servers (`github`, `context7`, `StitchMCP`) and registered plugins (`modern-web-guidance-plugin`, `firebase`, `android-cli-plugin`).
- [docs/research/ai-skills-ecosystem-comparison-and-workflow-synthesis.md](docs/research/ai-skills-ecosystem-comparison-and-workflow-synthesis.md): Definitive comparative analysis across Pocock, Osmani, Tan (`pstack`), and Google Elephant-Goldfish, detailing the architectural foundation and empirical autopsies.

---

## 🛠️ Complete Skill Catalog (Flat 4-Tier Architecture)

### Tier 1: Core Engineering Lifecycle

The end-to-end software delivery pipeline, hardened with Google Elephant-Goldfish, Addy Osmani's Anti-Rationalization Table, and Lauren Tan's proof-or-dismiss verification:

- **[orchestrate](skills/orchestrate/SKILL.md)**: Opt-in top-level router mapping tasks to Feature, Bugfix, Refactor, or Research playbooks.
- **[grill-me](skills/grill-me/SKILL.md)**: Interactive interviewing and plan stress-testing, resolving design decisions branch by branch.
- **[to-spec](skills/to-spec/SKILL.md)**: Turns conversation context into technical specs at the observable seam. Enforces the Elephant Zero-Code Invariant.
- **[spec-audit](skills/spec-audit/SKILL.md)**: Stateless, amnesiac cold audit (The Goldfish) stress-testing specifications against the Five Axes before ticketing.
- **[to-tickets](skills/to-tickets/SKILL.md)**: Decomposes approved specifications into tracer-bullet vertical slices with explicit blocking DAG edges (and Expand-Contract for wide refactors).
- **[implement](skills/implement/SKILL.md)**: Strict TDD task implementation governed by the Anti-Rationalization Table, optional `--arena` mode, and `prove-it-works` terminal output.
- **[diagnosing-bugs](skills/diagnosing-bugs/SKILL.md)**: Disciplined diagnosis loop for complex defects, race conditions, and regressions (tight red loop <5s, root-cause trace, zero symptom papering).
- **[code-review](skills/code-review/SKILL.md)**: Two-axis review (Standards vs. Spec) via parallel subagents, evaluated against Section 5 Five-Axis criteria and the Lauren Tan Proof-or-Dismiss Rule.
- **[retro](skills/retro/SKILL.md)**: Session retrospective analyzing defects and hard lessons to update linter rules, tests, and documentation.

---

### Tier 2: Auxiliary Engineering & Architecture

Supporting architecture, refactoring, workspace setup, and delivery skills:

- **[arena](skills/arena/SKILL.md)**: Authentic tournament engine spawning parallel candidates across isolated Git worktrees, cross-judging against rubrics, and grafting optimal components.
- **[codebase-design](skills/codebase-design/SKILL.md)**: Design deep, clean module boundaries and interfaces for codebases (John Ousterhout philosophy).
- **[domain-modeling](skills/domain-modeling/SKILL.md)**: Define and refine ubiquitous domain terminology (`GLOSSARY.md`) and architecture decision records (`docs/adr/`).
- **[improve-codebase-architecture](skills/improve-codebase-architecture/SKILL.md)**: Analyzes git churn and complexity hotspots, generating interactive visual HTML maps.
- **[setup-repo](skills/setup-repo/SKILL.md)**: Unified workspace initializer configuring issue trackers (GitHub or local markdown), triage labels, domain docs, and standards.
- **[setup-standards](skills/setup-standards/SKILL.md)**: Scaffolds `CODING_STANDARDS.md` (Code Judo, Anti-Slop, Five-Axis Quality Contract, Anti-Rationalization Table) and `AGENTS.md`.
- **[setup-permissions](skills/setup-permissions/SKILL.md)**: Interactively configures runtime permission boundaries (allow, ask, deny) for agent harnesses.
- **[setup-pre-commit](skills/setup-pre-commit/SKILL.md)**: Configures pre-commit hooks (Husky, lint-staged, Prettier, tests).
- **[tdd](skills/tdd/SKILL.md)**: Test-driven development workflow and mocking reference guidelines.
- **[pr](skills/pr/SKILL.md)**: Drafts concise, high-signal pull request descriptions from git diffs.
- **[prototype](skills/prototype/SKILL.md)**: Builds throwaway spikes (logic state models or UI variations) to answer design questions fast.
- **[wizard](skills/wizard/SKILL.md)**: Generates interactive bash wizards that guide humans through steps only they can perform.
- **[triage](skills/triage/SKILL.md)**: Triages incoming bug reports and feature requests against project scope.
- **[resolving-merge-conflicts](skills/resolving-merge-conflicts/SKILL.md)**: Guided resolution of in-progress git merge and rebase conflicts.
- **[wait-what](skills/wait-what/SKILL.md)**: Pauses execution and requests clarification when encountering fundamental ambiguities.
- **[loop-me](skills/loop-me/SKILL.md)**: Keeps agent in an automated execution loop until tests pass.
- **[wayfinder](skills/wayfinder/SKILL.md)**: Maps complex multi-session efforts into a shared ticket DAG.
- **[zoom-out](skills/zoom-out/SKILL.md)**: Steps back to inspect code architecture and layout choices.

---

### Tier 3: Education & Skill Development

Pedagogical skills designed to teach, tutor, lead, and verify understanding:

- **[code-coach](skills/code-coach/SKILL.md)**: Strict technical lead mode that yields implementation legwork to the developer across Scaffold, Socratic, and Toy postures.
- **[code-tutor](skills/code-tutor/SKILL.md)**: Interactive tutor mode teaching programming concepts step-by-step using small code chunks and comprehension checks.
- **[study-tutor](skills/study-tutor/SKILL.md)**: Patient study tutor guiding learning for academic subjects and complex concepts using analogies and active verification.
- **[show-me](skills/show-me/SKILL.md)**: Visualizes topics with concise diagrams, code-shape sketches, and focused HTML artifacts.
- **[scaffold-exercises](skills/scaffold-exercises/SKILL.md)**: Generates structured exercise directories with problems, solutions, and explainers.
- **[teach](skills/teach/SKILL.md)**: Structured curriculum and educational mission builder.
- **[toggle-code-coach](skills/toggle-code-coach/SKILL.md)**: Toggles active code-coach mode in project instructions (`AGENTS.md` or `CLAUDE.md`).
- **[ask-me](skills/ask-me/SKILL.md)**: Router over the skills in this repository.

---

### Tier 4: Writing & Anti-Slop

High-signal writing, editing, and research skills:

- **[humanizer](skills/humanizer/SKILL.md)**: Rewrites AI-sounding text into natural human prose without altering underlying meaning.
- **[orwell-writing](skills/orwell-writing/SKILL.md)**: Prose drafting and editing guided by George Orwell's six rules and ASD-STE100 Simplified Technical English.
- **[caveman](skills/caveman/SKILL.md)**: Ultra-compressed communication mode cutting token consumption ~75% while maintaining technical precision.
- **[writing-for-agents](skills/writing-for-agents/SKILL.md)**: Guides the creation and editing of agent skills and behavior specifications.
- **[writing-beats](skills/writing-beats/SKILL.md)**: Structures technical documents and prose using narrative beats.
- **[writing-fragments](skills/writing-fragments/SKILL.md)**: Drafts modular prose fragments for technical documentation.
- **[writing-shape](skills/writing-shape/SKILL.md)**: Outlines document hierarchy and flow before drafting prose.
- **[to-questionnaire](skills/to-questionnaire/SKILL.md)**: Converts ambiguous ideas into structured clarification questionnaires.
- **[find-skills](skills/find-skills/SKILL.md)**: Workspace setup aid for discovering and installing agent skills.
- **[research](skills/research/SKILL.md)**: Conducts deep background investigations against primary sources and official documentation.

---

## 🚀 Installation & Synchronization

To synchronize the entire flat suite into any agent environment:

```bash
npx skills add dersual/dersu-agent-skills
```
