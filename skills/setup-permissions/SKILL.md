---
name: setup-permissions
description: Interactively configures runtime permission boundaries (allow, ask, deny) for agent harnesses across workspaces, commands, and sensitive files.
---

# Setup Permissions

Guides the developer through configuring technical permission boundaries across development workspaces, commands, and sensitive paths.

## Process

Use an interactive interview approach (ask questions one at a time) to collect preferences before resolving configuration paths and writing files.

---

### 1. Inquire About Harness and Target Scope

Prompt the user to identify the target agent environment and the desired configuration scope:

1. **Harness Detection**:
   - Ask: *"Which agent harness are you configuring? (e.g., Google Antigravity, Claude Code, Cursor, Codex, Other)"*
   - If environment cues exist (such as active CLI tools, workspace directories, or system prompt identity), offer that detected harness as the recommended option.

2. **Scope Selection**:
   - Ask: *"Which scope are you configuring? (Global / Cross-Surface, Project-Specific, or Both)"*
   - **Global / Cross-Surface**: Sets machine-wide security invariants that protect the workstation across all projects.
   - **Project-Specific**: Sets tool runners, sensitive subpaths, or MCP permissions confined strictly to the active repository.

---

### 2. Present Security Baseline Defaults

Communicate the default security invariants to the user and request confirmation:

- **Deny (Unconditional Block)**:
  - `.git` and `.git/*` (prevents corruption of version control metadata)
  - `~/.ssh` and `~/.ssh/*` (prevents exposure or modification of SSH private keys)
- **Ask (Explicit Confirmation)**:
  - `*.env*` (prevents unreviewed modification of secrets and API keys)
  - Cloud sync directories (e.g., `OneDrive`, `Dropbox`)
  - Catch-all fallback (`*`) for writes outside designated developer folders

Ask: *"Do you want to accept these baseline security rules or modify any of them?"*

---

### 3. Inquire About Workspaces and Commands

Gather the user's directory topology through direct questions:

1. **Root Coding Directory (Unrestricted File Writes)**:
   - Ask: *"Which overall root directory stores your coding projects where file creation and editing should execute without confirmation prompts?"*
   - Example target: `write_file(C:\Users\<user>\Code Stuff)`

2. **Protected Subdirectories (Supervised File Writes)**:
   - Ask: *"Which specific subdirectories inside your coding workspace require confirmation before any write operation (e.g., coursework, exam prep, client work)?"*
   - Example target: `write_file(C:\Users\<user>\Code Stuff\School Code\*)`

3. **Global Command Utilities**:
   - Ask: *"Which cross-cutting command-line tools should run without confirmation prompts?"*
   - Default recommendation: `command(git)` and `command(git *)`.
   - Note: Recommend keeping project-specific runtimes (`pytest`, `npm`, `pdflatex`) out of global configurations. Keep those in project-level configurations.

---

### 4. Resolve Harness Configuration Location

Determine the exact configuration system for the chosen harness using this discovery protocol:

1. **Apply the Maximum Surface Coverage Rule**:
   - When configuring Global scope, locate the file that provides the broadest coverage across all interfaces of the harness (Desktop App, CLI, IDE extensions).
   - Do not configure a single-interface sub-tool if a shared cross-product configuration exists.
   - Consult harness documentation, CLI help (`--help`), or configuration directories to identify the shared storage layer.

2. **Locate Project Storage**:
   - For Project scope, discover the harness's project-level configuration store.
   - If the harness supports in-repo configuration (e.g., `.claude/config.json`), target the repository folder.
   - If the harness uses centralized project indexing (e.g., `~/.<harness>/config/projects/`), locate the file matching the current workspace path.

3. **Read Before Writing (Live Schema Conformance)**:
   - Always read the target file on disk before constructing the configuration.
   - Inspect existing keys and nesting to determine the active schema on that machine.
   - Adapt the insertion to match existing keys (e.g., `userSettings.globalPermissionGrants`, `permissions`, `allowedTools`) instead of imposing an assumed schema.
   - Preserve all unrelated keys and settings.

---

### 5. Transparent Briefing Before Applying Changes

Always present a 4-part transparent briefing to the user before modifying any configuration:

1. **Target File Path**: State the resolved absolute path on disk.
2. **Enforcement and Schema**: Explain in 1–2 direct sentences how the harness enforces this file and where the rules fit in its schema.
3. **Full Preview Block**: Render the complete, exact configuration block showing every rule formatted for that specific file.
4. **Execution Confirmation**: Ask for explicit confirmation before writing to disk.

---

### 6. Apply, Backup, and Verify

1. Upon user approval, create a backup copy of the target file (e.g., `<file>.bak`).
2. Write or merge the new permission configuration.
3. Read back the file to confirm file integrity and report the updated absolute path.
4. If writing is blocked or denied, print the full configuration block with clear instructions for manual placement.
