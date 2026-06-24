# dersu-agent-skills

A personal repository of agent skills and behavior rules for easy synchronization across different devices and environments.

## 📋 Behavioral Rules

* [AGENTS.md](AGENTS.md): Project-scoped rules and behavioral guidelines (cloned from global `GEMINI.md`) containing strategies to reduce common LLM coding mistakes, ensuring epistemic safety, goal-driven execution, and surgical edits.

---

## 🛠️ Consolidated Skills

* **[caveman](skills/caveman/SKILL.md)**: Ultra-compressed, token-saving communication mode.
* **[diagnose](skills/diagnose/SKILL.md)**: Structured diagnosis loops for reproducing, isolating, and fixing bugs.
* **[find-skills](skills/find-skills/SKILL.md)**: CLI and workspace setup aid for discovering new capabilities.
* **[grill-with-docs](skills/grill-with-docs/SKILL.md)**: Refines implementation plans by stress-testing them against project docs.
* **[handoff](skills/handoff/SKILL.md)**: Generates clear, concise handoff notes for the next agent session.
* **[solid](skills/solid/SKILL.md)**: Elevates software design quality using SOLID principles and clean code methodologies.
* **[tdd](skills/tdd/SKILL.md)**: Implements test-driven development using the red-green-refactor workflow.
* **[teach](skills/teach/SKILL.md)**: Structured teaching and educational guidance.
* **[zoom-out](skills/zoom-out/SKILL.md)**: Steps back to inspect code architecture and layout choices.

---

## ✨ Custom Added Skills

* **[branch-code-review](skills/branch-code-review/SKILL.md)**: A skeptical code-review workflow for reviewing local changes, staged code, or commit ranges with distinct severity categories.
* **[code-tutor](skills/code-tutor/SKILL.md)**: An interactive tutor mode that teaches programming concepts step-by-step using small code chunks and checks understanding.
* **[study-tutor](skills/study-tutor/SKILL.md)**: A generalized version of the tutor skill designed to patiently guide learning for any general academic topic or concept using analogies and active verification.
* **[grill-me](skills/grill-me/SKILL.md)**: Interactive interviewing and plan stress-testing, resolving design decisions branch by branch.

---

## 🚀 How to Synchronize Skills

To install all the skills in this repository globally on any new machine, execute:

```bash
npx skills add <username>/dersu-agent-skills -g --all
```
