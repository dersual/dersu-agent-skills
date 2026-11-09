# Research Report: AI Agent Engineering Skill Ecosystems — Comparative Analysis, Retrospective, & Definitive Workflow Architecture

**Date:** 2026-11-09  
**Status:** Definitive Source of Truth  
**Scope:** Architectural evaluation of four major AI agent engineering skill ecosystems (`mattpocock/skills`, `addyosmani/agent-skills`, Lauren Tan's `pstack`, and Google's `google/elephant-goldfish-model`), empirical autopsy of past user session failures (`or83devtools`, `my-agy-statusline`, and `School Code`), first-principles analysis of adversarial review token economics, and an un-compromised, fork-and-harden implementation plan for `dersu-agent-skills`.  
**Author:** Antigravity AI Systems Research & Software Architecture Pair  

---

## Executive Summary: The Single Source of Truth

This report establishes the **single definitive source of truth** for your AI engineering harness in `dersu-agent-skills`. It resolves all previous contradictions, grounds decisions in first-principles software engineering, and provides a clear blueprint for what skills to bring into this repository, what to modify, what to keep, and what to drop.

### The Core Decision: Fork and Harden into `dersu-agent-skills`

You should **not** rely on upstream external skill packages as unmodifiable black boxes. 
- External packages (installed via `npx skills add mattpocock/skills`) are read-only. Every update overwrites them. You cannot patch their flaws, embed anti-rationalization tables, or enforce proof-of-work invariants.
- **The Solution:** Bring the **Core Engineering Loop** from Matt Pocock directly into `dersu-agent-skills/skills/`. Own them in version control. Harden them with Addy Osmani's **Anti-Rationalization Tables**, Lauren Tan's **`prove-it-works`** execution proofs, and Google EGM's **Zero-Code Spec** invariant.
- Your personal and teaching skills (`code-tutor`, `study-tutor`, `humanizer`, `caveman`, `orwell-writing`, etc.) remain in `skills/` untouched.

```
                    DEFINITIVE HARNESS ARCHITECTURE
                    
┌─────────────────────────────────┐     ┌─────────────────────────────────┐
│     MATT POCOCK (Foundations)   │     │      ADDY OSMANI (Discipline)   │
│  • Core Loop: grill-me, to-spec,│     │  • Anti-Rationalization Tables  │
│    to-tickets, diagnosing-bugs  │     │  • Direct rebuttals for shortcuts│
│  • Deep Modules & Seams         │     │  • Seam-level testing invariants│
│  • Tracer-Bullet Task DAGs      │     │  • Five-Axis Quality Review     │
└────────────────┬────────────────┘     └────────────────┬────────────────┘
                 │                                       │
                 ▼                                       ▼
    ┌─────────────────────────────────────────────────────────┐
    │     HARDENED LOCAL SKILLS REPO (dersu-agent-skills)     │
    │                                                         │
    │  1. CLARIFY: /grill-me (Frontier Decision Tree)         │
    │  2. SPEC: /to-spec (The Elephant: Writes ZERO Code)     │
    │  3. AUDIT: /audit-spec (The Goldfish: Single-Pass Cold) │
    │  4. SLICE: /to-tickets (Vertical Tracer-Bullet DAG)     │
    │  5. BUILD: /implement (Anti-Rationalization + Proof)    │
    │  6. DEBUG: /diagnosing-bugs (Red-Capable Feedback Loop) │
    │  7. REVIEW: /code-review (2-Axis + Interrogation Rule)  │
    │  8. HARDEN: /retro (Turns repeated flaws into linters)  │
    └────────────────┬────────────────────────────────────────┘
                 ▲                                       ▲
                 │                                       │
┌────────────────┴────────────────┐     ┌────────────────┴────────────────┐
│      LAUREN TAN (Verification)  │     │      GOOGLE EGM (Epistemics)    │
│  • prove-it-works: Real CLI     │     │  • The Elephant: Long chat      │
│    terminal execution artifacts │     │    writes spec, writes ZERO code│
│  • Interrogation Invariant:     │     │  • The Goldfish: Fresh subagent │
│    Criticisms dismissed without │     │    audits spec cold with no     │
│    concrete failure proof       │     │    conversational bias          │
└─────────────────────────────────┘     └─────────────────────────────────┘
```

