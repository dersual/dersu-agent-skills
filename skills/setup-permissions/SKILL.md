---
name: setup-permissions
description: Configures agent permission boundaries (allow, ask, deny) and Auto Mode posture. Use when setting up a repository, enabling Auto Mode, reducing confirmation prompts, or fixing sandbox permission errors.
---

# Setup Permissions

Interview the user one question at a time. Collect all preferences before reading or writing configuration files.

---

### 1. Identify Harness, Scope, and Execution Posture

1. **Harness Detection**:
   - Ask: *"Which agent harness are you configuring?"*
   - Offer the active harness as the recommended option when environment cues identify it.

2. **Scope Selection**:
   - Ask: *"Which scope are you configuring? (Global / Cross-Surface, Project-Specific, or Both)"*
   - **Global / Cross-Surface**: Sets machine-wide invariants across all projects.
   - **Project-Specific**: Sets tool runners, protected subpaths, or MCP permissions for the active repository.

3. **Auto Mode and Sandbox Posture**:
   - Ask: *"Do you want Auto Mode and Sandbox enabled as your default workflow, with explicit Deny and Ask guardrails?"*
   - Recommend **Yes** so routine workspace work runs without constant prompts.

Done when: harness, scope, and Auto Mode posture are recorded.

---

### 2. Confirm Security Baseline Defaults

Present these baseline rules and ask the user to accept or adjust them:

- **Deny (Unconditional Block)**:
  - `~/.ssh` and `~/.ssh/*` (protects SSH private keys)
  - Root, home, or drive-root wipe commands (e.g., `rm -rf /*`, `rm -rf ~*`, `Remove-Item * -Recurse -Force C:*`)
  - `.git` metadata writes, using only path or glob formats the harness supports (omit relative `.git` paths when the harness rejects them)
- **Ask (Explicit Confirmation)**:
  - `*.env*` (secrets and API keys; allow `*.env.example` if desired)
  - Cloud sync directories (e.g., `OneDrive`, `Dropbox`, `Google Drive`)
  - Normal file deletion commands (e.g., `rm`, `Remove-Item`) so project cleanups still work when approved
  - Remote, history-rewriting, or destructive git commands (e.g., `git push`, `git reset`, `git clean`, `git rebase`, `git branch -D`, `git checkout --force`, `git stash clear`, `git remote set-url`)
  - Fallback `*` for file writes and unknown shell commands outside designated folders
- **Allow (Silent Execution)**:
  - Safe read-only inspection commands across POSIX and PowerShell (e.g., `ls`, `dir`, `rg`, `grep`, `find`, `pwd`, `which`, `Get-ChildItem`, `Get-Location`, `Get-Command`, `Select-String`, `Test-Path`)
  - Shell file-readers (`cat`, `type`, `Get-Content`) only when paired with shell-level `Ask` rules for `*.env*` and `Deny` rules for `~/.ssh`
  - Standard local `git` commands (e.g., `status`, `diff`, `log`, `add`, `commit`, `checkout`, `branch`)

Ask: *"Do you want to accept these baseline rules or modify any of them?"*

Done when: the user confirms the baseline rules or lists exact changes.

---

### 3. Gather Workspace Topology and Tools

1. **Root Coding Directory (Unrestricted File Writes)**:
   - Ask: *"Which root directory stores your coding projects where file edits should run without prompts?"*

2. **Protected Subdirectories (Supervised File Writes)**:
   - Ask: *"Which subdirectories inside your coding workspace require confirmation before writes (e.g., coursework, exam prep, client work)?"*

3. **Project and Utility Runtimes**:
   - Ask: *"Which additional command-line tools should run without prompts?"*
   - Keep project-specific runtimes (`pytest`, `npm`, `pdflatex`) in project-level configurations rather than global configurations.

Done when: root directory, protected subdirectories, and allowed tools are recorded.

---

### 4. Discover Live Harness Configuration

1. **Apply Maximum Surface Coverage**:
   - For Global scope, locate the configuration file shared across all interfaces of the harness (Desktop App, CLI, IDE extensions).
   - Consult harness documentation, CLI `--help`, or config directories to confirm the active storage path.
   - Check the Auto Mode and Sandbox configuration keys.
   - Verify whether Auto Mode pauses on `ask` rules or enforces `deny` rules only.
   - Check if an orchestrator or ADE (such as Orca) launches the harness.
   - Verify whether that orchestrator defers to the harness config or bypasses `ask` rules.

2. **Locate Project Storage**:
   - For Project scope, locate the in-repo configuration file or centralized project store matching the active workspace.

3. **Read Before Writing (Live Schema Conformance)**:
   - Read the target configuration file on disk before building changes.
   - Match the active schema, key names, and path format rules (such as absolute-path requirements for sandbox deny rules).
   - On Windows, include both forward-slash and backslash path variants where the harness matches raw strings.
   - Preserve all unrelated keys and settings.

Done when: target file path, active schema, path constraints, and Auto Mode / ADE behavior are verified.

---

### 5. Present Briefing Before Writing

Present a 4-part briefing before modifying any file:

1. **Target File Path**: State the resolved absolute path on disk.
2. **Enforcement and Auto Mode Interaction**: Explain in 1–2 short sentences how the harness enforces the rules and how Auto Mode or any ADE wrapper handles `ask` and `deny`.
3. **Full Preview Block**: Show the exact configuration block formatted for that file.
4. **Execution Confirmation**: Ask for explicit approval before writing to disk.

Done when: the user approves the preview block.

---

### 6. Apply, Backup, Verify, and Smoke-Test

1. Create a backup copy of the target file (e.g., `<file>.bak`).
2. Write or merge the updated configuration.
3. Read back the file to verify syntax and integrity.
4. Run one harmless command (e.g., `git status` or directory listing).
5. Confirm the harness loads the new permissions without sandbox or schema errors.
6. If writing is blocked, print the full configuration block with manual placement steps.

Done when: the updated file is verified on disk and the smoke-test command succeeds.
