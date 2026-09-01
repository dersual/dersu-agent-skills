# Coding Standards

Engineering conventions and quality standards for this codebase. Automated tooling (formatters/linters) handles syntax; this document defines structure, boundaries, error handling, and slop prevention.

## 1. Structure & Simplicity (Code Judo)

- **Zero Useless Indirection:** Do not create identity wrappers, single-use classes, or pass-through helpers. Inline until genuine reuse emerges (Rule of Three).
- **Flat Control Flow:** Prefer early returns, guard clauses, and pattern matching. Avoid deep nesting (> 2 levels).
- **File & Module Scope:** Keep files focused. Decompose modules approaching 500–1,000 lines into focused, colocated modules.
- **Canonical Layering:** Keep business logic in domain/service layers. Do not leak domain rules into UI, routing, or presentation components.
- **Contract & Alias Stability:** Do not delete backwards-compatibility aliases or public exports that protect existing callers without an explicit deprecation plan.

## 2. Types & Invariants

- **No Type Escapes:** Never use `any` or `as unknown as T` to silence compiler errors. Fix types at the boundary.
- **Parse at the Boundary:** Validate untrusted external data (HTTP, CLI, disk, environment) at the perimeter into typed domain models. Keep internal trusted paths lean and direct.
- **Data Shapes:** Default to plain objects/interfaces and pure functions over complex class inheritance hierarchies.

## 3. Anti-Slop (Clean AI Output)

- **No Narration Comments:** Never write comments explaining *what* code does (e.g., `// return response` or `// increment counter`). Comment only non-obvious *why* (business constraints, algorithmic subtleties, workarounds).
- **Preserve Navigation Banners:** Structural section headers (e.g., `// ── DOM BINDINGS ──` or block labels) that aid visual scanning in large files are welcome. Only strip redundant syntax narration.
- **Natural, Humanized Prose:** Keep PR descriptions, commit messages, and markdown documentation concise, direct, and free of chatbot filler, inflated claims, or marketing fluff.
- **No Paranoia Guards:** Avoid wrapping trusted internal code in defensive `try/catch` blocks that swallow errors or return silent fallbacks. Fail fast and let errors bubble to designated boundary handlers.
- **Preserve Local Idioms:** Match existing codebase style, naming conventions, and patterns rather than introducing foreign paradigms or unnecessary third-party dependencies.

## 4. Tests

- **Public Seams & Invariants:** Test observable public behavior and contracts, not private internal mechanics.
- **No Tautological Tests:** Avoid tests that merely re-assert mocks or mirror implementation details.
- **Avoid Excessive Mocking:** Prefer fast, deterministic integration and unit tests over heavy mock graphs.