---

## Part 1: First-Principles Answers to Core Questions

### 1. Adversarial Review vs. Anti-Rationalization Tables: What is the Difference?

These two mechanisms are often confused, but they operate at completely different layers of the harness:

| Dimension | Anti-Rationalization Table (Addy Osmani) | Adversarial Review (Google EGM / Lauren Tan) |
| :--- | :--- | :--- |
| **What is it?** | A static table of **forbidden excuses and mandatory rebuttals** written directly into the skill prompt or coding standards. | A **dynamic second-pass audit** where an independent agent or subagent inspects the work. |
| **When does it run?** | **During authoring.** While the agent is actively writing code or tests. | **After authoring.** Before a spec is sliced, or after code is written. |
| **How does it work?** | When the agent is tempted to take a shortcut (*"I'll mock Electron IPC because running tests takes too long"*), the table explicitly blocks the excuse: <br>• **REJECTED:** *Mocks that do not reflect runtime reality cause production outages. Test against the real seam.* | A reviewer inspects the artifact cold, looking for edge-case gaps, broken contracts, or missing error handling. |
| **Token / Compute Cost** | **Zero extra subagents. Zero extra API calls.** It is pure prompt text read by the primary authoring model. | **1 extra subagent.** Costs an additional model call. |
| **Where does it live?** | In `skills/implement/SKILL.md` and `skills/setup-standards/templates/CODING_STANDARDS.md`. | In `skills/audit-spec/SKILL.md` (spec review) and `skills/code-review/SKILL.md` (code review). |

#### Does `code-review` already do adversarial review?
**Yes, but at the wrong time for architecture.**
- Matt Pocock's `code-review` runs **after code is written**. It spawns two subagents: Standards (refactoring smells) and Spec (fidelity to acceptance criteria).
- Google Elephant-Goldfish Model (EGM) runs **before code is written**. It audits the *specification document* before tickets are created.
- **Why this timing matters:** Catching an architectural flaw in a spec document costs ~1,500 tokens of Markdown editing. Catching that same flaw after code is written, tests are scaffolded, and files are split costs 50,000–150,000 tokens of refactoring.

---

### 2. Adversarial Review Token Economics: The Twitter Critique vs. Bounded Reality

You raised a valid challenge: *Twitter discussions argue that adversarial review wastes tokens. Is there an actual rebuttal?*

#### Why Twitter is 100% Right About Naive Multi-Agent Loops
Unconstrained multi-agent review loops are **token incinerators**:
1. **The Circular Ping-Pong Trap:** Agent A writes code $\to$ Agent B critiques style $\to$ Agent A rewrites to satisfy Agent B $\to$ Agent B finds new stylistic nitpicks $\to$ 80,000 tokens burned on bikeshedding with zero functional improvement.
2. **Pedantic Hallucinations:** When models are prompted to "be critical," they invent hypothetical risks (e.g., *"What if this timestamp fails in the year 2099?"* or *"Consider using the Abstract Factory pattern"*).
3. **Absurd Overhead on Simple Code:** Spawning critic agents on a 20-line CSS change or a basic helper function costs far more in tokens than any minor defect it could catch.

#### The First-Principles Antidotes to Token Waste
To make adversarial review high-ROI, your harness must enforce **three strict invariants**:

1. **Single-Pass Audit (No Debate Loops):**  
   The auditor subagent runs **once**. It outputs a concise Markdown findings table and immediately terminates. It never enters a multi-turn chat debate with the author agent.
2. **Lauren Tan's Interrogation Rule (Burden of Proof):**  
   Any critique from a reviewer is **automatically dismissed and deleted** unless it is supported by a **reproducible execution proof** (a failing test case, a concrete counter-example, or an unhandled edge-case trace). Subjective opinions and stylistic advice are banned.
