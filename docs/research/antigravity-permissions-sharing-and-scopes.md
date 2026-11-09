# Research Report: Antigravity Permissions Sharing, Storage Topology, and Scope Architecture

**Date:** 2026-11-07  
**Topic:** Verification of permission sharing across Antigravity products (Desktop App, CLI, IDE), CLI `/permissions` TUI 3-scope architecture, GitHub Issue #559, and runtime overrides.  
**Repository:** `dersu-agent-skills`  
**Author:** Antigravity Agent  

---

## Executive Summary

This report synthesizes four primary sources:
1. Official Antigravity Documentation (`https://antigravity.google/docs/permissions/#updated-permission-settings`)
2. Antigravity CLI TUI (`/permissions`) Scope Selection Interface
3. GitHub Issue #559 (`google-antigravity/antigravity-cli`: *Persist project permissions together with the code*)
4. AI Google Dev Community Discussion (`https://discuss.ai.google.dev/t/are-antigravity-app-and-cli-permissions-actually-shared/198588/3`)
5. Local disk inspection across `~/.gemini/config/config.json`, `~/.gemini/antigravity-cli/settings.json`, and `~/.gemini/config/projects/`.

### Core Discoveries
1. **The CLI TUI exposes three explicit scopes:**
   - **`Project`**: Scoped to the active project workspace.
   - **`Shared with Antigravity`**: Rules that apply to all Antigravity products (App, CLI, IDE).
   - **`Global`**: Rules that apply globally to the CLI only.
2. **Where they write on disk:**
   - `Shared with Antigravity` writes to: `~/.gemini/config/config.json` (`userSettings.globalPermissionGrants`).
   - `Global` (CLI-only) writes to: `~/.gemini/antigravity-cli/settings.json` (`permissions`).
   - `Project` writes to: `~/.gemini/config/projects/<project-id>.json` (`permissionGrants.permissionGrants`).
3. **Why manual editing initially failed:**
   In earlier sessions, rules were placed exclusively into `~/.gemini/antigravity-cli/settings.json`. That is the CLI-Only Global file. The Desktop App reads `config.json` (`Shared with Antigravity`). Because the user recently entered the rules into `Shared with Antigravity` via the TUI, `config.json` is now fully populated and synchronized.
4. **Project permissions and GitHub Issue #559:**
   Currently, Antigravity does not store project permissions inside the git repository. They are stored locally in `~/.gemini/config/projects/<project-id>.json`. GitHub Issue #559 is the active community request to allow in-repo persistence (e.g. `.agents/permissions.json`).
5. **Behavior of `--dangerously-skip-permissions`:**
   This flag automatically confirms operations that would otherwise prompt (`ask`). It **never** executes commands or actions marked with `deny`. `Deny` rules remain an unconditional block under all circumstances.

---

## Part 1: The 3-Tier Scope Architecture in the CLI TUI

When you open `/permissions` in the CLI, the TUI displays three distinct configuration scopes:

```
Permission Config Editor
Select a config scope to edit:
  Project
> Shared with Antigravity
  Global
```

### 1. Scope: `Shared with Antigravity`
- **Description:** *"Rules that apply to all Antigravity products"*
- **Filesystem Location:** `~/.gemini/config/config.json`
- **JSON Key:** `userSettings.globalPermissionGrants`
- **Target Surfaces:** Antigravity Desktop App, Antigravity IDE, and Antigravity CLI.
- **Enforcement:** Machine-wide baseline safety. Rules here are respected universally across all projects and interfaces.

### 2. Scope: `Global` (CLI-Only)
- **Description:** Global rules applying strictly to standalone CLI sessions.
- **Filesystem Location:** `~/.gemini/antigravity-cli/settings.json`
- **JSON Key:** `permissions`
- **Target Surfaces:** Standalone CLI (`agy`).
- **Enforcement:** Evaluated during terminal CLI workflows. Does not sync back to the Desktop App unless manually mirrored or configured via `Shared with Antigravity`.

