# ADR 0006: Agent-Ready Vault Documentation

## Status
Accepted

## Context
Synapse aims to create a vault that serves as long-term memory for the user, accessible by multiple AI agents. These agents need clear instructions on how to interact with the vault.

## Decision
The `synapse init` command will generate a comprehensive **Agent Protocol Kit** at the root of the vault.

1. **Multi-Agent Support**: It will create specific documentation for major AI agents to ensure they inherit the vault's context:
    - `AGENTS.md`: The master human-legible documentation (Source of Truth).
    - `GEMINI.md`: Optimized for Gemini CLI and Google models.
    - `CLAUDE.md`: Optimized for Anthropic Claude.
    - `.cursorrules`: Optimized for the Cursor editor.
    - `AI.md`: General fallback for various Obsidian AI plugins.
2. **Referral Strategy**: To avoid data duplication (DRY), agent-specific files will act as "Pointers," instructing the AI to read the root `AGENTS.md` for core rules, while providing model-specific behavioral tips.
3. **Engagement Rules**: Instructions will provide a clear map for external agents:
    - Describe the folder hierarchy and YAML standards to help external agents "understand" the context.
    - Encourage agents to respect the vault's organization to maintain compatibility with Synapse's gardening tools.
    - Synapse itself will prioritize **Structural Integrity** (indexing, linking) and will not interfere with manual content in existing notes.
4. **Skeleton Template**: These files are part of the initial vault skeleton, ensuring an "AI-Native" environment from the start.

## Consequences
- **Positive**: Immediate visibility for AI agents; clear entry point for vault documentation.
- **Negative**: Adds one more file to the vault root (though this is standard for project documentation).
