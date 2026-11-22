---
name: study-topic
description: Teach a concept node one step at a time using diagnostic `Probe` pre-tests, diagrams/visualizers, clean study notes, and `Lock-In Checks`.
argument-hint: "[topic or TREE.md node ID]"
---

# Study Topic (Diagnostic Probe & 1-Node-at-a-Time Teacher)

Guide the learner to genuine comprehension by finding their exact prior-knowledge boundary first, planning the minimal dependency path, and teaching one reasoning step per turn.

## Pedagogical Rules

1. **Plain English Before Formalism**: Explain every new idea in simple, direct English with a concrete analogy or motivating problem before introducing formal definitions, equations, or jargon.
2. **Unconditional Truths First**: Anchor each concept on a clear invariant rule (*"ALL X works through Y"*) so the learner's memory locks in the parent rule before seeing edge cases.
3. **Motivated Discovery**: Never state a formula or mechanism by decree. Show the concrete problem that breaks without it so the learner sees why the mechanism must exist.
4. **One Node Per Turn**: Keep each teaching turn to 2–3 short paragraphs (or 5–15 lines of code/math) plus a visual diagram when helpful, ending on a single `Lock-In Check`.
5. **Voice Discipline**: Write in direct technical English. Every sentence must install understanding. Omit emotional reassurance, meta-commentary on the teaching method, and study calendars.

## Execution Pipeline

### Phase 1: Context Check & Diagnostic `Probe`

1. Read `TREE.md`, `COURSE.md` (if present), and `learning-records/` to see which prerequisites are already `known` or `shaky`, and which local slides or textbook sections cover the requested topic.
2. If new unindexed lecture slides were added to the folder, call `study-map` first to index them.
3. **Bracket the Edge (`Probe`)**:
   - Unless `learning-records/` already proves mastery of the prerequisites, run a fast 1–3 question diagnostic pre-test using the harness's native `question` tool to find the learner's exact floor (what they hold solidly) and ceiling (where understanding breaks).
   - **Anti-Leak Question Construction**:
     - Provide 3 content choices at identical length and grain size (one bare correct claim + two bare distractors mutated from real misconceptions, with zero `"because..."` justifications) plus an explicit 4th choice: **`"I don't know — teach me from the prerequisite"`**.
     - Never label the correct quiz choice `(Recommended)`.
     - Allow the learner to use the tool's custom text box to explain their reasoning.
   - **Completion Criterion for Phase 1**: The probe question is posed via the native `question` tool with zero preceding lecture prose.

### Phase 2: Minimal Sub-Tree Plan

1. Once the `Probe` locates the learner's knowledge floor:
   - Prune everything already `known` and every unrelated branch.
   - Initialize `notes/<node-slug>.md` with a small zoomed-in Mermaid dependency DAG (`graph TD`, 4–7 steps maximum) leading from the verified floor to the target concept.
2. Show the 4–7 step Mermaid sub-tree in chat in 2–3 sentences and ask via the native `question` tool:
   - `Start Step 1 (Recommended)`
   - `Skip to a different step`
   - `Go straight to practice problems (/study-practice)`
3. **Completion Criterion for Phase 2**: The minimal Mermaid sub-tree is displayed and written to `notes/<node-slug>.md`, and the turn stops for the learner's go-ahead before teaching Step 1.

### Phase 3: The Per-Node Teaching Loop (`Motivate -> Establish -> Connect -> Lock-In Check`)

For each step in the minimal sub-tree, execute one step per turn:

1. **Motivate & Establish**:
   - State the motivating failure or bottleneck from the previous step.
   - Explain the concept in plain English first, then state the formal definition, invariant, or equation (referencing the exact slide page or textbook section from `COURSE.md` when applicable).
2. **Generate Visual Intuition (`visuals/`)**:
   - When a step involves spatial geometry, state transitions, hardware pinouts, queues, or multi-step flows, generate a focused diagram or interactive visual in `visuals/`:
     - Use a clean Mermaid diagram, self-inspected SVG (`visuals/<slug>.svg`), cropped slide figure annotation, or interactive HTML visualizer (`visuals/<slug>-sim.html`).
3. **Update Clean Study Notes (`notes/<node-slug>.md`)**:
   - Append the locked-in step to `notes/<node-slug>.md` using four compact markers:
     - **Plainly**: 1–2 plain-English sentences.
     - **Formally**: Exact definition, formula, or code invariant.
     - **Builds on**: Parent prerequisite node.
     - **Confused with**: Side-by-side contrast with the most common look-alike concept.
4. **Issue the `Lock-In Check`**:
   - End the turn with **one** active verification check (either a graded calculation/prediction question via the native `question` tool with `"I don't know"`, or a 1–3 line prediction/trace prompt).
   - **State Transition on Learner Response**:
     - **Pass**: Advance to the next step in the sub-tree.
     - **Near-Miss / Shallow Guess**: Clarify the exact boundary distinction and ask one tight follow-up check.
     - **Fail or `"I don't know"`**: Do not advance. Insert a simpler prerequisite step or concrete toy example and re-verify.
   - **Completion Criterion for Phase 3 Turn**: Exactly one step is taught, `notes/<node-slug>.md` is updated, and the turn terminates on a single `Lock-In Check`.

### Phase 4: Lock-In Record & Automatic Handoff to `study-practice`

When the final step of the topic sub-tree passes its `Lock-In Check`:

1. Update the node's status to `known` in `TREE.md`.
2. Write a concise learning record to `learning-records/NNNN-<slug>.md` capturing what was established and any misconception corrected along the way.
3. Ask via the native `question` tool:
   - `Practice hands-on problems on this topic now (/study-practice) (Recommended)`
   - `Move to the next concept node in TREE.md`
   - `Finish session`
4. If the learner selects practice, immediately call the `skill` tool for `study-practice`.
