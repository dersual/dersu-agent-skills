# Handoff: Study Suite (`study*`) & Research Synthesis -> Next Phase (`code-tutor` / `code-coach` / `code-mentor`)

**Date:** 2026-11-22  
**Repository:** `C:\Users\dersu\Code Stuff\dersu-agent-skills`  
**Commits Landed in This Session:**
- `731c9cd`: `feat(study): add 4-skill study suite, domain glossary, ADR, and research reports`
- `36f8f69`: `fix(study): harden local auto-save server and trim skill pointer descriptions`

---

## 1. Conversation & Session Locations (Direct Links & IDs)

### A. Current OpenCode Session (Where `study*` Was Designed & Built)
- **Primary Session ID:** `ses_e0085de24ffeu4WK3es3NF3NFM`
- **Background Research Subagent Session IDs:**
  - `ses_e0084ef45ffezidBxw064eWxds` (Primary-source GitHub verification of external learning repos)
  - `ses_e0078b6e3ffeHPN5W9iwKtz61s` (Forensic autopsy of `School Code` transcript, YouTube videos, and cognitive science papers)
- **Code-Review Subagent Session IDs:**
  - `ses_dfc71f7e0ffel1aHhT4tujdnC9` (Standards & `/writing-for-agents` audit)
  - `ses_dfc71f7dbffeW0oxj2WHfqo55c` (Spec fidelity audit)
