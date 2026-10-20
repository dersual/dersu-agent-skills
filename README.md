# dersu-agent-skills

A personal repository of agent skills and behavior rules for easy synchronization across different devices and environments.

## 📋 Behavioral Rules & System Setup

- [AGENTS.md](AGENTS.md): Project-scoped rules and behavioral guidelines (cloned from global `GEMINI.md`) containing strategies to reduce common LLM coding mistakes, ensuring epistemic safety, goal-driven execution, and surgical edits.
- [PLUGINS-AND-MCP.md](PLUGINS-AND-MCP.md): Setup and reference guide for environment MCP servers (`github`, `context7`, `StitchMCP`) and registered plugins (`modern-web-guidance-plugin`, `firebase`, `android-cli-plugin`).

---

## 🛠️ Local Skills (This Repository)

The 13 core custom skills stored locally in `skills/`:

- **[caveman](skills/caveman/SKILL.md)**: Ultra-compressed, token-saving communication mode.
- **[code-coach](skills/code-coach/SKILL.md)**: Strict senior technical lead mode that yields implementation legwork to the developer across Scaffold, Socratic, and Toy postures.
- **[code-tutor](skills/code-tutor/SKILL.md)**: Interactive tutor mode that teaches programming concepts step-by-step using small code chunks and checks understanding.
- **[find-skills](skills/find-skills/SKILL.md)**: CLI and workspace setup aid for discovering new capabilities.
- **[humanizer](skills/humanizer/SKILL.md)**: Converts technical, formal, or robotic text into natural, human-friendly prose.
- **[orwell-writing](skills/orwell-writing/SKILL.md)**: Draft, rewrite, edit, review, polish, copyedit, simplify, humanize, or create written prose using George Orwell's six rules and ASD-STE100 Simplified Technical English.
- **[refine-resume-bank](skills/refine-resume-bank/SKILL.md)**: Audits and refines project experiences into high-impact Master Resume Bullet Bank entries using strict software engineering standards.
- **[setup-permissions](skills/setup-permissions/SKILL.md)**: Interactively configures runtime permission boundaries (allow, ask, deny) for agent harnesses across workspaces, commands, and sensitive files.
- **[setup-standards](skills/setup-standards/SKILL.md)**: Scaffolds or standardizes repository coding standards (`CODING_STANDARDS.md`) and agent behavioral guidelines (`AGENTS.md`).
- **[study-tutor](skills/study-tutor/SKILL.md)**: A patient study tutor designed to patiently guide learning for any topic or concept using analogies and active verification.
- **[tailor-resume](skills/tailor-resume/SKILL.md)**: Generates a 1-page tailored LaTeX resume targeted at a specific job description or role by curating and prioritizing bullets from the Master Resume Bullet Bank.
- **[toggle-code-coach](skills/toggle-code-coach/SKILL.md)**: Toggles active code-coach mode in project instructions (`CLAUDE.md`, `GEMINI.md`, or `AGENTS.md`).
- **[zoom-out](skills/zoom-out/SKILL.md)**: Steps back to inspect code architecture and layout choices.

---

## 📦 External Skills Suite ([mattpocock/skills](https://github.com/mattpocock/skills))

We use [mattpocock/skills](https://github.com/mattpocock/skills) as our primary external skill set (replacing `addyosmani/agent-skills`). The 37 installed skills from this suite include:

- **ask-matt**: Ask Matt Pocock AI assistant for advice on TypeScript, web development, and agent workflows.
- **batch-grill-me**: Batch processing for grill-me plan stress-testing.
- **claude-handoff**: Generate handoff context formatted specifically for Claude and agent transitions.
- **code-review**: Systematic multi-axis code review.
- **codebase-design**: Design deep, clean module boundaries and interfaces for codebases.
- **design-an-interface**: Explore and generate multiple contrasting API/interface designs.
- **diagnosing-bugs**: Disciplined diagnosis loop for complex bugs and performance regressions.
- **domain-modeling**: Define and refine domain terminology, models, and ubiquitous language.
- **edit-article**: Refine and edit articles for clarity, flow, and impact.
- **grill-me**: Interactive interviewing and plan stress-testing, resolving design decisions branch by branch.
- **grill-with-docs**: Refine implementation plans by stress-testing them against project docs.
- **grilling**: Relentlessly stress-test plans, architecture decisions, and ideas.
- **handoff**: Structured handoff notes for next agent session.
- **implement**: Drive end-to-end task implementation with verification steps.
- **improve-codebase-architecture**: Analyze and refactor codebase architecture for maintainability.
- **loop-me**: Keep agent in execution loop until goals/tests are verified.
- **prototype**: Build throwaway prototypes (logic state models or UI variations) to answer design questions fast.
- **qa**: Conversational QA and bug logging session.
- **research**: Conduct deep background research against official documentation and primary sources.
- **resolving-merge-conflicts**: Guided resolution of git merge and rebase conflicts.
- **scaffold-exercises**: Create exercise directory structures with sections, problems, solutions, and explainers.
- **setup-matt-pocock-skills**: Skill installer and setup helper for Matt Pocock's skills repository.
- **setup-pre-commit**: Configure pre-commit hooks (Husky, lint-staged, Prettier, tests).
- **tdd**: Test-driven development workflow (red-green-refactor loop).
- **teach**: Structured teaching and educational guidance.
- **to-questionnaire**: Convert ambiguous ideas into structured clarification questionnaires.
- **to-spec**: Turn user requests and ideas into comprehensive technical specifications.
- **to-tickets**: Break down specs and plans into actionable, trackable task tickets.
- **triage**: Triage incoming bugs, requests, and issue reports.
- **wait-what**: Halt and request user clarification when facing ambiguity or confusion.
- **wayfinder**: Plan large multi-session efforts as a shared map of decision tickets on an issue tracker.
- **wizard**: Interactive step-by-step setup wizard for features and configs.
- **writing-beats**: Structure prose and technical documentation using narrative beats.
- **writing-for-agents**: Create and edit predictable agent skills and guidance documents.
- **writing-fragments**: Draft modular prose fragments for documentation and essays.
- **writing-great-skills**: Reference and vocabulary for writing and editing predictable agent skills.
- **writing-shape**: Outline overall document flow and structural shape before writing.

---

## ⚠️ Deprecated Skills

The following skills in `deprecated/` are superseded by [mattpocock/skills](https://github.com/mattpocock/skills):

- **[branch-code-review](deprecated/branch-code-review/SKILL.md)**: Deprecated in favor of `code-review` from `mattpocock/skills`.
- **[solid](deprecated/solid/SKILL.md)**: Deprecated in favor of `setup-standards`, `CODING_STANDARDS.md`, and `code-review`.
- **[tdd](deprecated/tdd/SKILL.md)**: Deprecated in favor of `tdd` from `mattpocock/skills`.

---

## 🚀 Installation & Synchronization

To install external skills from `mattpocock/skills` globally:

```bash
npx skills add mattpocock/skills
```

To synchronize local skills from this repository:

```bash
npx skills add dersual/dersu-agent-skills
```