3. **Threshold Gate (Specs Only):**  
   Adversarial audit is triggered **only** for new architectural specifications, security boundaries, or concurrency primitives. It is **strictly banned** for bug fixes, CSS, and routine CRUD tasks.

---

### 3. The Speccing Pipeline: `/grill-me`, `/to-spec`, `/to-tickets`, and `/audit-spec`

You asked: *We have /spec or /grill-me, but which one are we using? Is that part of to-tickets? Where does the Goldfish fit?*

Here is the exact, un-contradicted sequence of how these skills fit together:

```
                      THE COMPLETE SPECIFICATION PIPELINE
                      
  ┌────────────────────────────────────────────────────────────────────────┐
  │ Step 1: CLARIFY INTENT & DECISIONS                                     │
  │ Command: /grill-me                                                     │
  │ • Explores user intent as a decision tree.                             │
  │ • Asks the frontier of unsettled architectural choices in batches.     │
  │ • Invariant: Finding facts is the agent's job; making decisions is yours│
  └───────────────────────────────────┬────────────────────────────────────┘
                                      │ Decisions settled
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ Step 2: DRAFT THE SPECIFICATION DOCUMENT                               │
  │ Command: /to-spec                                                      │
  │ • Synthesizes decisions into docs/specs/<feature>.md.                  │
  │ • Defines problem statement, user stories, seams, and boundaries.      │
  │ • The Elephant Invariant: STRICTLY ZERO PRODUCTION CODE WRITTEN.       │
  └───────────────────────────────────┬────────────────────────────────────┘
                                      │ Spec written to disk
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ Step 3: AUDIT THE SPECIFICATION (The Goldfish Audit)                   │
  │ Command: /audit-spec (Used on non-trivial architectural features)      │
  │ • Spawns a fresh, stateless subagent with ZERO conversation history.   │
  │ • Reads docs/specs/<feature>.md cold, like a complete stranger.        │
  │ • Flags unstated assumptions, missing edge cases, or broken contracts. │
  │ • Single-pass output; Lauren Tan proof-or-dismiss rule enforced.       │
  └───────────────────────────────────┬────────────────────────────────────┘
                                      │ Spec approved by user
                                      ▼
  ┌────────────────────────────────────────────────────────────────────────┐
  │ Step 4: DECOMPOSE INTO TASK GRAPHS                                     │
  │ Command: /to-tickets                                                   │
  │ • Deconstructs the approved spec into vertical tracer-bullet slices.   │
  │ • Every ticket cuts through schema, API, UI, and test.                 │
  │ • Declares explicit blocking DAG edges.                                │
  └────────────────────────────────────────────────────────────────────────┘
```

You do **not** choose between `/spec` and `/grill-me`. You use `/grill-me` to interview and decide, `/to-spec` to author the specification document, `/audit-spec` (Goldfish) to verify the document cold, and `/to-tickets` to slice the work.

---

### 4. Pstack's `/arena` and `/swarm`: Why Drop Them from Daily Defaults?

You asked: *Pstack's arena ideas were interesting, but why drop them? What is the justification?*

#### What is `/arena` in `pstack`?
In `pstack`, `/arena` spawns 3 to 4 subagents in parallel Git worktrees. Each subagent writes an independent implementation of the same ticket. A judge agent runs tests against all of them, selects the winning baseline, and grafts strong components from the losers into the final branch.

#### Why `/arena` is Dropped from Daily Defaults
1. **The Model & Quota Reality:**  
   You explicitly stated: *"i only want to use free models... and antigravity pro (however im a free trial, so no argon).... We're only using their Gemini 1.5 Flash High... it's not a planning model."*  
   Running `/arena` on a single feature multiplies token consumption by **3x to 4x** and consumes 4 concurrent tool sessions. On free tiers, trial quotas, or rate-limited environments, running `/arena` on routine tickets will quickly trigger rate limits and exhaust hourly quotas.
2. **Negative ROI on Routine Engineering:**  
   For 95% of engineering tasks (adding an Electron IPC channel, writing a CLI parser, creating a React component), there are not three fundamentally different implementations. Forcing multiple agents to write the same 20 lines of code wastes tokens with zero architectural gain.
