# ADR 0003: Configuration Management with Pydantic Settings

## Status
Accepted

## Context
The application needs to manage sensitive data (API Keys) and user preferences (Vault paths, model selection) across different environments.

## Decision
We will use `pydantic-settings` to manage configuration.
- **Priority**: Env vars > `.env` file > `~/.synapse/settings.yaml` > Defaults.
- **Validation**: Configurations will be validated at startup. Missing keys will trigger user-friendly errors via `rich`.
- **Defaults**: The system will define a default data loader (e.g., `google-takeout`) in the settings, which can be overridden via CLI flags or the `settings.yaml` file.

## Consequences
- **Positive**: Type-safe configuration; automatic validation; clear error messages.
- **Negative**: Adds a dependency (`pydantic-settings`).