- **Local OpenCode Session Database & Storage:**
  - **SQLite Session DB:** [`C:\Users\dersu\.local\share\opencode\opencode.db`](file:///C:/Users/dersu/.local/share/opencode/opencode.db) (Query table `session` / `message` / `part` where `session_id = 'ses_e0085de24ffeu4WK3es3NF3NFM'`, or resume in OpenCode CLI via `opencode -s ses_e0085de24ffeu4WK3es3NF3NFM`)
  - **OpenCode Data Directory:** [`C:\Users\dersu\.local\share\opencode\`](file:///C:/Users/dersu/.local/share/opencode/)

### B. Originating Antigravity `School Code` Session (The 205-Step Post-Mortem Input)
- **Antigravity Conversation ID:** `c1bc5e66-388e-4dae-9701-9bb2a7ec2694`
- **Compact Transcript JSONL:** [`C:\Users\dersu\.gemini\antigravity-cli\brain\c1bc5e66-388e-4dae-9701-9bb2a7ec2694\.system_generated\logs\transcript.jsonl`](file:///C:/Users/dersu/.gemini/antigravity-cli/brain/c1bc5e66-388e-4dae-9701-9bb2a7ec2694/.system_generated/logs/transcript.jsonl)
- **Full Transcript JSONL:** [`C:\Users\dersu\.gemini\antigravity-cli\brain\c1bc5e66-388e-4dae-9701-9bb2a7ec2694\.system_generated\logs\transcript_full.jsonl`](file:///C:/Users/dersu/.gemini/antigravity-cli/brain/c1bc5e66-388e-4dae-9701-9bb2a7ec2694/.system_generated/logs/transcript_full.jsonl)
- **Target Course Workspace:** [`C:\Users\dersu\Code Stuff\School Code`](file:///C:/Users/dersu/Code%20Stuff/School%20Code)

---

## 2. All Files Created or Modified in This Session

### Research & Post-Mortem Inputs / Reports (`docs/research/`)
1. [`docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/Branch%20%E2%80%A2%20AI%20Knowledge%20Tree%20Mapping%20Workflow.pdf): Gemini research session export covering Semantic Tree / Pareto 80/20 Curriculum Mapping, Ausubel (1960), Collins & Quillian (1969), Novak & Gowin (1984), Eero Alvar (`amosblomqvist/learn`), Aleks Gornik's engineering workflow, and Matt Pocock's `teach` skill.
2. [`docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md): The 6 student grievances (A–F) and 3 unresolved architectural questions from the `School Code` catch-up session.
3. [`docs/research/learning-skills-primary-source-verification.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/learning-skills-primary-source-verification.md): Live GitHub primary-source verification of `amosblomqvist/learn`, `amosblomqvist/learnharness`, `vasanthsreeram/Alvarmethod`, `mohitagw15856/pm-claude-skills`, and local teaching skills.
4. [`docs/research/deep-learning-architecture-and-school-autopsy.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/deep-learning-architecture-and-school-autopsy.md): Deep turn-by-turn forensic autopsy of the 205-step `School Code` transcript, full extraction of Eero Alvar's (`watch?v=kzcI5F4tGiU`) and Aleks Gornik's (`watch?v=GPM5MgFEkpk`) YouTube workflows, analysis of the 3 cognitive science papers, and comparison of architectural options.

### Domain Model & Architecture Docs
5. [`GLOSSARY.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/GLOSSARY.md): Canonical definitions for `Semantic Tree`, `Root`, `Trunk`, `Branch`, `Leaf`, `Cross-Link`, `Course Overlay`, `Probe`, `Lock-In Check`, and `Practice Artifact`.
6. [`docs/adr/0001-four-skill-study-architecture.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/adr/0001-four-skill-study-architecture.md): ADR recording why we kept `skills/teach` and `skills/code-tutor` untouched, moved `skills/study-tutor` to `deprecated/study-tutor`, and built the 4-skill `study*` architecture.

### New & Archived Skills
7. [`skills/study/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/study/SKILL.md): Workspace router and advisor (`/study`).
8. [`skills/study-map/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/study-map/SKILL.md): Setup and incremental mapper (`/study-map`) for `TREE.md` (1-screen `Semantic Tree`) and `COURSE.md` (`Course Overlay`).
9. [`skills/study-topic/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/study-topic/SKILL.md): Diagnostic `Probe` pre-test + 1-node-at-a-time teacher (`/study-topic`) producing zoomed-in sub-trees and notes in `notes/<slug>.md`, diagrams in `visuals/`, and chaining into `study-practice`.
10. [`skills/study-practice/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/study-practice/SKILL.md): Problem, flashcard, and project drill engine (`/study-practice`) with an embedded, zero-dependency `practice/server.mjs` template created fresh once inside the active study folder to auto-save all HTML clicks, LaTeX answers, and pasted handwritten-work photos directly to `learning-records/results.jsonl` and `practice/submissions/`.
11. [`deprecated/study-tutor/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/deprecated/study-tutor/SKILL.md): Archived stateless `study-tutor` (`disable-model-invocation: true`).

---

## 3. Summary of Key Decisions & Takeaways Relevant to `code-tutor` / `code-coach` / `code-mentor`

If the next agent session evaluates or redesigns **`code-tutor`**, **`code-coach`**, or a new **`code-mentor`** workflow, these principles established during our session apply directly:

1. **Portability Invariant (Pure Markdown Skills Only)**:
   - `dersu-agent-skills` is used to sync skills across devices and accounts.
   - Skills in `skills/` must remain **100% self-contained Markdown (`SKILL.md`)** and never depend on external helper scripts inside the `dersu-agent-skills` repository path. If a skill needs a local runtime helper (like `practice/server.mjs`), the template belongs inside `SKILL.md` so the agent generates it fresh inside the user's active working folder.
2. **Why `study-tutor` Was Deprecated (And What That Means for `code-tutor`)**:
   - Look at `deprecated/study-tutor/SKILL.md` vs. `skills/code-tutor/SKILL.md`: both were written with the exact same 32-line stateless template (*"1. Explain like the learner is new... 4. Ask the learner to explain back..."*).
   - In `study-tutor`, that template failed because:
     - It had **no diagnostic `Probe`** (always assumed the user knew nothing).
     - Its always-loaded `description` collided with other skills and spent context load on every turn.
     - Asking the user to type out long explanations in chat after every paragraph triggered the **Asymmetric Correction Trap** when the user was tired.
     - It had **no workspace state** (`TREE.md`, `learning-records/`) across sessions.
   - We deliberately left `skills/code-tutor/SKILL.md` and `skills/code-coach/SKILL.md` untouched in this session so you can examine how `code-tutor`, `code-coach`, and any new `code-mentor` workflow should be structured using your separate coding notes.
3. **`/writing-for-agents` Levers Validated During Code Review**:
   - **Split by Sequence**: Separating Setup/Mapping from Teaching and Practice prevents **Premature Completion** (where visible later steps pull the agent to rush initial diagnosis/setup).
   - **Agent-Callable Handoffs**: Keeping sequential skills model-invoked allows Skill A to invoke Skill B via the `skill` tool automatically at phase boundaries, while keeping top-level YAML `description` pointers short (~20 words each) to minimize always-loaded context token cost.
   - **Auto-Captured Results Over Copy-Pasting**: Whenever an agent generates interactive browser artifacts (quizzes, flashcards, visual labs), results must write back to disk automatically (e.g., via a local loopback server writing to `.jsonl`) rather than requiring manual copy-pasting.
