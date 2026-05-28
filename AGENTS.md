# Synapse Repository Agent Protocol

This file serves as the **Source of Truth** for all AI agents working on the Synapse codebase.

## 1. Architecture Standards
- **CLI Framework**: Use `click` for commands and `rich` for all terminal output/feedback.
    - Implement a global `--verbose` flag to toggle granular DEBUG logs in the terminal.
- **Agent Orchestration**: Use `crewai`. Keep agent definitions decoupled from CLI logic via callbacks/events.
- **Configuration**: Use `pydantic-settings`. 
    - Global config: `~/.synapse/settings.yaml`.
- **Manifest & State**:
    - Location: Inside the Vault at `.synapse/manifest/`.
    - Format: Hybrid JSON files (one per conversation hash).
    - Use Hash-based auditing (Gardener Sync) to detect external changes.
- **Logging**:
    - Tool: `loguru`.
    - Persistence: Save logs to `.synapse/logs/` within the Vault for traceability.
- **Vault Lifecycle**:
    - `init`: Generates the full skeleton (Folders, AGENTS.md, GEMINI.md, CLAUDE.md, .cursorrules, AI.md at root, Indices, Manifest).
    - `process`: Imports/Distills data. Supports `--dry-run` and auto-resumes via manifest. Auto-initializes if the vault is missing.
    - `garden`: Audits and maintains the vault integrity.

## 2. Tooling & Workflow
- **Linter/Formatter**: Use `ruff`.
- **Testing**: Use `pytest` with `pytest-mock`. 
    - No live API calls in unit tests.
- **Documentation**: All major decisions must be in `docs/adr/`. README must be in English.

## 3. Data Integrity & Non-Interference
- **Non-Interference**: Synapse agents MUST NOT modify existing manual content in `/Atlas` or `/Journal`.
- **Structural Focus**: Synapse's "intelligence" is dedicated to **Distillation** (new notes), **Indexing** (MOCs), and **Linking**.
- **User Sovereignty**: The user's personal notes and their interactions with external AI agents are outside Synapse's management scope.
- Use Pydantic models for ALL internal data structures.
