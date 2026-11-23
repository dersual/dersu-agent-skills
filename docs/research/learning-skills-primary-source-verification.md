# Research Report: Learning Skills Primary-Source Verification & Grievance Mapping

**Date:** 2026-11-21  
**Status:** Verified against Primary Sources  
**Scope:** Fact-check of external repositories cited in `docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf`, technical autopsy of five external GitHub learning skill suites and five local `dersu-agent-skills` teaching skills, and mechanistic mapping against the six student grievances and three unresolved questions in `docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md`.

---

## Executive Summary

This report verifies every GitHub repository, star count, file structure, and mechanism cited in the Gemini web session (`docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf`) against live GitHub API metadata and raw repository source files as of November 21, 2026.

1. **Zero Hallucinated Repositories:** All six external repositories cited in the Gemini PDF exist at their exact URLs. None were fabricated.
2. **Accurate Star & Fork Metrics:** The Gemini PDF reported accurate traction metrics (`amosblomqvist/learn` at 4,277 stars; `amosblomqvist/learnharness` at 10,906 stars; `mattpocock/skills` at 329,637 stars). However, the PDF omitted the low star counts on `iannbing/skills-for-learning` (1 star), `ahmed3bead/teach-me` (1 star), and `vasanthsreeram/Alvarmethod` (167 stars), and noted 5 format templates in `skills/teach/` where only 4 exist.
3. **Architectural Gap in Local Skills:** None of the current local teaching skills (`teach`, `study-tutor`, `code-tutor`, `code-coach`, `scaffold-exercises`) combine upfront dependency-tree curriculum mapping, syllabus/notes ingestion, and strict question-tool checkpoints. Combining mechanisms from `amosblomqvist/learn`, `vasanthsreeram/Alvarmethod`, `mohitagw15856/pm-claude-skills`, and local `code-coach` directly resolves all six grievances in `SESSION_POSTMORTEM_AND_GRIEVANCES.md`.

---

## Part 1: Fact-Check Matrix — Gemini PDF Claims vs. Live GitHub Primary Sources

All GitHub metrics below were fetched directly from `https://api.github.com/repos/<owner>/<repo>` on 2026-11-21.

