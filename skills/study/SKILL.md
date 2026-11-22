---
name: study
description: Route and advise on studying an academic course or technical subject. Inspects the study folder and invokes `study-map`, `study-topic`, or `study-practice`.
argument-hint: "[optional: topic, assignment, or goal]"
---

# Study (Workspace Router & Compass)

Treat the current working directory as a stateful study workspace. Absorb 100% of organizational logistics so the learner spends 100% of their energy on concepts and practice problems.

## Workspace Layout

All `study*` skills read and write this shared structure inside the user's active study folder:

```text
./
├── TREE.md                        # 1-screen Semantic Tree (Roots -> 20% Trunk -> Branches -> Cross-Links)
├── COURSE.md                      # Optional Course Overlay (deadlines, slide PDFs, problem sets, syllabus gaps)
├── notes/                         # Clean Markdown + LaTeX study guides and zoomed-in topic sub-trees
├── visuals/                       # SVG diagrams, cropped slide figures, and interactive HTML visualizers
├── practice/                      # Hands-on practice sets, code projects, and local auto-save server
│   ├── server.mjs                 # Created once on demand; serves all HTML pages and writes results to disk
│   ├── set-NN-<slug>.html         # Interactive HTML quiz, flashcard, LaTeX, and photo-paste pages
│   ├── proj-NN-<slug>/            # Runnable starter code and test scripts for coding/project problems
│   └── submissions/               # Auto-saved photos/screenshots of handwritten work
└── learning-records/              # Persistent memory across sessions
    ├── results.jsonl              # Auto-saved clicks, answers, and photo submissions from HTML practice pages
    └── NNNN-<slug>.md             # Short logs of demonstrated mastery and specific weak spots
```

## Execution Steps

1. **Inspect Workspace State Silently**:
   - Check if `TREE.md` and `COURSE.md` exist.
   - Scan the directory for unindexed course files (new lecture slide PDFs, syllabi, exercise booklets, homework specs) that do not appear in `TREE.md` or `COURSE.md`.
   - Read the latest files in `learning-records/` (including any new lines in `learning-records/results.jsonl`) to identify shaky nodes or unfinished practice sets.

2. **Recommend and Route via Native `question` Tool**:
   - Present a 3-line status summary of the workspace (current `Trunk`/`Branch` progress, any newly detected files, and the highest-priority deadline or shaky node).
   - Call the harness's native `question` tool with concrete options tailored to the workspace state (put the recommended action first with `(Recommended)`):
     - **Setup or Update Map (`study-map`)**: Recommended when `TREE.md` is missing or new slide/homework files were added to the folder.
     - **Learn a Concept Step-by-Step (`study-topic`)**: Recommended when a required `Root`, `Trunk`, or `Branch` node is `unprobed` or `blocked`.
     - **Practice Problems or Projects (`study-practice`)**: Recommended when the concept node is ready for problem repetition, homework execution, exam prep, or weak-spot drilling.
   - If the user already stated a clear target in their prompt (for example, *"give me practice problems on monitors"* or *"map this course folder"*), skip the menu and invoke the matching skill immediately.

3. **Invoke Target Skill**:
   - Call the `skill` tool for `study-map`, `study-topic`, or `study-practice` and begin Step 1 of that skill in the same turn.
   - **Completion Criterion**: The workspace state is inspected, the target skill (`study-map`, `study-topic`, or `study-practice`) is loaded, and execution has transitioned with zero motivational filler or multi-week schedules.
