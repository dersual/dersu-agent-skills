# 🔌 Plugins & MCP Servers Setup Guide

This document details the configuration, repository links, and setup for **plugins** and **MCP (Model Context Protocol) servers** configured in `~/.gemini/config/mcp_config.json` for Google Antigravity (AGY) / Gemini CLI and general AI coding tools.

---

## 🛠️ Configured MCP Servers

Below are the official documentation links, GitHub repositories, and sample configurations for each registered MCP server.

### 1. [StitchMCP Server](https://stitch.withgoogle.com)
* **Official Docs / Repositories**: [Google Stitch](https://stitch.withgoogle.com) | [davideast/stitch-mcp](https://github.com/davideast/stitch-mcp) | [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)
* **Description**: Connects AI agents to Google Stitch UI design remote endpoints (`https://stitch.googleapis.com/mcp`) via `mcp-remote` with API key authentication.
* **Note**: *Repository configurations can sometimes be older; it is recommended to check the [Google Stitch Documentation](https://stitch.withgoogle.com) for the latest setup instructions.*
* **Configuration (`mcp_config.json`)**:
  ```json
  "StitchMCP": {
    "command": "npx",
    "args": [
      "-y",
      "mcp-remote",
      "https://stitch.googleapis.com/mcp",
      "--header",
      "X-Goog-Api-Key: <YOUR_API_KEY>"
    ]
  }
  ```

---

### 2. [context7 MCP Server](https://context7.com)
* **Official Docs / Repositories**: [context7.com](https://context7.com) | [upstash/context7](https://github.com/upstash/context7)
* **Description**: Real-time documentation resolution engine by Upstash, fetching and injecting version-specific API docs directly into prompt contexts.
* **Note**: *Repository configurations can sometimes be older; it is recommended to check the [Official Context7 Documentation](https://context7.com) for the latest setup instructions.*
* **Configuration (`mcp_config.json`)**:
  ```json
  "context7": {
    "serverUrl": "https://mcp.context7.com/mcp",
    "headers": {
      "CONTEXT7_API_KEY": "<YOUR_CONTEXT7_API_KEY>"
    }
  }
  ```

---

### 3. [github MCP Server](https://github.com/github/github-mcp-server)
* **Official Docs / Repository**: [github/github-mcp-server](https://github.com/github/github-mcp-server)
* **Description**: Official GitHub Copilot MCP remote server integration (`https://api.githubcopilot.com/mcp/`) for repository search, issue management, PR code reviews, and workflow automation.
* **Note**: *Repository configurations can sometimes be older; it is recommended to check the [Official GitHub MCP Server Guide](https://github.com/github/github-mcp-server) for the latest setup instructions.*
* **Configuration (`mcp_config.json`)**:
  ```json
  "github": {
    "serverUrl": "https://api.githubcopilot.com/mcp/",
    "headers": {
      "Authorization": "<YOUR_GITHUB_TOKEN>"
    }
  }
  ```

---

### 4. [firebase-mcp-server](https://firebase.google.com/docs/cli/mcp-server)
* **Official Docs / Repository**: [Firebase MCP Server Official Guide](https://firebase.google.com/docs/cli/mcp-server) | [firebase/firebase-tools](https://github.com/firebase/firebase-tools) | [firebase/agent-skills](https://github.com/firebase/agent-skills)
* **Description**: Official Firebase tools MCP server bundled into `firebase-tools`, enabling agents to manage Firebase projects, Firestore, Auth, and Security Rules.
* **Note**: *Repository configurations can sometimes be older; it is recommended to check the [Official Firebase MCP Guide](https://firebase.google.com/docs/cli/mcp-server) for the latest setup instructions.*
* **Configuration (`mcp_config.json`)**:
  ```json
  "firebase-mcp-server": {
    "command": "npx",
    "args": ["-y", "firebase-tools@latest", "mcp"]
  }
  ```

---

### 5. [figma-dev-mode-mcp-server](https://github.com/figma/mcp-server-guide)
* **Official Docs / Repository**: [figma/mcp-server-guide](https://github.com/figma/mcp-server-guide) | [Official Figma Dev Mode MCP Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server)
* **Description**: Figma Dev Mode MCP server running locally via an SSE bridge (`http://127.0.0.1:3845/sse`) for extracting design components, tokens, and properties directly from Figma.
* **Note**: *Repository configurations can sometimes be older; it is recommended to check the [Official Figma Guide](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Dev-Mode-MCP-Server) for the latest setup instructions.*
* **Configuration (`mcp_config.json`)**:
  ```json
  "figma-dev-mode-mcp-server": {
    "command": "npx",
    "args": ["mcp-remote", "http://127.0.0.1:3845/sse"]
  }
  ```

---

## 🔌 Registered Plugins

Plugins are installed under `~/.gemini/config/plugins/`.

### 1. [agent-skills](https://github.com/addyosmani/agent-skills)
* **Description**: Comprehensive suite of software engineering skills and subagents (`code-reviewer`, `security-auditor`, `test-engineer`, `web-performance-auditor`).
* **Repository**: [https://github.com/addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)
* **Installation**: See [README.md](README.md#📦-external-skills--antigravity-plugins).

---

### 2. [modern-web-guidance-plugin](https://github.com/GoogleChrome/modern-web-guidance)
* **Description**: Curated collection of agent skills for modern web development by Chrome and Edge teams.
* **Repository**: [https://github.com/GoogleChrome/modern-web-guidance](https://github.com/GoogleChrome/modern-web-guidance)
* **Installation**:
  ```bash
  git clone https://github.com/GoogleChrome/modern-web-guidance.git ~/.gemini/config/plugins/modern-web-guidance-plugin
  # Or for general AI tools:
  npx modern-web-guidance@latest install
  ```

---

### 3. [firebase agent-skills](https://github.com/firebase/agent-skills)
* **Description**: Official Firebase agent skills (`firebase-basics`, `firebase-auth-basics`, `firebase-app-hosting-basics`, `firebase-ai-logic-basics`, `firebase-crashlytics`).
* **Repository**: [https://github.com/firebase/agent-skills](https://github.com/firebase/agent-skills)
* **Official Docs**: [https://firebase.google.com/docs/cli](https://firebase.google.com/docs/cli)

---

### 4. [android-cli-plugin](https://github.com/android/skills)
* **Description**: Official Android developer tools plugin providing `android-cli` skills for SDK management, project creation, emulator orchestration, and build diagnostics.
* **Repository**: [https://github.com/android/skills](https://github.com/android/skills)

---

## 🤗 Additional Skill Sources

### [Hugging Face Skills](https://github.com/huggingface/skills)
* **Repository**: [https://github.com/huggingface/skills](https://github.com/huggingface/skills)
* **Description**: Official Hugging Face skills for model searching, dataset exploration, fine-tuning (`hf-cli`, `huggingface-datasets`, `huggingface-llm-trainer`).
* **Installation**:
  ```bash
  npx skills add huggingface/skills -g
  ```

---

## 📂 Configuration File Locations

| Asset | Path |
| :--- | :--- |
| **MCP Server Config File** | `~/.gemini/config/mcp_config.json` (`%USERPROFILE%\.gemini\config\mcp_config.json`) |
| **Plugins Directory** | `~/.gemini/config/plugins/` (`%USERPROFILE%\.gemini\config\plugins\`) |
