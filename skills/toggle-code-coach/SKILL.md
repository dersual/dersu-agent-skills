---
name: toggle-code-coach
description: Toggles active code-coach mode in workspace instructions. Use when enabling, disabling, or toggling code-coach, coding mentor, or anti-atrophy mode.
---

Toggle the active state of `code-coach` mode in the workspace instructions.

## Steps

1. **Locate Instruction File**: Look for `CLAUDE.md`, `GEMINI.md`, or `AGENTS.md` (in priority order) in the workspace root. If none exist, target `AGENTS.md`.
2. **Evaluate Current State**:
   - **Active**: The file contains a pointer line referencing the `code-coach` skill.
   - **Inactive**: The file does not contain a pointer line referencing the `code-coach` skill.
3. **Execute Toggle**:
   - **To Disable** (or when currently Active): Remove the line referencing `code-coach` and clean up redundant blank lines.
   - **To Enable** (or when currently Inactive): Append the following pointer rule to the target file:
     `"When generating code, debugging, or explaining concepts, invoke and strictly follow the rules in the code-coach skill."`
4. **Confirm State**: Output a single-sentence confirmation stating the new state (Active or Inactive) and the updated configuration file path.
5. **Completion Criterion**: The target instruction file is saved and accurately reflects the desired state.
