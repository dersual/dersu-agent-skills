---
name: study-practice
description: Run hands-on problem sets, flashcard decks, exam drills, or mini-projects with zero lecturing. Supports both auto-saving interactive HTML practice pages (`practice/set-NN-<slug>.html` backed by an on-demand local `practice/server.mjs`) and guided chat/code problem solving accepting code, LaTeX, prose, or photos of handwritten work (`Practice Artifacts`). Logs results and weak spots to `learning-records/`.
argument-hint: "[topic, TREE.md node, homework/exercise file, or 'html' / 'chat' / 'project']"
---

# Study Practice (Problem, Flashcard & Project Drill Engine)

Deliver high-repetition, hands-on practice immediately. Never lecture, never write multi-week schedules, and never dump full solutions before the learner attempts the work.

## Core Invariants

1. **Problem 1 on Turn 1**: Your first response must deliver either **Problem 1** (in chat or a scaffolded code folder) or open a **ready-to-solve HTML Practice Page** (`practice/set-NN-<slug>.html`). Zero meta-plans or preamble.
2. **Real Course Problems First**: When `COURSE.md` or local course files exist (exercise booklets like `eb1.pdf`–`eb9.pdf`, homework specs, past exams, textbook chapters), extract problems directly from those primary files before inventing synthetic ones. Mix in retry variations for past weak spots recorded in `learning-records/`.
3. **Three Practice Depths**:
   - **Depth 1 (Recall & Invariants)**: Flashcards and multiple-choice questions testing core `Trunk` rules and boundary conditions.
   - **Depth 2 (Application, Traces, Proofs & Code)**: Execution traces, math/statistics derivations, LaTeX proofs, SQL/Relational Algebra queries, and runnable code problems.
   - **Depth 3 (Contrast & Bug Diagnosis — "Why X Not Y")**: Confusable pairs side-by-side, broken proofs, or race-condition/buggy code where the learner must pinpoint the exact failure step.
4. **All `Practice Artifacts` Accepted**: Evaluate code files, terminal test runs, LaTeX math, plain-text reasoning, and uploaded or pasted photos/screenshots of handwritten work (`practice/submissions/*.png`).

---

## Three Execution Formats

Pick the format that matches the user's request or the nature of the material (or let the user switch at any time):

### Format A: Interactive HTML Practice Page (`practice/set-NN-<slug>.html`)

Use when the learner wants a **batch of problems, flashcards, multiple-choice drills, or a mock quiz/exam** on a clean page where every click, typed LaTeX answer, and pasted photo is recorded automatically to disk with **zero copy-pasting**.

#### 1. Ensure `practice/server.mjs` Exists Once in the Study Workspace
Check if `./practice/server.mjs` exists in the current working directory. If not, create `./practice/server.mjs` once using this exact zero-dependency Node.js template (it serves all HTML/SVG/PNG files in the study workspace and auto-saves every interaction to `./learning-records/results.jsonl` and `./practice/submissions/`):

```javascript
import http from "node:http";
import fs from "node:fs";
import path from "node:path";

const ROOT = process.cwd();
const PORT = Number(process.env.STUDY_PORT || 4321);
const MIME = {
  ".html": "text/html; charset=utf-8",
  ".js": "text/javascript; charset=utf-8",
  ".css": "text/css; charset=utf-8",
  ".json": "application/json; charset=utf-8",
  ".svg": "image/svg+xml",
  ".png": "image/png",
  ".jpg": "image/jpeg",
};

fs.mkdirSync(path.join(ROOT, "learning-records"), { recursive: true });
fs.mkdirSync(path.join(ROOT, "practice", "submissions"), { recursive: true });

function readBody(req) {
  return new Promise((resolve, reject) => {
    const chunks = [];
    req.on("data", (c) => chunks.push(c));
    req.on("end", () => resolve(Buffer.concat(chunks).toString("utf8")));
    req.on("error", reject);
  });
}

http.createServer(async (req, res) => {
  res.setHeader("Access-Control-Allow-Origin", "*");
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, OPTIONS");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type");
  if (req.method === "OPTIONS") { res.writeHead(204); return res.end(); }

  if (req.method === "POST" && req.url === "/api/record") {
    const payload = JSON.parse(await readBody(req));
    const entry = { timestamp: new Date().toISOString(), ...payload };
    fs.appendFileSync(path.join(ROOT, "learning-records", "results.jsonl"), JSON.stringify(entry) + "\n");
    res.writeHead(200, { "Content-Type": "application/json" });
    return res.end(JSON.stringify({ ok: true }));
  }

  if (req.method === "POST" && req.url === "/api/upload") {
    const { setId, itemId, dataUrl, notes } = JSON.parse(await readBody(req));
    const match = /^data:image\/(\w+);base64,(.+)$/.exec(dataUrl || "");
    if (!match) { res.writeHead(400); return res.end(JSON.stringify({ ok: false })); }
    const filename = `${setId || "set"}-${itemId || "item"}-${Date.now()}.${match[1]}`;
    const relPath = path.join("practice", "submissions", filename);
    fs.writeFileSync(path.join(ROOT, relPath), Buffer.from(match[2], "base64"));
    const entry = { timestamp: new Date().toISOString(), setId, itemId, type: "image-submission", imagePath: relPath, notes };
    fs.appendFileSync(path.join(ROOT, "learning-records", "results.jsonl"), JSON.stringify(entry) + "\n");
    res.writeHead(200, { "Content-Type": "application/json" });
    return res.end(JSON.stringify({ ok: true, imagePath: relPath }));
  }

  const cleanUrl = decodeURIComponent((req.url || "/").split("?")[0]);
  const filePath = path.resolve(ROOT, "." + cleanUrl);
  if (!filePath.startsWith(ROOT) || !fs.existsSync(filePath) || fs.statSync(filePath).isDirectory()) {
    res.writeHead(404); return res.end("Not found");
  }
  res.writeHead(200, { "Content-Type": MIME[path.extname(filePath)] || "application/octet-stream" });
  fs.createReadStream(filePath).pipe(res);
}).listen(PORT, "127.0.0.1", () => {
  console.log(`Study server running at http://127.0.0.1:${PORT}`);
});
```

#### 2. Author `practice/set-NN-<slug>.html` & Launch Server
- Start `node practice/server.mjs` in the background if it is not already listening on `127.0.0.1:4321`, and open `http://127.0.0.1:4321/practice/set-NN-<slug>.html` for the user.
- Every HTML practice page must wire its interactions directly to `/api/record` and `/api/upload`:
  - **Multiple-Choice & Flashcards**: Clicking an option or self-grading a flashcard (`Got It` / `Shaky` / `Missed`) immediately sends `fetch('/api/record', { method: 'POST', headers: {'Content-Type': 'application/json'}, body: JSON.stringify({ setId, itemId, type, prompt, userAnswer, correctAnswer, isCorrect, confidence }) })`.
  - **Math / LaTeX / Short-Answer Boxes**: Submitting text or LaTeX immediately posts to `/api/record`.
  - **Handwritten Photo Paste (`Ctrl+V`) / Drag-and-Drop Box**: Include a paste/drop target on open-ended math/diagram questions that reads the image via `FileReader.readAsDataURL` and posts to `/api/upload`, displaying a green `"Saved to practice/submissions/..."` badge on the page.
