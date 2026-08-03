# dersu-agent-skills

A personal repository of agent skills and behavior rules for easy synchronization across different devices and environments.

## 📋 Behavioral Rules & System Setup

- [AGENTS.md](AGENTS.md): Project-scoped rules and behavioral guidelines (cloned from global `GEMINI.md`) containing strategies to reduce common LLM coding mistakes, ensuring epistemic safety, goal-driven execution, and surgical edits.
- [PLUGINS-AND-MCP.md](PLUGINS-AND-MCP.md): Setup and reference guide for environment MCP servers (`github`, `context7`, `StitchMCP`) and registered plugins (`modern-web-guidance-plugin`, `firebase`, `android-cli-plugin`).

---

## 🛠️ Local Skills (This Repository)

The 16 core custom skills stored locally in `skills/`:

- **[caveman](skills/caveman/SKILL.md)**: Ultra-compressed, token-saving communication mode.
- **[code-tutor](skills/code-tutor/SKILL.md)**: Interactive tutor mode that teaches programming concepts step-by-step using small code chunks and checks understanding.
- **[diagnose](skills/diagnose/SKILL.md)**: Structured diagnosis loops for reproducing, isolating, and fixing bugs.
- **[find-skills](skills/find-skills/SKILL.md)**: CLI and workspace setup aid for discovering new capabilities.
- **[grill-me](skills/grill-me/SKILL.md)**: Interactive interviewing and plan stress-testing, resolving design decisions branch by branch.
- **[grill-with-docs](skills/grill-with-docs/SKILL.md)**: Refines implementation plans by stress-testing them against project docs.
- **[handoff](skills/handoff/SKILL.md)**: Generates clear, concise handoff notes for the next agent session.
- **[humanizer](skills/humanizer/SKILL.md)**: Converts technical, formal, or robotic text into natural, human-friendly prose.
- **[orwell-writing](skills/orwell-writing/SKILL.md)**: Draft, rewrite, edit, review, polish, copyedit, simplify, humanize, or create written prose using George Orwell's six rules and ASD-STE100 Simplified Technical English.
- **[prototype](skills/prototype/SKILL.md)**: Build throwaway prototypes (logic state models or UI variations) to answer design questions fast.
- **[solid](skills/solid/SKILL.md)**: Elevates software design quality using SOLID principles and clean code methodologies.
- **[study-tutor](skills/study-tutor/SKILL.md)**: A patient study tutor designed to patiently guide learning for any topic or concept using analogies and active verification.
- **[teach](skills/teach/SKILL.md)**: Structured teaching and educational guidance.
- **[wayfinder](skills/wayfinder/SKILL.md)**: Plan large multi-session efforts as a shared map of decision tickets on an issue tracker.
- **[writing-great-skills](skills/writing-great-skills/SKILL.md)**: Reference and vocabulary for writing and editing predictable agent skills.
- **[zoom-out](skills/zoom-out/SKILL.md)**: Steps back to inspect code architecture and layout choices.

---

## 📦 External Skills Suite ([mattpocock/skills](https://github.com/mattpocock/skills))

We use [mattpocock/skills](https://github.com/mattpocock/skills) as our primary external skill set (replacing `addyosmani/agent-skills`). The 26 installed skills from this suite include:

- **ask-matt**: Ask Matt Pocock AI assistant for advice on TypeScript, web development, and agent workflows.
- **batch-grill-me**: Batch processing for grill-me plan stress-testing.
- **claude-handoff**: Generate handoff context formatted specifically for Claude and agent transitions.
- **codebase-design**: Design deep, clean module boundaries and interfaces for codebases.
- **code-review**: Systematic multi-axis code review.
- **design-an-interface**: Explore and generate multiple contrasting API/interface designs.
- **diagnosing-bugs**: Disciplined diagnosis loop for complex bugs and performance regressions.
- **domain-modeling**: Define and refine domain terminology, models, and ubiquitous language.
- **edit-article**: Refine and edit articles for clarity, flow, and impact.
- **grilling**: Relentlessly stress-test plans, architecture decisions, and ideas.
- **implement**: Drive end-to-end task implementation with verification steps.
- **improve-codebase-architecture**: Analyze and refactor codebase architecture for maintainability.
- **qa**: Conversational QA and bug logging session.
- **research**: Conduct deep background research against official documentation and primary sources.
- **resolving-merge-conflicts**: Guided resolution of git merge and rebase conflicts.
- **setup-matt-pocock-skills**: Skill installer and setup helper for Matt Pocock's skills repository.
- **setup-pre-commit**: Configure pre-commit hooks (Husky, lint-staged, Prettier, tests).
- **tdd**: Test-driven development workflow (red-green-refactor loop).
- **to-questionnaire**: Convert ambiguous ideas into structured clarification questionnaires.
- **to-spec**: Turn user requests and ideas into comprehensive technical specifications.
- **to-tickets**: Break down specs and plans into actionable, trackable task tickets.
- **triage**: Triage incoming bugs, requests, and issue reports.
- **wizard**: Interactive step-by-step setup wizard for features and configs.
- **writing-beats**: Structure prose and technical documentation using narrative beats.
- **writing-fragments**: Draft modular prose fragments for documentation and essays.
- **writing-shape**: Outline overall document flow and structural shape before writing.

---

## ⚠️ Deprecated Skills

The following skills in `deprecated/` are superseded by [mattpocock/skills](https://github.com/mattpocock/skills):

- **[branch-code-review](deprecated/branch-code-review/SKILL.md)**: Deprecated in favor of `code-review` from `mattpocock/skills`.
- **[tdd](deprecated/tdd/SKILL.md)**: Deprecated in favor of `tdd` from `mattpocock/skills`.

---

## 🚀 Installation & Synchronization

To install external skills from `mattpocock/skills` globally:

```bash
npx skills add mattpocock/skills -g --all
```

To synchronize local skills from this repository:

```bash
npx skills add <username>/dersu-agent-skills -g --all
```
