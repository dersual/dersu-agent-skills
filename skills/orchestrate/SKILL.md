---
name: orchestrate
description: "Opt-in top-level workflow router. Analyzes the task and maps it to the appropriate engineering playbook: Feature, Bugfix, Refactor, or Research/Investigation."
disable-model-invocation: true
---

# Orchestrate

An opt-in top-level workflow router. Analyzes the user's intent and executes the corresponding sequence of skills.

Individual skills remain directly callable at any time (`/grill-me`, `/to-spec`, `/spec-audit`, `/to-tickets`, `/implement`, `/diagnosing-bugs`, `/code-review`, `/arena`). Use `/orchestrate` when you want the harness to guide an end-to-end task through its canonical playbook.

## Playbook Routing Matrix

| Task Type | Trigger Signals | Canonical Playbook Sequence |
| :--- | :--- | :--- |
| **Feature** | New capability, user story, API endpoint, UI view | `/grill-me` → `/to-spec` → `/spec-audit` → `/to-tickets` → `/implement` → `/code-review` → `/retro` |
| **Bugfix** | Broken behavior, throwing error, crash, regression | `/diagnosing-bugs` (tight red loop, root cause trace, regression test) → `/code-review` |
| **Refactor** | Architecture cleanup, decoupling, dead code, technical debt | `/improve-codebase-architecture` → `/codebase-design` → Characterization Tests → `/to-tickets` (Expand-Contract) → `/implement` → `/code-review` |
| **Research / Spike** | Unknown API, architectural uncertainty, exploratory evaluation | `/research` (docs & primary sources) OR `/prototype` (throwaway UI/logic spike) OR `/arena` (parallel tournament) |

---

## Playbook Workflows

### 1. Feature Playbook
1. **Clarify Decisions:** Run `/grill-me` to resolve ambiguities and lock design trade-offs.
2. **Draft Specification:** Run `/to-spec` to record user stories, interface contracts, and testing seams. Enforces the Elephant Zero-Code Invariant.
3. **Cold Audit:** Hand off immediately to `/spec-audit` for a stateless review. Must pass before tickets are created.
4. **Decompose to DAG:** Run `/to-tickets` to generate vertical tracer-bullet slices with blocking edges.
5. **Implement:** Run `/implement` on the frontier tickets using strict TDD, the Anti-Rationalization Table, and `prove-it-works` terminal verification. If architectural uncertainty is high, invoke `--arena`.
6. **Review & Retrospect:** Run `/code-review` (2-axis standards and spec review with proof-or-dismiss) followed by `/retro`.

### 2. Bugfix Playbook
1. **Construct Feedback Loop:** Call `/diagnosing-bugs` Phase 1. Build a tight, deterministic red-capable test or CLI script that runs in seconds.
2. **Trace Root Cause:** Reproduce and minimise. Never wrap symptoms in defensive guards (`?.`, try/catch defaults); locate where the invariant was first violated.
3. **Regression Test & Fix:** Write a regression test at the correct seam, apply the fix, and capture unedited terminal proof (`prove-it-works`).
4. **Review:** Call `/code-review` to verify the fix and prevent collateral regressions.

### 3. Refactor Playbook
1. **Map Architectural Hotspots:** Call `/improve-codebase-architecture` to visualize churn, dependencies, and complex modules.
2. **Design Deep Interfaces:** Call `/codebase-design` to design deep module boundaries and establish clean seams.
3. **Lock Boundary Invariants:** Write characterization tests at the outer seam before touching implementation code to ensure existing behavior is preserved.
4. **Sequence Expand-Contract:** Call `/to-tickets` using the Expand-Contract pattern:
   - *Expand:* Introduce new interfaces alongside old ones.
   - *Migrate:* Transition callers in batches.
   - *Contract:* Delete legacy code once all callers have migrated.
5. **Implement & Review:** Call `/implement` followed by `/code-review`.

### 4. Research & Investigation Playbook
- **Documentation & Investigation:** Call `/research` to gather primary sources and produce markdown findings.
- **Throwaway Spikes:** Call `/prototype` to build a throwaway sandbox answering specific UI or state questions.
- **Parallel Tournament (`arena`):** Call `/arena` when two competing implementations need to be built in parallel Git worktrees, benchmarked, and synthesized.
