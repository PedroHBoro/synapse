# ADR 0002: Testing Strategy and LLM Mocking

## Status
Accepted

## Context
Testing applications that rely on LLMs is challenging due to costs, latency, and non-deterministic outputs. We need a reliable way to test our business logic without hitting live APIs during unit tests.

## Decision
1. **Unit Tests**: Will focus on data parsing, file writing, and manifest management.
2. **LLM Mocking**: We will use `pytest-mock` and custom "Dummy LLM" implementations to simulate agent responses.
3. **Contract Testing**: We will use Pydantic models to enforce schemas on LLM outputs.
4. **Integration Tests**: Will be used sparingly with local models or specific test keys.

## Consequences
- **Positive**: Fast, deterministic, and free test suite. Robust handling of LLM hallucinations.
- **Negative**: Requires more effort to set up initial mock structures.
