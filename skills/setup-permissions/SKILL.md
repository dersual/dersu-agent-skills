---
name: setup-permissions
description: Interactively configures runtime permission boundaries (allow, ask, deny) for agent harnesses across workspaces, commands, and sensitive files.
---

# Setup Permissions

Guides the developer through configuring technical permission boundaries across development workspaces, commands, and sensitive paths.

## Process

Use an interactive interview approach (ask questions one at a time) to collect preferences before resolving configuration paths and writing files.

---

### 1. Inquire About the Agent Harness

Prompt the user to identify the target agent environment:

- Ask: *"Which agent harness are you configuring? (e.g., Google Antigravity CLI, Claude Code, Cursor, Codex, Other)"*
- If the current session contains environment cues (such as `~/.gemini/antigravity-cli`, `CLAUDE_PROJECT_DIR`, or system prompt identity), offer that detected harness as the recommended option.

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
   - Note: Recommend keeping project-specific runtimes (`pytest`, `npm`, `pdflatex`) out of global configurations. Keep those in project-level documentation or prompt them interactively.

---

### 4. Resolve Harness Configuration Location

Determine the exact configuration system for the chosen harness:

- **Google Antigravity CLI (`agy`)**:
  - Target file: `~/.gemini/antigravity-cli/settings.json`
  - Mechanism: Evaluates glob patterns across `deny`, `ask`, and `allow` arrays for `write_file(...)` and `command(...)`.
- **Claude Code**:
  - Target file: `~/.claude.json` (user-level) or `.claude/config.json` (project-level).
  - Mechanism: Uses allowed tools and approved command lists.
- **Other / Custom Harnesses**:
  - Conduct targeted research: inspect local configuration files on disk or consult tool documentation to locate where permissions, trusted directories, or command rules reside.

---

### 5. Transparent Briefing Before Applying Changes

Always present a 4-part transparent briefing to the user before modifying any configuration:

1. **Target File Path**: State the exact absolute path on disk (e.g., `C:\Users\<user>\.gemini\antigravity-cli\settings.json`).
2. **Enforcement Mechanics**: Explain in 1–2 direct sentences how this harness evaluates and enforces the rules.
3. **Full Preview Block**: Render the complete, exact configuration block (in JSON/YAML/text format) showing every rule.
4. **Execution Confirmation**: Ask for explicit confirmation before writing to disk. Offer to create a backup file before writing.

#### Example Antigravity CLI Preview Block:

```json
{
  "permissions": {
    "allow": [
      "write_file(C:\\Users\\<user>\\Code Stuff)",
      "command(git)",
      "command(git *)"
    ],
    "ask": [
      "write_file(C:\\Users\\<user>\\Code Stuff\\School Code)",
      "write_file(C:\\Users\\<user>\\Code Stuff\\School Code\\*)",
      "write_file(*.env*)",
      "write_file(C:\\Users\\<user>\\OneDrive)",
      "write_file(C:\\Users\\<user>\\OneDrive\\*)",
      "write_file(*)"
    ],
    "deny": [
      "write_file(.git)",
      "write_file(.git\\*)",
      "write_file(C:\\Users\\<user>\\.ssh)",
      "write_file(C:\\Users\\<user>\\.ssh\\*)"
    ]
  }
}
```

---

### 6. Apply and Verify

1. Upon user approval, create a backup copy of the target file (e.g., `settings.json.bak`).
2. Write or merge the new permission configuration.
3. Confirm file integrity and report the updated absolute path to the user.
4. If writing is blocked or denied, print the full configuration block with clear instructions for manual placement.