### 3. Scope: `Project`
- **Description:** Rules applying only when working inside a specific project/repository.
- **Filesystem Location:** `~/.gemini/config/projects/<project-id>.json`
- **JSON Key:** `permissionGrants.permissionGrants`
- **Discovery Mechanism:** Antigravity matches the current workspace folder path against `projectResources.resources[].folderUri`.
- **Enforcement:** Applies only while operating in that project workspace. Overrides global allow/ask presets for repository-specific runtimes (`npm test`, `pytest`, `cargo build`).

---

## Part 2: Analysis of GitHub Issue #559 & Community Discussion

### GitHub Issue #559: "Persist project permissions together with the code"
- **The Core Problem:** Antigravity stores project-scoped permissions on the local developer workstation (`~/.gemini/config/projects/<project-id>.json`) rather than within the codebase.
- **Consequences Identified by the Community:**
  1. Team members cloning the same repository must re-configure permissions individually.
  2. Developers moving between multiple workstations lose project-level permissions.
  3. CI/CD pipelines cannot ingest repository permission boundaries automatically.
- **Current Workaround:** Maintain an in-repo file (e.g., `.agents/permissions.json`) and use an agent or script to map those rules into Antigravity's local configuration store.

### Forum Discussion (`discuss.ai.google.dev`)
The discussion confirms that editing `~/.gemini/antigravity-cli/settings.json` directly affects only the CLI. To achieve cross-product sharing across the App and CLI, rules must be placed into `~/.gemini/config/config.json` (the store used by `Shared with Antigravity`).

---

## Part 3: Verification of Local Machine Configuration

We inspected `C:\Users\dersu\.gemini` after the user updated the `Shared with Antigravity` scope:

### 1. `C:\Users\dersu\.gemini\config\config.json` (Shared Scope)
Status: **VERIFIED AND ACTIVE**
```json
"userSettings": {
  "globalPermissionGrants": {
    "allow": [
      "write_file(C:\\Users\\dersu\\.gemini\\antigravity-cli)",
      "write_file(C:\\Users\\dersu\\Code Stuff)",
      "command(git)",
      "command(git *)",
      "read_file(C:\\Users\\dersu\\Code Stuff)"
    ],
    "deny": [
      "write_file(.git)",
      "write_file(.git\\*)",
      "write_file(C:\\Users\\dersu\\.ssh)",
      "write_file(C:\\Users\\dersu\\.ssh\\*)"
    ],
    "ask": [
      "write_file(C:\\Users\\dersu\\Code Stuff\\School Code)",
      "write_file(C:\\Users\\dersu\\Code Stuff\\School Code\\*)"
    ]
  }
}
```

### 2. `C:\Users\dersu\.gemini\antigravity-cli\settings.json` (CLI Scope)
Status: **VERIFIED AND ACTIVE**
Contains an identical set of `allow`, `ask`, and `deny` rules.

**Conclusion:** Both the Desktop App and CLI are now in full alignment for global commands and paths.

---

## Part 4: Technical Analysis of `--dangerously-skip-permissions`

### 1. What does the flag do?
Running `agy --dangerously-skip-permissions` bypasses all interactive confirmation prompts. It automatically approves any operation that falls under the **`ask`** access list or default confirmation triggers (e.g. running non-allowlisted shell commands or modifying files outside sandbox boundaries).

### 2. Can it execute commands on `deny`?
**NO.**
Antigravity enforces a strict evaluation order:
$$\text{Deny} > \text{Ask} > \text{Allow}$$

- A `deny` rule is an unconditional execution abort.
- If an agent attempts to execute an action matching a `deny` rule (such as writing to `.git` or `~/.ssh`), the engine blocks the action immediately.
- `--dangerously-skip-permissions` does not bypass, disable, or ignore `deny` rules.

### 3. What operations can it not do by default?
1. **Denylisted Actions:** Anything matched by `deny` rules is blocked.
2. **Sandbox Escapes:** If sandbox mode is active, commands cannot access resources outside sandbox boundaries without explicit operating system permissions.
3. **Protected Core Metadata:** File writes targeting version control metadata (`.git`) are blocked by default to prevent corruption.
