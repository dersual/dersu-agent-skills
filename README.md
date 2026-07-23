# dersu-agent-skills

A personal repository of agent skills and behavior rules for easy synchronization across different devices and environments.

## 📋 Behavioral Rules & System Setup

- [AGENTS.md](AGENTS.md): Project-scoped rules and behavioral guidelines (cloned from global `GEMINI.md`) containing strategies to reduce common LLM coding mistakes, ensuring epistemic safety, goal-driven execution, and surgical edits.
- [PLUGINS-AND-MCP.md](PLUGINS-AND-MCP.md): Setup and reference guide for environment MCP servers (`github`, `context7`, `StitchMCP`) and registered plugins (`modern-web-guidance-plugin`, `firebase`, `android-cli-plugin`).

---

## 🛠️ Active Skills

- **[caveman](skills/caveman/SKILL.md)**: Ultra-compressed, token-saving communication mode.
- **[code-tutor](skills/code-tutor/SKILL.md)**: Interactive tutor mode that teaches programming concepts step-by-step using small code chunks and checks understanding.
- **[diagnose](skills/diagnose/SKILL.md)**: Structured diagnosis loops for reproducing, isolating, and fixing bugs.
- **[find-skills](skills/find-skills/SKILL.md)**: CLI and workspace setup aid for discovering new capabilities.
- **[grill-me](skills/grill-me/SKILL.md)**: Interactive interviewing and plan stress-testing, resolving design decisions branch by branch.
- **[grill-with-docs](skills/grill-with-docs/SKILL.md)**: Refines implementation plans by stress-testing them against project docs.
- **[handoff](skills/handoff/SKILL.md)**: Generates clear, concise handoff notes for the next agent session.
- **[prototype](skills/prototype/SKILL.md)**: Build throwaway prototypes (logic state models or UI variations) to answer design questions fast.
- **[solid](skills/solid/SKILL.md)**: Elevates software design quality using SOLID principles and clean code methodologies.
- **[study-tutor](skills/study-tutor/SKILL.md)**: A generalized version of the tutor skill designed to patiently guide learning for any general academic topic or concept using analogies and active verification.
- **[teach](skills/teach/SKILL.md)**: Structured teaching and educational guidance.
- **[wayfinder](skills/wayfinder/SKILL.md)**: Plan large multi-session efforts as a shared map of decision tickets on an issue tracker.
- **[writing-great-skills](skills/writing-great-skills/SKILL.md)**: Reference and vocabulary for writing and editing predictable agent skills.
- **[zoom-out](skills/zoom-out/SKILL.md)**: Steps back to inspect code architecture and layout choices.

---

## ⚠️ Deprecated Skills

The following skills have been moved to the `deprecated/` directory because their functionality is superseded by [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills):

- **[branch-code-review](deprecated/branch-code-review/SKILL.md)**: Deprecated in favor of `code-review-and-quality` and the `code-reviewer` subagent from `addyosmani/agent-skills`.
- **[tdd](deprecated/tdd/SKILL.md)**: Deprecated in favor of `test-driven-development` and the `test-engineer` subagent from `addyosmani/agent-skills`.

---

## 📦 External Skills & Antigravity Plugins

We rely on [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) for standard software engineering workflows (e.g., TDD, code review, security audits, performance profiling).

### Installation Methods

> [!IMPORTANT]
> Standard installation via `npx skills add` only installs skill markdown definitions. If you are using **Google Antigravity / Gemini CLI**, install it as a **Plugin** so that its bundled **subagents** (`code-reviewer`, `security-auditor`, `test-engineer`, `web-performance-auditor`) are also loaded and registered!

#### 1. Antigravity / Gemini CLI Plugin Installation (Recommended for AGY)

To gain access to both skills and subagents in Antigravity:

```bash
# Clone into the Antigravity plugins directory:
git clone https://github.com/addyosmani/agent-skills.git ~/.gemini/config/plugins/agent-skills
```

Or via CLI plugin commands (if available in your AGY setup):

```bash
gemini plugin add addyosmani/agent-skills
# or
agy plugin add addyosmani/agent-skills
```

#### 2. General Agent Skills Installation

If you only need the skills globally across standard agent skill loaders:

```bash
npx skills add addyosmani/agent-skills -g --all
```

---

## 🚀 How to Synchronize This Repository

To install all active skills from this repository globally on any new machine:

```bash
npx skills add <username>/dersu-agent-skills -g --all
```