3. **When Arena IS Justified (As an On-Demand Tool):**  
   Arena is reserved exclusively for high-stakes, uncertain spikes (e.g., *"We cannot decide whether to use RxJS or an EventBus for cross-window state, build both as throwaway spikes and measure latency"*). It is kept as an on-demand specialized skill, but banned from the default daily loop.

---

### 5. Why Routing Must Be an Optional Convenience, Not a Mandatory Gatekeeper

You asked: *What does poteto-mode do? How does it route? Can an LLM router truly be trustworthy?*

#### How `/poteto-mode` Operates in `pstack`
In Lauren Tan's system, `/poteto-mode` is **not a mandatory wrapper that intercepts every user prompt**.
- It is an **explicit slash command** (`/poteto-mode <goal>`).
- It parses the user's high-level goal and pattern-matches it against **23 static Markdown playbooks** (`bugfix.md`, `feature.md`, `investigation.md`, `refactor.md`, etc.).
- It does not consider skills outside of `pstack` (it knows nothing of Matt Pocock's `grill-me`, nor your teaching skills).

#### The Model Reality of LLM Routers
1. **Latency Tax (TTFT):** If every turn must pass through an autonomous classifier agent, you add 3 to 10 seconds of latency to every interaction.
2. **Classification Fragility on Flash Models:** Small, high-speed models (`gemini-1.5-flash`) frequently misclassify nuanced requests (e.g., confusing an architectural concurrency defect with a routine feature request).
3. **Developer Friction:** When an engineer explicitly types `/diagnosing-bugs` or `/to-spec`, they want that exact workflow executed immediately. Forcing them through an LLM router that second-guesses their command is counterproductive.

> [!IMPORTANT]
> **Definitive Rule:**  
> Routing must be an **OPTIONAL convenience command** (`/orchestrate <task>`), never a mandatory gatekeeper. All individual skills (`/grill-me`, `/to-spec`, `/to-tickets`, `/diagnosing-bugs`, `/implement`, `/code-review`) remain directly callable first-class commands.

---

## Part 2: Wait-What Explanation: Google Elephant-Goldfish (Dave Rensin)

> [!NOTE]
> *Written in strict ASD-STE100 Simplified Technical English.*

### What is the problem?
You talk with an AI agent for a long time. You discuss features, edge cases, and ideas.  
The chat gets very long.  
This long chat causes two problems:
1. **The AI forgets**: The context window fills with text. The AI loses reasoning precision.
2. **The AI agrees too much (Confirmation Bias)**: The AI wants to please you. If your idea has a flaw, the AI ignores the flaw because you discussed it earlier.

If this same AI writes code now, it makes mistakes based on assumptions that are not written down.

### How does the Elephant-Goldfish model fix this?
The model separates memory into two roles:

1. **The Elephant (Big Memory)**:
   - Your main chat agent is the Elephant.
   - It remembers your full conversation.
   - It reads your project history and guides.
   - It writes the **design document** (`spec.md`).
   - **Important rule:** The Elephant writes **zero code**. It writes only the specification.

2. **The Goldfish (No Memory)**:
   - The Goldfish is a new subagent.
   - It has **zero memory** of your past conversation.
   - It reads **only** the design document (`spec.md`) and existing code files.
   - It reads like a complete stranger.
   - If the design document misses an edge case, the Goldfish sees it immediately because it cannot read your past chat.

### Why does this help you?
You catch design bugs **before** you write code.  
You do not waste tokens arguing in circles.  
The Goldfish checks the spec once. You fix the spec. Then you build the code with confidence.

---

## Part 3: Session Autopsy: Real Evidence from `or83devtools` & `my-agy-statusline`

Why were tests in past sessions weak? We inspected the actual session transcripts and codebases to identify the exact mechanisms.

### Case 1: `or83devtools` (Single-City IO Breakdown)
* **Workspace:** `C:\Users\dersu\Code Stuff\or83-suite\or83devtools`  
* **Session ID:** `00a15d3d-80f6-4563-ab19-07cfbe37ebb6`  
* **The Failure Mechanism:**  
  Looking directly at [test/city/city.ipc.test.js](file:///C:/Users/dersu/Code%20Stuff/or83-suite/or83devtools/test/city/city.ipc.test.js#L21-L49):

```javascript
// Test from or83devtools/test/city/city.ipc.test.js
it("successfully delegates loadJsonFile and saveJsonFile to injected ipcRenderer", async () => {
  const mockIpc = {
    invoke: async (channel, payload) => {
      if (payload.action === "get_json") {
        return { data: [{ id: "test_city" }] }; // HARDCODED MOCK
      }
      if (payload.action === "save_file") {
        return { status: "SUCCESS" };           // HARDCODED MOCK
      }
      return null;
    },
  };
  CityIpc.setIpcRenderer(mockIpc);
  const data = await CityIpc.loadJsonFile("test.json");
  assert.deepEqual(data, [{ id: "test_city" }]);
});
```

* **The Flaw:**  
  The test mocked out `ipcRenderer` completely. It verified that calling `CityIpc.loadJsonFile` returned the exact hardcoded array that `mockIpc` was programmed to return.
  - It **never** tested Electron IPC serialization across process boundaries.
  - It **never** tested whether `#btn-export-city` in `city.html` successfully triggered the controller.
  - The suite was 100% green while the feature broke in production.
* **Why Pocock's skills allowed this:** Pocock's `tdd` skill commanded the agent to "write tests", but provided no guard against tautological mocking. Under context pressure, the agent took the path of least resistance.

### Case 2: `my-agy-statusline` (Execution Without Assertion)
* **Workspace:** `C:\Users\dersu\Code Stuff\my-agy-statusline`  
* **Session ID:** `9a826493-2775-430c-ab23-11239c096c4b`  
* **The Failure Mechanism:**  
  Looking directly at [tests/test_ps1.ps1](file:///C:/Users/dersu/Code%20Stuff/my-agy-statusline/tests/test_ps1.ps1#L42):

```powershell
# From my-agy-statusline/tests/test_ps1.ps1
Get-Content $fixturePath -Raw | powershell -NoProfile -File $scriptPath
```

* **The Flaw:**  
  The test simply verified that piping JSON into `statusline.ps1` did not crash with an unhandled exception. It contained **zero assertions** on the output string:
  - Did the ANSI escape sequences format correctly without breaking terminal column width?
  - Did narrow mode properly truncate tool names?
  - The test suite printed `[SUCCESS]` while visual regressions occurred in live PowerShell prompts.

### How Addy Osmani & Lauren Tan Directly Eliminate These Failures

```
┌──────────────────────────────────────┬──────────────────────────────────────────────────┐
│ Past Session Failure Mode            │ Antidote / Rule Enforcement                      │
├──────────────────────────────────────┼──────────────────────────────────────────────────┤
│ Tautological Mocking in or83devtools │ Addy Osmani's Anti-Rationalization Invariant:    │
│ (Mocking IPC to return hardcoded     │ "REJECTED: Mocking the seam because running real │
│ data, never touching real electron   │ IPC is difficult. Tests must verify against the  │
│ process boundaries)                  │ observable runtime boundary."                    │
├──────────────────────────────────────┼──────────────────────────────────────────────────┤
│ Unasserted Execution in statusline   │ Lauren Tan's prove-it-works Invariant:           │
│ (Running script to see if it throws, │ "Execution proof requires capturing verifiable   │
│ without asserting terminal output)   │ machine artifacts of actual visual rendering,    │
│                                      │ ANSI codes, and edge-case contracts."            │
└──────────────────────────────────────┴──────────────────────────────────────────────────┘
```

---

## Part 4: Anti-Slop Redundancy: The Case for Pruning

You noted: *"Wasn't unslop and deslop already integrated into my code standards here? Do I need another skill?"*

Let's compare the components:
1. **[CODING_STANDARDS.md](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/setup-standards/templates/CODING_STANDARDS.md#L22-L29) (Section 3: Anti-Slop):**  
   Already establishes rules for code and comments: *Explain Why, Not What; Preserve Navigation Banners; Fail Fast; Match Local Idioms.* Enforced automatically during `/code-review`.
2. **[skills/humanizer/SKILL.md](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/humanizer/SKILL.md):**  
   A dedicated 35 KB engine designed to de-slop prose, documentation, and resumes based on Wikipedia's *Signs of AI writing*.
3. **Lauren Tan's `unslop`:**  
   A brief 40-line cursor prompt instructing the agent to strip corporate jargon.

### The Verdict: Do NOT Add a Separate `unslop` Skill
Adding a third standalone `unslop` skill is 100% redundant. Keep anti-slop rules in `CODING_STANDARDS.md` for code, and use `humanizer` for prose and documentation.

---

## Part 5: In-Progress Skills: Software Factory & Chief of Staff

- **Fact Check:** In Matt Pocock's upstream repository, `chief-of-staff` and `software-factory` are located under `skills/in-progress/`.
- They are **experimental prototypes**, not hardened production tools.
- **The Verdict:** Keep them out of your active daily pipeline. Treat them as conceptual research, not operational dependencies.

---

## Part 6: The Definitive Plan: What to Copy, Modify, Keep, and Drop

This section is the single source of truth for structuring `dersu-agent-skills`.

### 1. What Stays Untouched in `dersu-agent-skills/skills/`
Do **not** delete your personal, teaching, and writing skills:
- `code-tutor` & `study-tutor` (Interactive step-by-step tutoring)
- `scaffold-exercises` (Curriculum generator)
- `humanizer` (Wikipedia-based prose de-slopper)
- `orwell-writing` (ASD-STE100 technical writing guide)
- `caveman` (Token-saving compression)
- `find-skills` & `setup-permissions` (Environment management)
- `refine-resume-bank` & `tailor-resume` (Career tools)
- `show-me`, `zoom-out`, `code-coach`, `toggle-code-coach` (Exploration & posture controls)
- `wait-what` (ASD-STE100 re-pitching tool)

### 2. What Core Skills are Forked & Hardened into `dersu-agent-skills/skills/`
Bring the core engineering skills from Matt Pocock directly into `dersu-agent-skills/skills/`, and modify them with Addy Osmani's and Lauren Tan's invariants:

```
C:\Users\dersu\Code Stuff\dersu-agent-skills\skills\
├── grill-me/                      # Pocock's frontier decision tree interview
│   └── SKILL.md
├── to-spec/                       # Pocock's seam spec + GOOGLE EGM ZERO-CODE RULE
│   └── SKILL.md
├── audit-spec/                    # NEW: Google EGM Goldfish stateless cold audit
│   └── SKILL.md
├── to-tickets/                    # Pocock's tracer-bullet vertical slice DAG decomposition
│   └── SKILL.md
├── implement/                     # Pocock's implement + ADDY ANTI-RATIONALIZATION + TAN PROVE-IT-WORKS
│   └── SKILL.md
├── diagnosing-bugs/               # Pocock's red-capable feedback loop debugger
│   └── SKILL.md
├── code-review/                   # Pocock's 2-axis review + LAUREN TAN PROOF-OR-DISMISS RULE
│   └── SKILL.md
├── retro/                         # Pocock's session retrospective & linter hardening
│   └── SKILL.md
├── orchestrate/                   # NEW: Opt-in high-level router (Lauren Tan pattern)
│   └── SKILL.md
├── codebase-design/               # Pocock's deep module & seam vocabulary
│   └── SKILL.md
├── domain-modeling/               # Pocock's glossary & ubiquitous language builder
│   └── SKILL.md
└── resolving-merge-conflicts/     # Pocock's git conflict resolution assistant
    └── SKILL.md
```

### 3. Exact Modifications Applied to Each Core Skill

#### A. `to-spec/SKILL.md` (Modified with Google EGM)
- **Modification:** Add the Elephant Invariant:
  > **The Invariant Rule of the Specification Author:** You are strictly forbidden from writing production code, creating implementation files, or patching logic. Your sole deliverable is the design document at `docs/specs/<feature>.md`.

#### B. `audit-spec/SKILL.md` (New Skill: The Goldfish)
- **Specification:**
  ```markdown
  ---
  name: audit-spec
  description: Stateless, zero-context adversarial review of technical specifications. Spawns an amnesiac subagent to audit docs/specs/<feature>.md before tickets are created.
  disable-model-invocation: true
  ---
  
  # Stateless Specification Audit (The Goldfish)
  
  You are an adversarial software auditor. You have ZERO context of prior conversations.
  Read ONLY the target specification document and referenced source code.
  
  ## Audit Dimensions
  1. **Completeness**: What edge cases are unstated? What failure paths are omitted?
  2. **Seam Safety**: Are boundary interfaces minimal and deep?
  3. **Testability**: Can this be verified at an external seam without mocking internal state?
  
  ## Lauren Tan Interrogation Rule
  Every critique MUST cite:
  - The exact section and line in the spec.
  - The concrete failure scenario or counter-example.
  Any critique lacking an executable failure path is dismissed.
  ```

#### C. `implement/SKILL.md` (Modified with Addy Osmani & Lauren Tan)
- **Modification:** Embed the Anti-Rationalization Table and `prove-it-works` mandate:
  ```markdown
  ## Mandatory Anti-Rationalization Invariants
  - **No Mocking the Seam**: If a test fails, fix the underlying defect or environment harness. Never replace a real integration seam (Electron IPC, Git subprocesses, DOM events) with a trivial mock to force a green test.
  - **No Deferred Verification**: You cannot mark a task complete by stating "tests will be added later." The test must exist, run, and pass in this turn.
  - **Prove It Works**: You must print the actual CLI command and its unedited machine terminal output proving the fix works. Self-attestation is rejected.
  ```

#### D. `code-review/SKILL.md` (Modified with Lauren Tan Interrogation Invariant)
- **Modification:** Add the Burden-of-Proof rule to the Reviewer subagents:
  > **Reviewer Invariant:** Review findings are strictly dismissed unless supported by a reproducible failure proof (a failing test case or verifiable contract violation). Stylistic nitpicks and speculative suggestions are prohibited.

#### E. `setup-standards/templates/CODING_STANDARDS.md`
- **Modification:** Add Section 5: *Verification Invariants (Anti-Rationalization)* directly into the repository standards template to ensure that all future projects inherit these protections.

---

## Primary Source Citations & References

1. **Dave Rensin**, *"Elephants, Goldfish and the New Golden Age of Software Engineering"*, Google Open Source & Research Publications, 2025/2026. [https://github.com/google/elephant-goldfish-model](https://github.com/google/elephant-goldfish-model)
2. **Matt Pocock**, *Skills for Real Engineers: Spec-Driven Development, Deep Modules, and Task Graphs*, 2025/2026. [https://github.com/mattpocock/skills](https://github.com/mattpocock/skills)
3. **Addy Osmani**, *Agent Skills: Production-Grade Software Engineering Lifecycles for AI Coding Agents*, 2025/2026. [https://github.com/addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)
4. **Lauren Tan (`@poteto`)**, *pstack: Cursor Engineering Playbooks, Parallel Arenas, and Proof-Backed Verification*, Cursor Plugin Directory, 2025/2026. [https://github.com/cursor/plugins/tree/main/plugins/pstack](https://github.com/cursor/plugins/tree/main/plugins/pstack)
5. **Dersu Research Vault**, *Global Steering Files (`AGENTS.md`) & Rule Friction Retrospective*, [agents-rule-friction-retro.md](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/agents-rule-friction-retro.md), 2026.
6. **Empirical Session Logs**, `00a15d3d-80f6-4563-ab19-07cfbe37ebb6` (`or83devtools`), `9a826493-2775-430c-ab23-11239c096c4b` (`my-agy-statusline`), and `0a4730e5-9110-4bcd-86a6-f882d52b567b` (`School Code`).
