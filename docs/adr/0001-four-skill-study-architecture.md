# Four-Skill Study Architecture with On-Demand Local Auto-Save Backend

Status: accepted

We separate academic course and subject mastery from Matt Pocock's `skills/teach` skill by moving `skills/study-tutor` to `deprecated/study-tutor` and introducing four pure-Markdown `study*` skills (`study`, `study-map`, `study-topic`, `study-practice`).

## Context and Problem

In `School Code` (`SESSION_POSTMORTEM_AND_GRIEVANCES.md`), a single free-form tutoring conversation failed across 205 turns:
1. It blurred long-term subject fundamentals (`Trunk`) with immediate homework and exam deadlines (`Course Overlay`).
2. It offloaded study planning and file hunting onto the student instead of indexing local slides and exercise PDFs.
3. It dumped multi-week lecture walls and unsolicited schedules instead of serving step-by-step checks and repetitive practice problems.

Meanwhile, Matt Pocock's `skills/teach/SKILL.md` authors standalone HTML essays (`./lessons/0001-*.html`) whose in-browser HTML quizzes cannot report results back to the CLI/IDE agent. Conversely, `skills/study-tutor/SKILL.md` is a stateless 32-line prompt with no pre-test probing, no concept tree, and an always-loaded description that collides with stateful study commands. Finally, because `dersu-agent-skills` is synced across devices and accounts as portable Markdown skills, the skills themselves cannot depend on external script paths inside this repository.

## Considered Options

1. **Modify `skills/teach/SKILL.md` in place:** Rejected because authoring full HTML lesson essays per turn conflicts with fast problem drilling, and static HTML quizzes without a local endpoint hide learner answers from the agent.
2. **One monolithic `/study` skill:** Rejected under `/writing-for-agents` (*Splitting by Sequence*) because keeping setup/mapping steps and teaching/drilling steps in the same prompt pulls the agent toward premature completion (rushing syllabus ingestion to start lecturing).
3. **Four pure-Markdown skills (`study`, `study-map`, `study-topic`, `study-practice`) that scaffold a unified workspace (`TREE.md`, `COURSE.md`, `notes/`, `visuals/`, `practice/server.mjs`, `learning-records/`) on demand:** Accepted.

## Decision

1. **Keep `skills/teach` and `skills/code-tutor` untouched; move `skills/study-tutor` to `deprecated/study-tutor`.**
2. **Expose four pure-Markdown `study*` skills:**
   - `study`: Entry router and advisor. Inspects `TREE.md`, `COURSE.md`, unindexed course files, and `learning-records/`, recommends the next action via the native `question` tool, and invokes the target skill.
   - `study-map`: Setup and incremental mapper. Keeps `TREE.md` under one screen for the macro `Semantic Tree` (`Root -> 20% Trunk -> Branch -> Leaf -> Cross-Link`), and writes/updates `COURSE.md` for class logistics (`Course Overlay`: deadlines, 80/20 filtered slides/textbooks, problem sets, and missing syllabus gaps).
   - `study-topic`: Diagnostic concept teacher. Runs a binary-search `Probe` via the native `question` tool (with `"I don't know"`), builds a 4–7 step minimal sub-tree inside `notes/<slug>.md`, teaches one node per turn with plain English, diagrams/visualizers in `visuals/`, and a `Lock-In Check`, and hands off to `study-practice`.
   - `study-practice`: Pure problem, flashcard, and project engine. Supports (A) interactive HTML practice pages (`practice/set-NN-<slug>.html`), (B) guided 1-on-1 chat problems, and (C) runnable code/project folders (`practice/proj-NN-<slug>/`).
3. **Generate `practice/server.mjs` fresh once per study workspace:** When creating HTML quizzes, flashcards, LaTeX answer inputs, or `Ctrl+V` handwritten-work photo dropzones, `study-practice` writes a zero-dependency ~45-line Node.js server (`practice/server.mjs`) directly inside the active study folder. All HTML pages in the folder post clicks, answers, and pasted images to `/api/record` and `/api/upload`, saving them automatically to `learning-records/results.jsonl` and `practice/submissions/` with zero copy-pasting.
