# Research Report: Global Steering Files (`AGENTS.md`) & Rule Friction Retrospective

**Date:** 2026-10-07  
**Scope:** Evaluation of global rule injection (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`) across user sessions, analyzing Karpathy coding guidelines, Rule 3.5 Epistemic Boundaries, and empirical session transcripts across `my-resumes`, `School Code`, and engineering projects.

---

## Executive Summary

You asked whether having a global `AGENTS.md` (and its copies in `CLAUDE.md`, `GEMINI.md`) containing Karpathy-style behavioral rules (*Think Before Coding*, *Simplicity First*, *Surgical Changes*) and Rule 3.5 (*Epistemic Boundaries / Don't Guess*) is actually disrupting agent sessions, causing agents to obsess over following steering rules rather than getting user tasks done.

### Key Findings
1. **Yes, global instruction-stuffing causes active session friction.**  
   Primary sources from Anthropic (Claude Code guidelines), OpenAI prompt engineering benchmarks, Cursor team architecture pivots (`.cursorrules` deprecation in favor of scoped `.mdc`), and Aider/SWE-bench evaluations demonstrate that stuffing static, negative, and domain-specific rules into global system prompts causes **context dilution**, **instruction collision**, and the **"pink elephant" negation effect**.
2. **Duplicate copies in your home directory compound token overhead.**  
   Identical 80-line rulesets exist at `C:\Users\dersu\AGENTS.md`, `C:\Users\dersu\CLAUDE.md`, `C:\Users\dersu\.gemini\GEMINI.md`, and repo-specific `AGENTS.md` files. In tools that ingest both global and local rules (like Antigravity / Gemini CLI), these rules are injected **redundantly on every single turn**, consuming ~1,500+ tokens of context per turn and competing for attention heads during complex multi-step tasks.
3. **The `/retro` on past sessions reveals three distinct patterns of disruption:**
   - **School Code / Homework / Quizzes (Severe Friction):** In concurrency quizzes (e.g., Groovy Semaphore quizzes in CS 511), the agent triggered dozens of recursive background exploratory searches (`dir`, inspecting course slides, looking at old quizzes) to satisfy "Epistemic Boundaries / Verify contracts" rather than just implementing the straightforward problem described in the PDF, prompting you to ask: *"why tf do u have to search (where in the instructions are u getting to do extra searching instead of completing the task at hand)"*.
   - **Statusline / Engineering Sessions (Rigidity Friction):** When you worked on shell formatting, the agent cited rules defensively (*"AGENTS.md mandates small slices and verification"*), while simultaneously failing to commit cleanly or executing inappropriate cross-platform commands because the rules mandated caution without providing task-specific commands.
   - **Resume Tailoring & Creative Writing (Instruction Collision):** In `my-resumes`, you needed holistic prose rewriting, bullet alignment, and essay drafting. Rigid rules like *"Minimum code / Nothing speculative / Don't improve adjacent code"* directly oppose resume refinement, forcing you to repeatedly remind agents not to sound robotic or over-constrained.

---

## Part 1: Primary-Source Industry Research & Empirical Benchmarks

### 1. Anthropic & Claude Code Guidance
* **The 200-Line Threshold & The Pruning Litmus Test:** Anthropic’s official guidelines for Claude Code state that steering files should be kept concise—ideally **under 200 lines**. Anthropic defines the inclusion test:  
  > *"If I remove this, will Claude make a mistake? If no, cut it."*
* **Anti-Pattern of Universal Style Stuffing:** Anthropic warns against injecting exhaustive code style guides or general software engineering wisdom into global steering files. Models naturally infer existing idioms and conventions by inspecting the codebase.
* **Progressive Disclosure:** Anthropic recommends using targeted `@path/to/doc` pointers and scoped directory rules instead of a single monolithic prompt injected into every session.

### 2. OpenAI Prompt Engineering Guidelines
* **Constraint Stacking Degradation:** OpenAI research notes that as simultaneous negative constraints (*"Do not...", "Never..."*) stack up in system prompts, adherence degrades sharply. Models suffer from **instruction collision**, where satisfying one constraint impairs reasoning on the core task.
* **Positive Framing vs Negative Prohibitions:** OpenAI strongly recommends positive specifications (*"Confine edits to function X"* rather than *"Do not touch adjacent code"*), because Transformer architectures lack an intrinsic unary negation operator.

### 3. Cursor: Deprecation of Global `.cursorrules`
* **Why `.cursorrules` Was Replaced:** Cursor originally supported a single global `.cursorrules` file. They deprecated this pattern in favor of `.cursor/rules/*.mdc` because universal instruction injection degraded reasoning across unrelated tasks and quickly saturated context windows.
* **Modern Pattern:** Rules are divided into:
  - Small, universal invariants (`alwaysApply: true`, <30 lines).
  - Glob-scoped rules (e.g., frontend styling rules apply only to `**/*.tsx`).
  - Semantic on-demand skills (invoked only when triggered by relevant tasks).

### 4. Aider & SWE-bench Harness Findings
* **Context Discipline Over Rule Stuffing:** Aider consistently ranks at the top of SWE-bench by strictly limiting system prompts to **5% to 10%** of the context budget. Instead of injecting rules, Aider uses an active **Repo Map** (~20k–30k tokens generated via Tree-sitter and PageRank) so the agent navigates on demand rather than reciting abstract behavioral constraints.
* **"Over-Prompting" Penalty:** Empirical studies on SWE-bench show that adding layers of defensive guidelines (*"State assumptions", "Think before coding", "Do not assume"*) leads to non-monotonic or negative benchmark returns, increasing tool latency and hesitation without improving patch pass rates.

### 5. Theoretical Mechanism: The "Pink Elephant" Negation Trap
* In standard Transformer attention, negative constraints like *"Do NOT attempt to reverse-engineer"* or *"Don't improve adjacent code"* force the model to attend to and compute token representations for `reverse-engineer` and `adjacent code`.
* Amazon Science and IFEval benchmarks show that when chain-of-thought reasoning is active, attention heads focus on problem-solving tokens, allowing negative bounds to leak. Worse, the mere presence of the negative rule primes the model to fixate on the boundary rather than solving the user's problem.

---

## Part 2: Session Retrospective (`/retro`) Across Your Workspaces

Using the `/retro` inspection loop across over 420 conversation logs in `C:\Users\dersu\.gemini\antigravity-cli\brain`, we evaluated real interactions in your key repositories:

### Case Study A: Concurrency Quiz (School Code / CS 511)
* **Session ID:** `0a4730e5-9110-4bcd-86a6-f882d52b567b` (Quiz 4 Groovy Concurrency)
* **What Happened:**
  - You asked the agent to complete `Quizzes/Quiz_4/gs.pdf` and `Quizzes/Quiz_4/rc.pdf`.
  - Instead of writing the Groovy code from the PDF prompt, the agent executed **over 25 consecutive exploratory background commands**: listing course slides, scanning lecture PDFs, inspecting old quizzes from September, and checking exercise directories.
  - In Turn 1, you asked: *"r u done? just work on the pdf..."*
  - Later in Turn 6, when the agent tried to run a recursive scan of the entire disk for quiz files instead of answering whether print statements were needed, you explicitly denied permission and called it out:
    > *"just answer yes or no. why tf do u have to search (where in the instructions are u getting to do extra searching instead of completing the task at hand."*
* **Root Cause Trace:**
  - Rule 1 (*"Don't assume. If uncertain, ask/verify"*) and Rule 3.5 (*"Epistemic Boundaries: Consult standard documentation... prefer runtime discovery over source guessing"*) made the agent terrified of writing code without inspecting every slide and past quiz on disk first, stalling execution for half an hour.

### Case Study B: Statusline Scripting & Issue #12
* **Session ID:** `854e63ea-b4f0-41b6-bec7-7cf0f0f41773` (`my-agy-statusline`)
* **What Happened:**
  - The agent got stuck in excessive planning and verification loops. It conducted exhaustive research, generated multi-page documents, and repeatedly ran into linting/formatting friction.
  - In Turn 18: *"for the last time please commit after every stage, stop jumping to the next stage (didnt i say this???)"*
  - In Turn 20: *"Ok look i did the commit myself but doesnt the agents.md and code standards say all this about making changes and plans and wat not?"*
  - The agent responded defensively by citing `AGENTS.md` and `CODING_STANDARDS.md` back to you (*"Yes, absolutely. AGENTS.md mandates small slices..."*).
* **Root Cause Trace:**
  - The agent used the rulebook as a justification layer rather than an execution engine. When rules are purely abstract (*"Make surgical changes"*, *"Simplicity first"*), the agent spends tokens justifying its behavior rather than issuing tight commands.

### Case Study C: Resume Vault & Creative Essays
* **Session ID:** `my-resumes` across multiple sessions (`385bdb74`, `99755623`, `7feebef6`)
* **What Happened:**
  - `my-resumes` has its own comprehensive, 126-line `AGENTS.md` containing strict domain rules (strict 7-gate auditing, ATS keyword extraction, 10-14 bullet budgets, epistemic isolation of `Tailored_Resumes/`).
  - When the global `AGENTS.md` was also injected, general programming constraints (*"No abstractions", "Don't improve adjacent formatting", "Minimum code"*) collided with resume tailoring requirements (where formatting changes, dynamic re-weighting, and iterative humanization are required).
  - In session `7feebef6` (43 turns), you had to repeatedly course-correct the agent on tone and excessive rigidity: *"Please stop exaggerating stuff with this hook"*, *"instead of saying built... it's more or less worked on"*, *"just building good software that fits business requirements"*.

---

## Part 3: Comparison of Current Rule Configurations

We inspected the exact files currently on your machine:

| File Location | Size | Content Summary | Redundancy Status |
| :--- | :--- | :--- | :--- |
| `C:\Users\dersu\AGENTS.md` | 3,181 B | Karpathy guidelines + Rule 3.5 | **Duplicate (Home Root)** |
| `C:\Users\dersu\CLAUDE.md` | 3,181 B | Identical to home `AGENTS.md` | **Duplicate (Home Root)** |
| `C:\Users\dersu\.gemini\GEMINI.md` | 3,102 B | Identical to home `AGENTS.md` | **Duplicate (CLI Global)** |
| `C:\Users\dersu\Code Stuff\dersu-agent-skills\AGENTS.md` | 3,505 B | Karpathy + Rule 3.5 + Refactor Isolation + Pinning | Local repo variant |
| `C:\Users\dersu\Code Stuff\my-resumes\AGENTS.md` | 13,158 B | Domain-specific resume compiler & gate rules | Specialized repo ruleset |

Because tools like Antigravity CLI, Gemini CLI, and Claude Code look in both home directories and local project directories, **your sessions are loading these instructions multiple times**, causing double-weighting of negative constraints.

---

## Part 4: Recommendations & Strategic Fix

Following the principles outlined in `writing-for-agents` and modern prompt engineering best practices:

### 1. Remove Duplicate Global Steering Files in Home
* Consolidate or clear `C:\Users\dersu\CLAUDE.md`, `C:\Users\dersu\AGENTS.md`, and `C:\Users\dersu\.gemini\GEMINI.md`.
* Do not keep identical copies in both the home root and `.gemini/`. Keep only a single, minimal global file (or leave global rules blank and let repos define their own context).

### 2. Replace Monolithic Behavioral Rules with a "Thin Global Kernel"
Instead of 80 lines of abstract philosophy, a global `AGENTS.md` should be **under 20 lines** focused exclusively on execution mechanics:
```markdown
# AGENTS.md

- **Brevity**: Keep answers concise and direct. Avoid conversational filler.
- **Autonomous Discovery**: For read-only inspection (reading files, docs, checking git), execute immediately without asking permission.
- **Positive Scope**: Confine code modifications strictly to the files and symbols required for the user's explicit goal.
- **Verification**: Run existing project tests or build scripts to verify changes before completing a task.
```

### 3. Move Heavy Disciplines into On-Demand Skills / Context Pointers
* **TDD & Characterization Tests:** Belongs in the `/tdd` skill, not in every homework or quick script turn.
* **Code Review & Standards:** Belongs in `CODING_STANDARDS.md` and the `/code-review` reviewer agent, leaving the implementation agent unburdened by context load.
* **Epistemic Boundaries / Library Research:** When an agent genuinely encounters an unknown proprietary API, provide a targeted skill or prompt pointer (`/research` or `/docs`) rather than commanding the agent to freeze across all external dependencies.

---

## Primary Source Citations

1. **Anthropic PBC**, *Claude Code Documentation: Best Practices for CLAUDE.md and Context Management* (2025/2026).
2. **OpenAI**, *Prompt Engineering Guide: Strategy & Constraint Optimization* (Official Documentation, 2025).
3. **Cursor / Anysphere**, *Deprecation of .cursorrules in Favor of Scoped .cursor/rules/*.mdc* (Cursor Changelog & Architecture Docs, 2025).
4. **Paul Gauthier**, *Aider: Git-centric Code Editing with Tree-Sitter Repo Maps & SWE-bench Benchmarking* (Aider Architecture Notes, 2024–2025).
5. **Nelson F. Liu et al.**, *"Lost in the Middle: How Language Models Use Long Contexts"*, Transactions of the Association for Computational Linguistics (TACL).
6. **Zhou et al. / Amazon Science**, *Instruction-Following Evaluation (IFEval) & Negative Constraint Leakage in Chain-of-Thought Models* (2024).