| Repository / Resource | Gemini PDF Claim (`Branch • AI Knowledge Tree Mapping Workflow.pdf`) | Verified Primary Source Reality (2026-11-21) | Verification Verdict |
| :--- | :--- | :--- | :--- |
| [`amosblomqvist/learn`](https://github.com/amosblomqvist/learn) | Full `.pi` agent harness config; ~4.3k stars, 451 forks; created Aug 2026; has `skills/teach/`, `skills/visualize/`, 4 TS extensions, 3 subagents. | Exists. **4,277 stars, 456 forks**. Created `2026-08-24`. Note: repo root *is* the `.pi` config (`skills/teach/SKILL.md`, `skills/visualize/SKILL.md`, `extensions/*.ts`, `agents/*.md`), designed to be cloned as `git clone ... .pi`. | **Verified Accurate** |
| [`amosblomqvist/learnharness`](https://github.com/amosblomqvist/learnharness) | Standalone desktop evolution of `learn`; ~9.8k–10.4k stars; adds persistent cross-session proposition & reasoning-chain knowledge graph. | Exists. **10,906 stars, 1,428 forks**. Created `2026-10-16`. AGPL-3.0 Next.js + Electron app (`learnharness.ai`). Persists propositions/chains in `graph/{nodes,chains,sessions,coverage}.jsonl` and separates `Prober`, `Teacher`, and `Practitioner` agents. | **Verified Accurate** (Stars grew from ~10.4k to 10.9k) |
| [`vasanthsreeram/Alvarmethod`](https://github.com/vasanthsreeram/Alvarmethod) | Community port translating Alvar's 3-phase DAG workflow into portable `SKILL.md` files for Claude Code, OpenCode, and Cursor. | Exists. **167 stars, 17 forks**. Created `2026-08-16`. MIT license. Contains 5 portable skills (`teach`, `probe`, `learn-profile`, `learn-visual`, `learn-verify`) and maps native question tools across Claude Code, Codex, Grok, Pi, and OpenCode. | **Verified Accurate** (Star count of 167 was omitted in PDF) |
| [`iannbing/skills-for-learning`](https://github.com/iannbing/skills-for-learning) | Contains `tutorial/SKILL.md`; maps out Core Concepts first with a Mermaid `graph TD` concept map before generating milestone-based practice projects. | Exists. **1 star, 1 fork**. Created `2026-04-22`. Path is `skills/tutorial/SKILL.md` (plus `guide`, `explain`, `walkthrough`). Generates `learn-<topic>/` git repo with `theory/01-core-concepts.md` (`graph TD`), `02-controversies.md`, `03-expert-quiz.md`, and `practice/`. | **Verified Accurate** (Low traction: 1 star) |
| [`mohitagw15856/pm-claude-skills`](https://github.com/mohitagw15856/pm-claude-skills) | Contains `study-notes-synthesizer/SKILL.md`; rejects lecture chronology with core rule: *"Organized by concept dependency, not lecture chronology"*. | Exists. **1,584 stars, 284 forks**. Created `2026-01-29`. Path is `skills/study-notes-synthesizer/SKILL.md`. Exact quote confirmed in `Framework` Rule 1 and `Quality Checks` line 48. | **Verified Accurate** |
| [`ahmed3bead/teach-me`](https://github.com/ahmed3bead/teach-me) | Contains `SKILL.md`; adaptive tutor skill with a "Source-Grounded Mode" for a syllabus, textbook, or playlist. | Exists. **1 star, 0 forks**. Created `2026-09-13`. Root `SKILL.md` routes to `references/source-grounded-mode.md`, `references/curriculum-delivery.md`, and `references/diagnostic-engine.md`, backed by JSON schemas in `schemas/`. | **Verified Accurate** (Low traction: 1 star) |
| [`mattpocock/skills`](https://github.com/mattpocock/skills) (`teach` skill) | ~327k stars on parent repo; copied to `dersu-agent-skills/skills/teach/SKILL.md`; paired with "5 read-only format specification templates (`*-FORMAT.md`)". | Exists. **329,637 stars, 27,697 forks**. Upstream path is `skills/productivity/teach/SKILL.md` (byte-identical to local `skills/teach/SKILL.md`). Contains **4** `*-FORMAT.md` files (`GLOSSARY`, `LEARNING-RECORD`, `MISSION`, `RESOURCES`), not 5. | **Minor Discrepancy** (4 format files exist, not 5; `reference/*.html` has no `REFERENCE-FORMAT.md`) |

---

## Part 2: Primary-Source Technical Autopsy of External Repositories

### 1. `amosblomqvist/learn` (Eero Alvar)
* **Repository URL:** `https://github.com/amosblomqvist/learn`
* **Inspected Files:**
  * [`README.md`](https://raw.githubusercontent.com/amosblomqvist/learn/main/README.md)
  * [`skills/teach/SKILL.md`](https://raw.githubusercontent.com/amosblomqvist/learn/main/skills/teach/SKILL.md)
  * [`skills/visualize/SKILL.md`](https://raw.githubusercontent.com/amosblomqvist/learn/main/skills/visualize/SKILL.md)
  * [`agents/researcher.md`](https://raw.githubusercontent.com/amosblomqvist/learn/main/agents/researcher.md)
  * [`agents/mermaid-maker.md`](https://raw.githubusercontent.com/amosblomqvist/learn/main/agents/mermaid-maker.md)
  * [`agents/svg-maker.md`](https://raw.githubusercontent.com/amosblomqvist/learn/main/agents/svg-maker.md)
  * [`extensions/quiz.ts`](https://raw.githubusercontent.com/amosblomqvist/learn/main/extensions/quiz.ts)
  * [`extensions/ask-user-question.ts`](https://raw.githubusercontent.com/amosblomqvist/learn/main/extensions/ask-user-question.ts)
  * [`extensions/md-log.ts`](https://raw.githubusercontent.com/amosblomqvist/learn/main/extensions/md-log.ts)
  * [`extensions/visual-tools/index.ts`](https://raw.githubusercontent.com/amosblomqvist/learn/main/extensions/visual-tools/index.ts)

#### Verified Architecture & Pedagogical Rules
1. **Two Core Pedagogical Principles (`skills/teach/SKILL.md`):**
   * **Principle i — Unconditional truths first:** Distinguishes an *unconditional truth* (a fact accepted at face value with zero caveats or nuance) from an *axiom* (a root node with no incoming edges). Instructs the model to find universal statements (*"ALL X is done through {Y}"*) or real definitions so the learner's brain locks them in without hedging against future contradictions.
   * **Principle ii — Motivated discovery ("How could I have discovered this?"):** Prohibits arbitrary decree. Every step must start from the motivating problem and show why someone would reach for that formula or manipulation (modeled on 3Blue1Brown). Dynamically switches between **Socratic** (posing the problem via `quiz` before revealing) and **Expository** (narrating the derivation when the learner is low-energy or the concept is beyond cold-reasoning reach).
2. **Strict Three-Phase State Machine (`skills/teach/SKILL.md`):**
   * **Phase 1 — Probe:** Separates skill measurement (`quiz` tool) from goal clarification (`ask_user_question` tool). Requires **bracketing the edge** across every prerequisite strand: finding both a floor (what the learner gets right) and a ceiling (where knowledge breaks). Mandates binary-searching difficulty upward on correct answers and probing around wrong answers to distinguish careless slips from systematic misconceptions.
   * **Phase 2 — Plan:** Dispatches the `researcher` subagent (`agents/researcher.md`) to verify facts and first principles. Outputs a two-part plan in chat before teaching: (1) prose explanation of the approach, and (2) a small Mermaid dependency DAG (`graph TD`) with unconditional truths at the roots and the learner's goal at the sink. Enforces a hard gate: *"Then stop and wait for his go-ahead... Do not begin Phase 3 until he okays the plan."*
   * **Phase 3 — Teach (The Per-Node Loop):** Traverses the Mermaid DAG one node at a time. Every node—whether foundational or derived—must execute four steps: **1. Motivate $\to$ 2. Establish $\to$ 3. Connect $\to$ 4. Quiz-check**.
3. **Anti-Leak Quiz Construction Procedure (`skills/teach/SKILL.md` & `extensions/quiz.ts`):**
   * `skills/teach/SKILL.md` enforces a 4-step construction algorithm: (1) every option is a bare claim with zero `"because..."` justification; (2) write the correct claim first, then mutate it into distractors representing specific misconceptions at the same grain size; (3) each distractor is diagnostic; (4) no asymmetric bolding.
   * `extensions/quiz.ts` implements programmatic Fisher-Yates shuffling (`shuffleOptions`), keys `correctAnswer` by option value string rather than index to prevent index-counting bugs, automatically injects an exclusive `"I don't know"` option (`__dont_know__`) that logs a clean knowledge gap rather than a wrong guess, and provides a Tab-accessible free-text `Note (optional):` editor so the learner can explain their thinking.
   * `extensions/quiz.ts` and `extensions/ask-user-question.ts` share a global mutex (`globalThis.__piSharedUiLock`) so TUI popups serialize cleanly.
4. **Render-and-Inspect Visual Subagents (`skills/visualize/SKILL.md`, `agents/mermaid-maker.md`, `agents/svg-maker.md`):**
   * Visuals are outsourced to `mermaid-maker` (for structural/relational graphs, capped at ~4–7 nodes to prevent cramming) or `svg-maker` (for coordinate geometry and spatial layouts).
   * Using `extensions/visual-tools/index.ts`, the subagent writes source code, renders a PNG preview (`@mermaid-js/mermaid-cli` + Chrome or `rsvg-convert`), **visually inspects the rendered PNG inline**, iterates until arrows, geometry, and labels are defect-free, and publishes `viz-<slug>-<timestamp>.png` for inline Obsidian embedding via `extensions/md-log.ts`.

---

### 2. `amosblomqvist/learnharness` (LearnHarness Desktop & Web Runtime)
* **Repository URL:** `https://github.com/amosblomqvist/learnharness`
* **Inspected Files:**
  * [`README.md`](https://raw.githubusercontent.com/amosblomqvist/learnharness/main/README.md)
  * [`docs/architecture.md`](https://raw.githubusercontent.com/amosblomqvist/learnharness/main/docs/architecture.md)
  * [`docs/teaching-methodology.md`](https://raw.githubusercontent.com/amosblomqvist/learnharness/main/docs/teaching-methodology.md)
  * [`skills/learnharness/SKILL.md`](https://raw.githubusercontent.com/amosblomqvist/learnharness/main/skills/learnharness/SKILL.md)

#### Verified Architecture & Evolution Beyond `learn`
1. **Three Specialized Runtime Agents (`docs/architecture.md`):**
   * **Prober:** Equipped with `probe`, `recall`, `ask_user_question`, `probe_done`, and read-only file/research/graph tools. Calling `probe_done` triggers a formal agent handoff to the Teacher.
   * **Teacher:** Equipped with `quiz`, `explain`, `ask_user_question`, `plan_init`, and background workers (`research`, `PDF`, `demo`, `visual`, `show_image`). `plan_init` validates and stores the Mermaid dependency DAG.
   * **Practitioner:** Runs dedicated practice sessions (`kind: "practice"`) using `problem` (commits a problem statement and hidden model solution) and `conclude` (records outcome and reveals solution).
2. **Non-Disruptive Side Questions (`docs/architecture.md` & `components/side-thread.tsx`):**
   * Learners can highlight any text or click a speech bubble to open a floating/dockable **Side Question** thread (`app/api/chats/[id]/side-chats/`).
   * Side questions execute a tool-less streamed call that answers the learner's immediate confusion in 1–2 sentences without interrupting the main lesson turn or derailing the DAG state machine. New side exchanges are injected back into the main agent's context window as attributed `side-question` references at the next turn boundary.
3. **PDF Figure Cropping & Annotation (`src/agent/tools/pdf-figure.ts`):**
   * The `visual` tool accepts `pdf: { path, page }`, renders the learner's local PDF page natively via `pdfjs` + Skia, allows the visual subagent to call `crop_page` at 300 DPI on lecture slide diagrams, and overlays SVG arrows and labels onto a content-addressed SHA-256 snapshot.
4. **Post-Hoc Proposition & Reasoning-Chain Knowledge Graph (`docs/architecture.md`):**
   * Rather than storing subjective "mastery ratings," an asynchronous pipeline (`Extractor` $\to$ `Identity Auditor` $\to$ `Deterministic Merger`) extracts objective **propositions** and **jointly-entailing reasoning chains** from teacher prose and imported PDF/Markdown notes into `graph/{nodes,chains,sessions,coverage}.jsonl`.
5. **Formalized Theory of Minimal Trees & Effort Allocation (`docs/teaching-methodology.md`):**
   * Section 7a (*Effort allocation*) codifies that the learner has finite mental effort per session: the system must absorb 100% of logistics (what to learn, order, source verification) so 100% of the learner's effort goes into material contact.
   * Section 7b (*The minimal tree*) codifies pruning everything already held and everything off the path to the goal, distinguishing the coarse **plan tree** (structural landmarks shown to the learner) from fine-grained **reasoning steps** (checked after every single step).

---

### 3. `vasanthsreeram/Alvarmethod` (Cross-Harness Portable Skill Pack)
* **Repository URL:** `https://github.com/vasanthsreeram/Alvarmethod`
* **Inspected Files:**
  * [`README.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/README.md)
  * [`skills/teach/SKILL.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/teach/SKILL.md)
  * [`skills/teach/references/philosophy.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/teach/references/philosophy.md)
  * [`skills/teach/references/process.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/teach/references/process.md)
  * [`skills/teach/references/learner-files.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/teach/references/learner-files.md)
  * [`skills/teach/references/quiz-ui.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/teach/references/quiz-ui.md)
  * [`skills/probe/SKILL.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/probe/SKILL.md)
  * [`skills/learn-profile/SKILL.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/learn-profile/SKILL.md)
  * [`skills/learn-verify/SKILL.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/learn-verify/SKILL.md)
  * [`skills/learn-visual/SKILL.md`](https://raw.githubusercontent.com/vasanthsreeram/Alvarmethod/main/skills/learn-visual/SKILL.md)

#### Verified Architecture & Portability Mechanisms
1. **Cross-Harness Native Question Tool Mapping (`skills/teach/references/quiz-ui.md`):**
   * Explicitly forbids pasting A/B/C/D multiple-choice questions as plain chat text.
   * Maps the graded quiz mechanism to each harness's native interactive picker:
     * **OpenCode:** `question` tool (`questions: [{ header, text, options: [...], ... }]`)
     * **Claude Code:** `AskUserQuestion` tool
     * **Codex / Grok Build:** `ask_user_question` tool
     * **Pi:** `quiz` or `ask_user` extension
   * Enforces 3 content choices + `"I don't know"` (`"Skip this strand; do not guess."`), forbids marking the correct answer `(Recommended)`, and uses the tool's `Other`/free-text slot as a reasoning talk-through channel.
2. **Five-State Strand Diagnostic Scoring (`skills/probe/SKILL.md`):**
   * Evaluates both answer selection and talk-through reasoning:
     * `correct + sound reason` $\to$ `known`
     * `correct, thin reason` $\to$ `edge`
     * `wrong, near-miss` $\to$ `edge`
     * `wrong, foundation missing` $\to$ `unknown`
     * `I don't know` $\to$ `blocked` or `unknown`
3. **Stateful `.alvar/` Local Workspace (`skills/teach/references/learner-files.md`):**
   * Persists state across sessions without requiring a custom database:
     * `.alvar/LEARNER.md`: Solid ground, goal, pace, struggle preferences, and hated LLM habits (generated via `learn-profile`).
     * `.alvar/maps/<slug>.md`: Table of dependency strands labeled `known | edge | unknown | blocked` with evidence and quiz logs.
     * `.alvar/sessions/<date>-<slug>.md`: Mermaid `graph TD` plan and node-by-node log (`taught`, `visual`, `quiz`, `result: lock-in | retry | insert-prereq`).
     * `.alvar/visuals/<slug>-<n>.svg`: Self-inspected SVG diagrams.

---

### 4. `iannbing/skills-for-learning`
* **Repository URL:** `https://github.com/iannbing/skills-for-learning`
* **Inspected Files:**
  * [`skills/tutorial/SKILL.md`](https://raw.githubusercontent.com/iannbing/skills-for-learning/main/skills/tutorial/SKILL.md)
  * [`skills/guide/SKILL.md`](https://raw.githubusercontent.com/iannbing/skills-for-learning/main/skills/guide/SKILL.md)
  * [`skills/explain/SKILL.md`](https://raw.githubusercontent.com/iannbing/skills-for-learning/main/skills/explain/SKILL.md)
  * [`skills/walkthrough/SKILL.md`](https://raw.githubusercontent.com/iannbing/skills-for-learning/main/skills/walkthrough/SKILL.md)

#### Verified Architecture & Pedagogical Rules
1. **Theory-to-Practice Repository Generator (`skills/tutorial/SKILL.md`):**
   * Generates a git-initialized repository `learn-<topic>/` containing:
     * `theory/01-core-concepts.md`: Explains *why* before *what* for 5–8 core concepts, anchored by a mandatory Mermaid `graph TD` concept map.
     * `theory/02-controversies.md`: At least 3 common confusions (with Mermaid decision trees), 2 criticisms/debates (requiring an opinionated stance rather than fence-sitting), and 2 production gotchas.
     * `theory/03-expert-quiz.md`: 10 trade-off and failure-mode questions using HTML `<details><summary>Reveal Answer</summary></details>` tags.
     * `practice/<project-name>/`: Minimal unbuilt code scaffold + `README.md` with 4–7 ordered, committable milestones (`- [ ] Step X.Y`) cross-referenced to `theory/`.
     * `.guide/learner-profile.md`: Tracks weak points and session logs across tutorials.
2. **5-Level Hint Escalation Ladder & Weak-Point Tracking (`skills/guide/SKILL.md`):**
   * Separates curriculum generation (`tutorial`) from hands-on coaching (`guide`).
   * Enforces "The learner drives" and a strict 5-level hint escalation ladder when stuck:
     * **Level 1 — Reframe:** Break down the first required action.
     * **Level 2 — Narrow:** Focus on input/output data flow.
     * **Level 3 — Point:** Name the specific function/concept and key detail.
     * **Level 4 — Demonstrate:** Show a minimal code snippet of the *pattern* (not the solution).
     * **Level 5 — Explain and show:** Provide the solution only on explicit request or after Levels 1–4 fail.
   * Any step requiring Level 3+ hints or revealing a conceptual misunderstanding is logged into `.guide/learner-profile.md` under `## Weak Points` with severity (`minor | moderate | significant`). When 3+ weak points accumulate, it generates `theory/weak-points.md` with targeted Mermaid diagrams and practice exercises.

---

### 5. `mohitagw15856/pm-claude-skills` (`study-notes-synthesizer`)
* **Repository URL:** `https://github.com/mohitagw15856/pm-claude-skills`
* **Inspected File:**
  * [`skills/study-notes-synthesizer/SKILL.md`](https://raw.githubusercontent.com/mohitagw15856/pm-claude-skills/main/skills/study-notes-synthesizer/SKILL.md)

#### Verified Architecture & Pedagogical Rules
1. **Five-Rule Exam Synthesis Framework (`skills/study-notes-synthesizer/SKILL.md`):**
   * **Rule 1 — Synthesize, never sequence:** *"organize by concept dependency, not by lecture order; lecture order is how it was taught, not how it's structured."*
   * **Rule 2 — Explain-then-anchor:** Every concept receives a **Plainly:** explanation first, followed by **Formally:** (formal definition), **Builds on:** (prerequisites), and **Confused with:** (adjacent concepts).
   * **Rule 3 — Confusable pairs side-by-side:** Contrasts easily confused pairs directly because exams test boundary distinctions.
   * **Rule 4 — Retrieval questions at three depths:** Every concept cluster includes self-test questions at three depths: (1) `[recall]` define, (2) `[apply]` problem application, and (3) `[why X not Y]` comparative justification.
   * **Rule 5 — Gaps are findings:** Explicitly compares messy notes/slides against the course syllabus and surfaces missing or under-covered topics at the very top of the study guide (`⚠ Gaps in your materials:`), prohibiting the AI from silently inventing content to hide gaps.
2. **Telegraphic Cram Sheet Cap:** Concludes with a `One-page cram sheet` strictly capped at 15–20 highest-yield items.

---

### 6. `ahmed3bead/teach-me`
* **Repository URL:** `https://github.com/ahmed3bead/teach-me`
* **Inspected Files:**
  * [`SKILL.md`](https://raw.githubusercontent.com/ahmed3bead/teach-me/main/SKILL.md)
  * [`references/source-grounded-mode.md`](https://raw.githubusercontent.com/ahmed3bead/teach-me/main/references/source-grounded-mode.md)
  * [`references/curriculum-delivery.md`](https://raw.githubusercontent.com/ahmed3bead/teach-me/main/references/curriculum-delivery.md)
  * [`references/diagnostic-engine.md`](https://raw.githubusercontent.com/ahmed3bead/teach-me/main/references/diagnostic-engine.md)
  * [`schemas/curriculum-map.schema.json`](https://raw.githubusercontent.com/ahmed3bead/teach-me/main/schemas/curriculum-map.schema.json)

#### Verified Architecture & Pedagogical Rules
1. **Source-Grounded Mode & 7-Point Understanding Gate (`references/source-grounded-mode.md`):**
   * Requires maintaining a coverage ledger (`schemas/source-coverage.schema.json`) tracking which exact PDF pages, timestamps, or slides were inspected (`scripts/inspect_source.py`).
   * Enforces a 7-point Understanding Gate before teaching any unit from a user's course materials, and requires labeling claims by provenance: `source`, `verified`, `disputed`, `external`, `adaptation`, `inferred`, or `unverified`.
2. **Unit-Boundary Consent Gate vs. Per-Turn Interrogation (`SKILL.md` Step 5):**
   * Unlike Alvar's per-step quiz mandate, `teach-me` forbids turning every chat turn into an oral exam: *"Finish a meaningful learning unit before offering an understanding check... End that boundary turn with the invitation alone, for example: 'That completes the unit. Would you like a short optional check, or shall we continue?' Never append a 'Quick check' task to a lesson before the boundary, and never state or assume the learner's answer before they give it."*
3. **Diagnostic Evidence Classification (`references/diagnostic-engine.md`):**
   * Classifies task evidence into five states (`demonstrated`, `partial`, `misconceived`, `unknown`, `blocked`) and mandates accepting an explicit learner statement of zero knowledge without forcing a redundant placement exam.

---

## Part 3: Technical Audit of Local Teaching & Learning Skills (`dersu-agent-skills/skills/`)

We inspected the five local teaching/coaching skills in `C:\Users\dersu\Code Stuff\dersu-agent-skills\skills\`:

| Local Skill Path | Core Mechanism | Strengths | Failure Modes Against `SESSION_POSTMORTEM_AND_GRIEVANCES.md` |
| :--- | :--- | :--- | :--- |
| [`skills/teach/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/SKILL.md) (plus `MISSION-FORMAT.md`, `RESOURCES-FORMAT.md`, `LEARNING-RECORD-FORMAT.md`, `GLOSSARY-FORMAT.md`) | Stateful workspace (`MISSION.md`, `RESOURCES.md`, `./lessons/*.html`, `./reference/*.html`, `./learning-records/*.md`, `./assets/*`, `NOTES.md`). Enforces *"Never trust your parametric knowledge"* and separates Fluency vs. Storage strength. | Durable multi-session file persistence; ADR-style `learning-records` track misconceptions and ZPD; reusable HTML quiz/simulator assets; strict anti-hallucination citation rules. | **No upfront dependency DAG:** Builds bottom-up one HTML lesson at a time without mapping the course trunk vs. branches. **No local syllabus ingestion pipeline:** Assumes web research (`RESOURCES.md`) rather than indexing local course PDFs/slides. |
| [`skills/study-tutor/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/study-tutor/SKILL.md) | 7-step per-chunk conversational loop: simple explanation $\to$ analogy $\to$ bite-sized chunk $\to$ ask learner to explain back $\to$ gentle correction $\to$ small practice problem $\to$ memory hook. | Enforces bite-sized pacing (2–3 paragraphs max) and waiting for learner responses before advancing. | **Stateless & unmapped:** No file persistence, no diagnostic pretest (always assumes learner is completely new in Step 1), no dependency graph, and relies on open-ended chat prompts rather than structured question tools. |
| [`skills/code-tutor/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/code-tutor/SKILL.md) | 7-step coding loop identical in structure to `study-tutor`: simple explanation $\to$ tiny example $\to$ 5–15 line code chunk $\to$ ask learner what it does $\to$ correction $\to$ small exercise $\to$ memory hook. | Caps code chunks at 5–15 lines; forbids dumping full solutions unless asked; waits for learner response. | **Stateless & unmapped:** Same gaps as `study-tutor`—no prerequisite probing, no macro curriculum map, no local file state, and no distinction between urgent homework triage and deep CS fundamentals. |
| [`skills/code-coach/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/code-coach/SKILL.md) (formerly toggled via [`deprecated/toggle-code-coach/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/deprecated/toggle-code-coach/SKILL.md)) | Enforces 3 strict anti-atrophy postures with hard completion criteria: **1. Scaffold** (signatures + TODOs + `NotImplementedError` only), **2. Socratic** (isolate bug mechanism + end with exactly 1 question, zero fix diffs), **3. Toy** (demonstrate concepts exclusively in an unrelated domain). | **Strongest guardrail against giving answers too easily (Grievance E) and preachiness (Grievance F).** Deterministic completion criteria prevent the model from leaking production code or rambling. | **No curriculum or ingestion layer:** Operates purely on single-turn code generation, debugging, or concept queries; does not index lecture slides or schedule practice drills. |
| [`skills/scaffold-exercises/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/scaffold-exercises/SKILL.md) | Scaffolds `exercises/XX-section/XX.YY-exercise/{problem,solution,explainer}` directory trees with `readme.md` and `main.ts` validated by `pnpm ai-hero-cli internal lint`. | Clean structural separation of `problem/` (student workspace with TODOs), `solution/` (reference), and `explainer/` (concepts). | **Coupled to `ai-hero-cli`:** Hardcoded to Matt Pocock's internal TypeScript course linter (`pnpm ai-hero-cli internal lint`); not generalizable to arbitrary university courses (e.g., Groovy, C, Python, math) without modification. |

---

## Part 4: Mechanistic Mapping to Student Grievances & Unresolved Questions

This section maps the verified mechanisms from the audited primary sources directly to the six student grievances (A–F) and three unresolved questions (1–3) documented in `docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md`.

### 1. Mapping to the Six Student Grievances (A–F)

| Grievance (`SESSION_POSTMORTEM_AND_GRIEVANCES.md`) | Root Failure in `School Code` Session | Verified Primary-Source Mechanism that Solves It | Exact Source File Citation |
| :--- | :--- | :--- | :--- |
| **A. Lack of Clear Objectives & Dual-Layer Structure** <br>*(Blurred 80/20 immediate assignment survival with broad long-term CS fundamentals)* | Assistant mixed immediate homework completion with unanchored theoretical lectures, never separating the course trunk from task deliverables. | **1. Dual-Layer Workspace Separation:** Separate the macro dependency map (`.alvar/maps/<topic>.md` + `theory/01-core-concepts.md` Mermaid `graph TD`) from concrete milestone execution (`MISSION.md` + `practice/<project>/README.md`). <br>**2. Explicit Mode Routing:** Route upfront between **Track 1: Task/Exam Triage** (Gornik 80/20 bottleneck pruning + `study-notes-synthesizer` high-yield cram sheet) and **Track 2: Deep Trunk Mastery** (Alvar's `Probe -> Plan -> Teach` minimal dependency tree). | • `amosblomqvist/learnharness`: `docs/teaching-methodology.md` (§7b *The minimal tree*) <br>• `iannbing/skills-for-learning`: `skills/tutorial/SKILL.md` <br>• `skills/teach/MISSION-FORMAT.md` |
| **B. High Cognitive Overhead for Course Logistics** <br>*(Student forced to organize schedules/topics instead of doing repetitive hands-on practice)* | Assistant forced the student to steer what to study next instead of indexing course slides and serving drills directly. | **1. System-Absorbed Logistics Principle:** *"The system absorbs the logistics; the learner never does... Research, fact-checking, planning, ordering, source-finding — none of it is the learner's problem."* <br>**2. Dependency-Ordered Notes Synthesis:** Ingest raw lecture slides/notes and automatically reorganize them by concept dependency (`Plainly` $\to$ `Formally` $\to$ `Builds on` $\to$ `Confused with` + 3-depth self-test drills + explicit syllabus gap list). <br>**3. Dedicated Practitioner Mode:** Serve continuous, stateful practice problems (`problem` $\to$ `conclude`) drawn directly from the dependency graph. | • `amosblomqvist/learnharness`: `docs/teaching-methodology.md` (§7a *Effort allocation*, §10.6) <br>• `mohitagw15856/pm-claude-skills`: `skills/study-notes-synthesizer/SKILL.md` <br>• `amosblomqvist/learnharness`: `docs/architecture.md` (*Practitioner*) |
| **C. Large Unchecked Leaps & Pacing Assumptions** <br>*(Assistant made large jumps and advanced without verifying comprehension)* | Assistant dumped multi-concept explanations and assumed comprehension without checkpoints. | **1. Single-Reasoning-Step Invariant:** *"One reasoning step per turn. Stop. Quiz that step. Advance only on lock-in. Fail -> stay, or insert a prerequisite node."* <br>**2. Pre-Teaching DAG Approval Gate:** Present the Mermaid dependency DAG in Phase 2 and freeze until the learner explicitly approves the plan. <br>**3. Bracketed Binary-Search Probe:** Locate the exact floor and ceiling (`known | edge | unknown | blocked`) on every prerequisite strand before teaching node 1. | • `amosblomqvist/learn`: `skills/teach/SKILL.md` (Phases 1–3) <br>• `vasanthsreeram/Alvarmethod`: `skills/teach/SKILL.md` (*Hard rules*) |
| **D. The Asymmetric Correction Trap** <br>*(Stressed student lacked energy to correct off-track AI; AI treated silence as agreement)* | Assistant relied on the student typing long free-text corrections when it guessed wrong or drifted. | **1. Native Question-Tool Checkpoints (`question` / `quiz`):** Replace open-ended chat guessing with low-friction native UI pickers containing 3 diagnostic distractors + an automatic **`"I don't know"`** option (`__dont_know__`) + an optional talk-through note field. Clicking `"I don't know"` takes one keystroke and forces the agent to insert a prerequisite node rather than advancing. <br>**2. Isolation of Side Questions:** Allow 1–2 sentence clarification queries without mutating or derailing the main lesson plan. | • `amosblomqvist/learn`: `extensions/quiz.ts` (`DONT_KNOW_VALUE`) <br>• `vasanthsreeram/Alvarmethod`: `skills/teach/references/quiz-ui.md` <br>• `amosblomqvist/learnharness`: `docs/architecture.md` (*Side questions*) |
| **E. Giving Answers Too Easily vs. Active Practice** <br>*(Assistant defaulted to generating solutions instead of holding a Socratic loop)* | Assistant wrote complete code or direct answers when asked about homework or concepts. | **1. Three Strict Postures (`code-coach`):** Enforce `Scaffold` (signatures + TODOs + `NotImplementedError` only, zero business logic), `Socratic` (explain failure mechanism + end with 1 question, zero fix diffs), and `Toy` (unrelated domain examples only). <br>**2. 5-Level Hint Escalation Ladder (`guide`):** Escalate from Reframe (L1) $\to$ Narrow (L2) $\to$ Point (L3) $\to$ Pattern Snippet (L4) $\to$ Full Solution only after L1–L4 fail or on explicit override (L5), logging L3+ struggles as weak points. | • `skills/code-coach/SKILL.md` <br>• `iannbing/skills-for-learning`: `skills/guide/SKILL.md` (*When the learner is stuck*) |
| **F. Unsolicited "Life Coaching" & Preachiness** <br>*(Assistant generated motivational reassurance and multi-week life/semester plans)* | Assistant padded responses with emotional reassurance (*"you're doing great"*) and unsolicited semester scheduling. | **1. Anti-Meta-Narration & Efficiency Mandate:** *"Every sentence is either installing understanding or it is overhead; overhead must earn its place... No meta-narration of the method, no labeled segments for their own sake."* <br>**2. Persistent Anti-Slop Voice Contract (`.alvar/LEARNER.md`):** Record hated LLM habits (no motivational fluff, no unsolicited schedules) once in `LEARNER.md` and read it at Turn 0 of every session. <br>**3. Short Compass Rule (`MISSION-FORMAT.md`):** *"If MISSION.md runs past a screen, it has stopped being a compass and started being a plan."* | • `amosblomqvist/learnharness`: `docs/teaching-methodology.md` (§8, §10.5) <br>• `vasanthsreeram/Alvarmethod`: `skills/learn-profile/SKILL.md` <br>• `skills/teach/MISSION-FORMAT.md` |

---

### 2. Answers to the Three Unresolved Architectural Questions

#### Question 1: Pacing & Checkpoint Architecture
> *How should the system determine when to continue vs. when to pause and go deeper? (e.g., explicit micro-checkpoints, mode switching between fast-task and deep-learning, or strict question-response gates).*

**Verified Primary-Source Solution:**
1. **Upfront Track Selection (Turn 0 Gate):** At session start, use the harness's native `question` tool (`ask_user_question` / `question`) to select the execution track:
   * **Deep-Learning Track (`Probe -> Plan -> Teach`):** Enforces Alvar's strict per-node gate (`Motivate -> Establish -> Connect -> Quiz-check`). The agent is forbidden from advancing to Node $N+1$ until the learner passes the graded `question` check on Node $N$.
   * **Fast-Task / Assignment Triage Track (`Scaffold + Hint Ladder`):** Uses `code-coach` postures (`Scaffold`, `Socratic`, `Toy`) paired with `iannbing/guide`'s 5-level hint escalation ladder and `ahmed3bead/teach-me`'s unit-boundary check invitation (*"That completes the unit. Would you like a short optional check, or shall we continue?"*).
2. **State-Transition Rules on Check Outcomes (`vasanthsreeram/Alvarmethod`):**
   * **Pass (`correct + sound reason`):** Mark node `known` in `.alvar/maps/<topic>.md` and advance to the next DAG node.
   * **Shallow Pass or Near-Miss (`edge`):** Issue one tighter applied follow-up question before advancing.
   * **Fail or `"I don't know"` (`unknown` / `blocked`):** Pause immediately, dynamically insert a prerequisite node into the Mermaid DAG, and teach the prerequisite.

#### Question 2: Curriculum Ingestion & Practice Generation
> *What is the optimal pipeline for the AI to ingest local course slides/textbooks, extract the core mental model, and immediately produce targeted, repetitive practice drills without conversational drift?*

**Verified Primary-Source Solution:**
Combine `ahmed3bead/teach-me`'s source inspection ledger, `mohitagw15856/pm-claude-skills`'s dependency synthesizer, and `iannbing/skills-for-learning`'s practice generator into a 4-stage local file pipeline:
1. **Stage 1 — Local Corpus Inspection (`teach-me` Source-Grounded Gate):** Read the local course directory (syllabi, lecture slide PDFs, past assignments) and write a coverage index mapping which files cover which topics, explicitly flagging syllabus gaps (`⚠ Gaps in your materials`).
2. **Stage 2 — Dependency-Tree Extraction (`study-notes-synthesizer` + Alvar `Plan`):** Reject chronological lecture order. Extract the **20% Trunk (Unconditional Truths / Core Mental Models)** and **80% Branches (Applied Modules & Edge Cases)** into a Mermaid `graph TD` dependency map saved to disk, with `Plainly` $\to$ `Formally` $\to$ `Builds on` $\to$ `Confused with` entries.
3. **Stage 3 — Three-Depth Practice Drill Generation (`study-notes-synthesizer` + `scaffold-exercises`):** For the target node or exam topic, immediately generate a repetitive drill bank split across three depths:
   * **Depth 1 (Recall / Invariant):** Graded MCQ via the native `question` tool using Alvar's 4-step distractor mutation rules.
   * **Depth 2 (Application / Code Scaffold):** Hands-on problem stub (`problem/` with signatures and `TODO`s via `code-coach` Scaffold posture) with a runnable verification command.
   * **Depth 3 (Contrast / Why X not Y):** Side-by-side confusable-pair debugging or trade-off scenario.
4. **Stage 4 — Stateful Weak-Point Loop (`iannbing/guide` + `skills/teach/learning-records`):** Log any drill requiring Level 3+ hints or answered incorrectly into `learning-records/NNNN-<slug>.md` (or `.guide/learner-profile.md`) so the next practice batch automatically weights drills toward shaky nodes without conversational re-planning.

#### Question 3: Guardrails Against AI Presumption
> *What prompt constraints effectively prevent the model from slipping into unsolicited life coaching, task planning, or long explanatory monologues?*

**Verified Primary-Source Solution:**
1. **Positive Completion Criteria Over Negative Prohibitions (`skills/code-coach/SKILL.md` & `docs/research/agents-rule-friction-retro.md`):**
   * As established in `agents-rule-friction-retro.md`, stacking negative rules triggers the "pink elephant" attention leak. Instead, use `code-coach`'s positive **Completion Criterion** pattern at the end of every workflow phase:
     * *Probe Turn Completion Criterion:* The turn outputs 1–3 graded questions via the native `question` tool and terminates immediately with zero explanatory prose.
     * *Plan Turn Completion Criterion:* The turn outputs a 3-sentence approach summary and one Mermaid `graph TD` (max 7 nodes), asks for plan approval via the `question` tool, and terminates with zero lesson content.
     * *Teach Turn Completion Criterion:* The turn teaches exactly one DAG node (max 2–3 short paragraphs or 5–15 lines of code) and terminates with a single lock-in `question` tool call.
2. **Hard Ban on Meta-Narration & Emotional Coaching (`learnharness/docs/teaching-methodology.md` §8 & §10.5):**
   * Embed the explicit efficiency rule: *"Every sentence is either installing understanding or it is overhead. Do not narrate the teaching method, do not output motivational reassurance, and do not generate multi-week study schedules."*
3. **Persistent Learner Profile Contract (`.alvar/LEARNER.md` / `NOTES.md`):**
   * Store learner constraints (`no life coaching`, `no semester schedules`, `system absorbs all logistics`, `hands-on drills first`) in a workspace file read at Turn 0 so the user never has to repeat behavioral corrections during high-stress study sessions.

---

## Primary Source Citations

1. **Eero Alvar (`@amosblomqvist`)**, *learn: My AI learning system (`.pi` configuration, skills, extensions, and subagents)*, GitHub, 2026. [`https://github.com/amosblomqvist/learn`](https://github.com/amosblomqvist/learn)
2. **Eero Alvar (`@amosblomqvist`)**, *learnharness: Agent harness for learning difficult things*, GitHub, 2026. [`https://github.com/amosblomqvist/learnharness`](https://github.com/amosblomqvist/learnharness) — Specifically [`docs/architecture.md`](https://raw.githubusercontent.com/amosblomqvist/learnharness/main/docs/architecture.md) and [`docs/teaching-methodology.md`](https://raw.githubusercontent.com/amosblomqvist/learnharness/main/docs/teaching-methodology.md).
3. **Vasanth Sreeram (`@vasanthsreeram`)**, *Alvarmethod: One-to-one AI teaching skills for Codex, Claude Code, Grok, Pi, and OpenCode*, GitHub, 2026. [`https://github.com/vasanthsreeram/Alvarmethod`](https://github.com/vasanthsreeram/Alvarmethod)
4. **Iann Bing (`@iannbing`)**, *skills-for-learning (`tutorial`, `guide`, `explain`, `walkthrough`)*, GitHub, 2026. [`https://github.com/iannbing/skills-for-learning`](https://github.com/iannbing/skills-for-learning)
5. **Mohit Agarwal (`@mohitagw15856`)**, *pm-claude-skills: `study-notes-synthesizer/SKILL.md`*, GitHub, 2026. [`https://github.com/mohitagw15856/pm-claude-skills/blob/main/skills/study-notes-synthesizer/SKILL.md`](https://github.com/mohitagw15856/pm-claude-skills/blob/main/skills/study-notes-synthesizer/SKILL.md)
6. **Ahmed Ebead (`@ahmed3bead`)**, *teach-me: Open-source AI tutor and source-grounded education plugin*, GitHub, 2026. [`https://github.com/ahmed3bead/teach-me`](https://github.com/ahmed3bead/teach-me)
7. **Matt Pocock (`@mattpocock`)**, *skills: `skills/productivity/teach/SKILL.md` and `skills/misc/scaffold-exercises/SKILL.md`*, GitHub, 2026. [`https://github.com/mattpocock/skills`](https://github.com/mattpocock/skills)
8. **Dersu Local Skills & Research Vault**, [`skills/teach/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/SKILL.md), [`skills/study-tutor/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/study-tutor/SKILL.md), [`skills/code-tutor/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/code-tutor/SKILL.md), [`skills/code-coach/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/code-coach/SKILL.md), [`skills/scaffold-exercises/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/scaffold-exercises/SKILL.md), [`docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md), and [`docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/Branch%20%E2%80%A2%20AI%20Knowledge%20Tree%20Mapping%20Workflow.pdf).
