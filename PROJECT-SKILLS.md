# Project-Level Skills & Resources

This file lists skills, plugins, and external resources that can be used selectively for specific repositories, workspaces, or projects rather than being installed globally.

Use this as a reference when a project calls for specialized capabilities that should not be part of the default developer environment.

> **Note:** Global plugins and MCP servers are documented separately in [`PLUGINS-AND-MCP.md`](./PLUGINS-AND-MCP.md). The resources below are intended for project-scoped usage. Installation and configuration may vary by project; prefer documenting project-specific setup in that project's README or configuration files.

---

## How to Use

When a project needs one of these resources:

1. Identify the skill, plugin, or resource relevant to the project.
2. Follow the upstream repository's or resource's official installation and usage instructions.
3. Install or link it within the project/workspace rather than adding it to the global environment when project-level isolation is preferred.
4. Document any project-specific installation or configuration required by contributors.
5. For AI-generated prose or copy, use the [`humanizer`](./skills/humanizer/SKILL.md) skill when appropriate to remove common AI-writing patterns.

Project-local resources may be placed in a repository's `skills/`, `.gemini/`, or other tool-specific project configuration directory depending on the resource and the AI coding environment being used.

---

## UI / UX & Frontend Design

Resources for projects involving frontend development, interface design, visual systems, accessibility, and UX.

### 1. ui-ux-pro-max-skill

**Repository:** [nextlevelbuilder/ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)

An AI-oriented UI/UX design skill providing design guidance, UI patterns, templates, accessibility considerations, and design-system assistance for frontend work.

Use this when a project requires more deliberate UI/UX design support than the general-purpose development environment provides.

Follow the upstream repository's README for installation and project-local setup instructions.

---

### 2. Impeccable

**Website:** https://impeccable.style/

A curated resource for UI patterns, visual language, and accessible component guidance. Useful for generating or refining frontend interfaces and making concrete design decisions rather than relying solely on generic AI-generated UI patterns.

Use this as a design reference when working on frontend projects where visual quality, consistency, accessibility, or component patterns are important.

---

## LLM & AI Research

Resources that are particularly useful for projects involving LLMs, machine learning, datasets, model experimentation, or AI research.

### Hugging Face Skills

**Repository:** [huggingface/skills](https://github.com/huggingface/skills)

A collection of skills for working with Hugging Face models, datasets, and related tooling.

This is particularly useful for LLM-based applications and research projects where model discovery, dataset exploration, evaluation, or other Hugging Face workflows are involved.

See [`PLUGINS-AND-MCP.md`](./PLUGINS-AND-MCP.md) for the existing Hugging Face tooling example and general plugin/MCP documentation.

---

## Humanizer

### humanizer

**Local skill:** [`skills/humanizer/SKILL.md`](./skills/humanizer/SKILL.md)

Use the humanizer skill when AI-generated prose, documentation, copy, or other natural-language output needs to be revised to remove common AI-writing patterns and produce more natural, human-oriented writing.

This skill is already maintained in this repository and can be referenced by project-specific workflows when needed.

---


The resources in this document are **references and recommendations**, not a requirement that every resource be installed into this repository.

Keep project-specific skills and configuration in the project that actually uses them whenever possible. This repository should primarily serve as the catalog and source of guidance for those resources.
