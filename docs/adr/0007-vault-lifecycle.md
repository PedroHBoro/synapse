# ADR 0007: Vault Lifecycle (Init, Import, Garden)

## Status
Accepted

## Context
We need a clear separation of concerns for how a vault is created, populated, and maintained to ensure a smooth user experience and long-term data integrity.

## Decision
We will define three distinct phases/operations for the vault lifecycle:

1. **Initialization (`init`)**: Creates the full vault skeleton. This includes the folder structure (`/Journal`, `/Atlas`, `/Identity`, `/Meta`), the `AGENTS.md` at root, initial `Index.md` files, and the `.synapse/manifest/` persistence layer.
2. **Ingestion/Importation (`process`)**: The core workflow. If the target directory is not a Synapse vault, it will auto-initialize. It loads raw data, runs the Distiller/Librarian agents, and populates the vault.
    - **Resilience**: It uses the manifest to skip already processed conversations (Resume capability).
    - **Safety**: Supports a `--dry-run` flag to simulate the process, showing a summary of what would be done without calling LLMs or writing to disk.
3. **Gardening/Maintenance (`garden`)**: A periodic cleanup and sync operation. It audits the vault for external changes (using hashes), fixes broken links, updates indices, and ensures the environment remains "Agent-Ready".

## Consequences
- **Positive**: Clear mental model for the user; robust "auto-fix" capabilities; ensures the vault never drifts too far from the intended structure.
- **Negative**: Requires careful implementation of the "auto-init" logic to avoid accidental overwrites.