- When the user returns to chat and says `"done"`, `"check my answers"`, or `"help on Q3"`, read `learning-records/results.jsonl` (and inspect any saved images in `practice/submissions/` via the `read` tool) to grade their work and walk through errors.

---

### Format B: Guided 1-on-1 Problem Solving in Chat

Use when working through complex derivations, proofs, execution traces, or homework questions one problem at a time:

1. Present **one problem** clearly (citing its source, e.g., `eb6.pdf Q2`), and stop.
2. Wait for the user's `Practice Artifact` (typed text, LaTeX, code snippet, or an attached/pasted image of handwritten work).
3. Inspect the exact steps of their work.

---

### Format C: Code & Mini-Project Milestones (`practice/proj-NN-<slug>/`)

Use when practicing programming, concurrency, SQL, R statistics scripts, or systems implementation:

1. Create `practice/proj-NN-<slug>/` containing:
   - `README.md` with clear problem requirements and 2–4 ordered milestones.
   - Starter code files containing structural signatures and `TODO` comments (zero pre-solved logic).
   - A fast, runnable test or verification script.
2. Tell the user which file to edit and how to run the check (or run the check for them when they say they are ready).

---

## Step-Diagnosis & Graduated Hint Protocol (When the Learner Makes a Mistake or Gets Stuck)

Never dump the full solved answer when the learner errs or says they are stuck. Follow this strict escalation:

1. **Isolate the Exact Step**: Point out what was right in their work first, then name the exact line, algebraic step, or assumption where the logic diverged.
2. **Give One Small Hint at a Time**:
   - **Hint 1 (Reframe / Invariant)**: Remind them of the governing `Trunk` rule or ask what happens at a concrete boundary input.
   - **Hint 2 (Narrow Mechanism)**: Point to the specific variable, queue, operator, or theorem required for that step.
   - **Hint 3 (Unrelated Toy Example)**: Show a 4–6 line working example of the mechanic in an unrelated toy domain.
   - **Full Walkthrough (Only after Hints 1–3 or explicit learner request)**: Walk through the complete solution step-by-step and immediately queue a similar follow-up problem so the learner executes the pattern themselves.
3. **Missing `Trunk` Foundation Check**:
   - If the learner's mistake shows they never learned the underlying `Trunk` concept, call the native `question` tool with two choices:
     1. `Give me a quick 4-sentence crash explanation right here and keep practicing`
     2. `Switch to /study-topic to learn this foundation step-by-step with visuals`
   - If they choose option 2, call the `skill` tool for `study-topic`.

---

## Recording Weak Spots & Updating `TREE.md`

After grading an HTML practice set (`learning-records/results.jsonl`) or finishing a chat/code problem batch:

1. Update the node's status in `TREE.md` (`known` if solved cleanly without heavy hints; `shaky` if hints or errors occurred).
2. Write or update `learning-records/NNNN-<slug>.md` recording:
   - Which problems were completed (`set-NN` or `ebX QY`).
   - Exact misconceptions or weak spots uncovered (so the next `study-practice` run automatically generates a retry problem on that weak spot).
3. **Completion Criterion**: Every learner submission in `learning-records/results.jsonl`, `practice/submissions/`, or chat is diagnosed step-by-step, weak spots are logged to `learning-records/NNNN-<slug>.md`, and `TREE.md` reflects current mastery.
