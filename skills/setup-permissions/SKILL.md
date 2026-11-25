---
name: setup-permissions
description: Interactively configures runtime permission boundaries (allow, ask, deny) and Auto Mode posture for agent harnesses across workspaces, commands, and sensitive files.
---

# Setup Permissions

Configures technical permission boundaries and execution mode defaults across workspaces, commands, and sensitive paths.

## Process

Interview the user one question at a time to collect preferences before inspecting configuration files and writing changes.

---

### 1. Identify Harness, Scope, and Execution Posture

1. **Harness Detection**:
   - Ask: *"Which agent harness are you configuring? (e.g., Google Antigravity, OpenCode, Codex, Claude Code, Cursor)"*
   - Offer the active harness as the recommended option when environment cues identify it.

2. **Scope Selection**:
   - Ask: *"Which scope are you configuring? (Global / Cross-Surface, Project-Specific, or Both)"*
   - **Global / Cross-Surface**: Sets machine-wide invariants across all projects.
   - **Project-Specific**: Sets tool runners, protected subpaths, or MCP permissions for the active repository.

3. **Auto Mode and Sandbox Posture**:
   - Ask: *"Do you want Auto Mode + Sandbox enabled as your primary workflow, with explicit Deny/Ask guardrails for sensitive targets?"*
   - Recommend **Yes** so routine workspace work runs without constant prompts while guardrails remain enforced.
   - Verify from harness docs or CLI help whether Auto Mode still pauses on `ask` rules or converts `ask` into `allow` (enforcing `deny` only).

---

### 2. Confirm Security Baseline Defaults

Present the baseline rules and ask the user to accept or adjust them:

- **Deny (Unconditional Block)**:
  - `~/.ssh` and `~/.ssh/*` (protects SSH private keys)
  - Catastrophic system-wipe commands (e.g., `rm -rf /`, `rm -rf ~`)
  - `.git` metadata writes, using only path or glob formats the target harness supports
- **Ask (Explicit Confirmation)**:
  - `*.env*` (secrets and API keys; allow `*.env.example` if desired)
  - Cloud sync directories (e.g., `OneDrive`, `Dropbox`, `Google Drive`)
  - Remote or history-rewriting git commands (e.g., `git push`, `git push --force`, `git reset --hard`, `git clean -fd`)
  - Fallback `*` for file writes and unknown shell commands outside designated folders
- **Allow (Silent Execution)**:
  - Safe read-only inspection commands (e.g., `ls`, `dir`, `cat`, `rg`, `grep`, `find`, `pwd`, `which`)
  - Standard local `git` commands (e.g., `status`, `diff`, `log`, `add`, `commit`, `checkout`, `branch`)

Ask: *"Do you want to accept these baseline rules or modify any of them?"*

---

### 3. Gather Workspace Topology and Tools

1. **Root Coding Directory (Unrestricted File Writes)**:
   - Ask: *"Which root directory stores your coding projects where file edits should run without prompts?"*

2. **Protected Subdirectories (Supervised File Writes)**:
   - Ask: *"Which subdirectories inside your coding workspace require confirmation before writes (e.g., coursework, exam prep, client work)?"*

3. **Project and Utility Runtimes**:
   - Ask: *"Which additional command-line tools should run without prompts?"*
   - Keep project-specific runtimes (`pytest`, `npm`, `pdflatex`) in project-level configurations rather than global configurations.

---

### 4. Discover Live Harness Configuration

1. **Apply Maximum Surface Coverage**:
   - For Global scope, locate the configuration file shared across all interfaces of the harness (Desktop App, CLI, IDE extensions).
   - Consult harness documentation, CLI `--help`, or config directories to confirm the active storage layer and Auto Mode / Sandbox keys.

2. **Locate Project Storage**:
   - For Project scope, locate the in-repo configuration file or centralized project store matching the active workspace.

3. **Read Before Writing (Live Schema Conformance)**:
   - Read the target configuration file on disk before building changes.
   - Match the active schema, key names, and path format rules (such as absolute-path requirements for sandbox deny rules).
   - Preserve all unrelated keys and settings.

---

### 5. Present Briefing Before Writing

Present a 4-part briefing before modifying any file:

1. **Target File Path**: State the resolved absolute path on disk.
2. **Enforcement and Auto Mode Interaction**: Explain in 1–2 direct sentences how the harness enforces the rules and how Auto Mode interacts with `ask` and `deny`.
3. **Full Preview Block**: Show the complete, exact configuration block formatted for that file.
4. **Execution Confirmation**: Ask for explicit confirmation before writing to disk.

---

### 6. Apply, Backup, Verify, and Smoke-Test

1. Create a backup copy of the target file (e.g., `<file>.bak`).
2. Write or merge the updated configuration.
3. Read back the file to verify syntax and integrity.
4. Run one harmless command (e.g., `git status` or directory listing) to verify the harness loads the new permissions without sandbox or schema errors.
5. If writing is blocked, output the full configuration block with manual placement steps.
