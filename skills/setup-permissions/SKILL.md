---
name: setup-permissions
description: Configure global or repo agent permissions (allow, ask, deny). Use when setting up permissions, hardening Full access or Auto Mode guardrails, reducing prompts, or fixing sandbox errors.
---

# Setup Permissions

Interview the user one question at a time. Collect all preferences before reading or writing configuration files.

---

### 1. Identify Harness, Scope, and Posture

1. **Harness**: Ask which agent harness to configure. Recommend the active harness when environment cues identify it.
2. **Scope**: Ask whether to configure **Global / Cross-Surface** (recommended default for machine-wide rules) or **Project-Specific** (only when a repo needs custom isolation).
3. **Posture**: Ask which execution posture the user wants:
   - **Full access + Hardened Deny (Recommended)**: Use Full access (or Auto Mode) for normal coding, switch to Ask mode only in protected folders, and put non-negotiable guardrails in `Deny`. Skip per-project `allow` lists.
   - **Ask mode + Allowlist**: Fail closed on `Ask` for unknown commands and maintain explicit `Allow` rules for routine tools.

Done when: harness, scope, and posture are recorded.

---

### 2. Confirm Security Baseline

Present these baseline rules and ask the user to accept or adjust them:

- **Deny (Unconditional Block — survives Full access / `--auto`)**:
  - `~/.ssh` and `~/.ssh/*`
  - Root, home, or drive-root wipe commands (`rm -rf /*`, `rm -rf ~*`, `Remove-Item * -Recurse -Force C:*`)
  - `.git` metadata writes, using only path or glob formats the harness accepts
  - `*.env*` secret files across read, edit, and shell tools (allow `*.env.example` explicitly)
  - Destructive or history-rewriting git commands (`git reset --hard`, `git clean -fd`, `git clean -fdx`, `git rebase`, `git branch -D`, `git checkout --force`, `git checkout -f`, `git stash clear`, `git remote set-url`)
- **Ask (Prompts in Ask mode and harnesses whose Auto Mode honors `ask`)**:
  - Protected subdirectories (e.g., coursework, exam prep, client work)
  - Cloud sync directories (`OneDrive`, `Dropbox`, `Google Drive`)
  - `git push` (or move to `Deny` if the user prefers pushing manually)
  - Normal file deletion (`rm`, `Remove-Item`) and fallback `*` when using Ask mode
- **Allow (Needed only when staying in Ask mode)**:
  - Safe read-only inspection commands across POSIX and PowerShell (`ls`, `dir`, `rg`, `grep`, `find`, `pwd`, `which`, `Get-ChildItem`, `Get-Location`, `Get-Command`, `Select-String`, `Test-Path`)
  - Shell file-readers (`cat`, `type`, `Get-Content`) only when `*.env*` and `~/.ssh` are blocked in `Deny`
  - Standard local `git` commands (`status`, `diff`, `log`, `add`, `commit`, `checkout`, `branch`)
  - MCP tools (`mcp(*)`, or read-only MCP allowed with write/delete MCP on `Ask`)

Done when: the user confirms the baseline rules or lists exact changes.

---

### 3. Gather Workspace Topology

1. **Root Coding Directory**: Ask which root directory holds coding projects.
2. **Protected Subdirectories**: Ask which subdirectories require confirmation before writes (e.g., coursework, client work).
3. **Additional Runtimes (Ask mode only)**: If using Ask mode, ask which runtimes (`python`, `node`, `npm run`, `dotnet`, `pdflatex`) should run silently. Scope script runners to subcommands where supported.

Done when: root directory, protected subdirectories, and any Ask-mode runtimes are recorded.

---

### 4. Discover Live Harness Configuration

1. **Locate Global Config**: Find the config file shared across all interfaces of the harness (Desktop App, CLI, IDE extensions).
2. **Verify Mode & ADE Interaction**:
   - Check Auto Mode, Full access, and Sandbox keys in harness docs or `--help`.
   - Verify whether Auto Mode honors `ask` rules or enforces `deny` only.
   - Check if an ADE (such as Orca) wraps the harness and whether it defers to harness config or bypasses `ask` rules.
3. **Locate Project Config**: For Project scope, find the in-repo config file or project store.
4. **Read Before Writing**: Read the target file on disk. Match its active schema, key names, and path constraints (on Windows, include both `/` and `\` variants when the harness matches raw strings). Preserve unrelated keys.

Done when: target path, active schema, path constraints, and ADE/mode behavior are verified.

---

### 5. Present Briefing Before Writing

Present a 4-part briefing before modifying any file:

1. **Target File Path**: State the resolved absolute path on disk.
2. **Enforcement & Mode Interaction**: State in 1–2 sentences how the harness enforces `ask` and `deny` under Auto Mode or Full access.
3. **Full Preview Block**: Show the exact configuration block formatted for that file.
4. **Execution Confirmation**: Ask for explicit approval before writing to disk.

Done when: the user approves the preview block.

---

### 6. Apply, Backup, Verify, and Smoke-Test

1. Back up the target file (e.g., `<file>.bak`).
2. Write or merge the updated configuration.
3. Read back the file to verify syntax and integrity.
4. Run one harmless command (e.g., `git status` or the harness config validator) to confirm the config loads without errors.
5. If writing is blocked, output the full configuration block with manual placement steps.

Done when: the updated file is verified on disk and the smoke-test command succeeds.
