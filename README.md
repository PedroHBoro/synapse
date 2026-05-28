# **Synapse: Intelligence-Driven Knowledge Distillation**

## **1. Overview**

**Synapse** is an open-source CLI tool designed to act as a bridge between ephemeral conversation streams (Google Takeout, Gemini, etc.) and a persistent knowledge system (**Obsidian**).

Unlike simple converters, Synapse leverages intelligent agents to:

*   **Distill** raw conversations into atomic, meaningful notes.
*   **Map** knowledge through cascading indexes.
*   **Evolve** a user identity profile (preferences, technical stack, and interests) iteratively.

## **2. Core Features**

*   **Input**: JSON files (Standard Google Takeout format).
*   **Output**: A structured, self-contained Obsidian Vault.
*   **Idempotency**: Smart processing that avoids duplicates via a manifest system.
*   **Tone Preservation**: Maintains the user's personality and writing style in generated notes.
*   **Smart Navigation**: Automated creation of bidirectional links [[ ]].

## **3. Architecture & Tech Stack**

### **3.1 Design Patterns**
*   **Adapter Pattern**: For data ingestion (Input Drivers).
*   **Bridge Pattern**: For LLM integration, allowing easy provider switching.
*   **Strategy Pattern**: For different organization and indexing methods.

### **3.2 Tech Stack**
*   **Language**: Python 3.12+ (Linux environment).
*   **Agent Orchestration**: **CrewAI**.
*   **State Persistence**: Hybrid YAML manifest system located in `.synapse/manifest/`.
*   **CLI Framework**: **Click** with **Rich** for enhanced UI/UX.
*   **Configuration**: **Pydantic Settings**.
*   **Quality**: **Ruff** (Linting/Formatting) and **Pytest** (Testing).

## **4. Execution Roadmap**

### **Milestone 1: Foundation & DX (Developer Experience)**
*   [ ] Initialize CLI structure using Click and Rich.
*   [ ] Implement Configuration Engine with Pydantic Settings (reading `.synapse` and env vars).
*   [ ] Develop Vault Bootstrap logic (folder tree creation and manifest initialization).
*   [ ] Set up Quality Gates (Ruff, Mypy, and Pytest configuration).

### **Milestone 2: Data Ingestion (The Adapter Phase)**
*   [ ] Implement the Input Driver interface (Adapter Pattern).
*   [ ] Develop the Google Takeout JSON Loader/Parser.
*   [ ] Create a comprehensive unit test suite for the loader.

### **Milestone 3: Atomic Distillation (The Distiller Agent)**
*   [ ] Integrate CrewAI with Gemini/OpenAI providers.
*   [ ] Develop the **Distiller** agent (prompts, roles, and tasks).
*   [ ] Build the Markdown Writer with Obsidian-compatible YAML frontmatter.
*   [ ] Implement Mocked Tests to verify distillation logic without hitting live APIs.

### **Milestone 4: Connectivity & Identity (The Librarian Agent)**
*   [ ] Develop the **Librarian** agent for curation and cross-linking.
*   [ ] Implement Identity Evolution logic (updating `User_Profile.md`).
*   [ ] Build the Auto-Linking system for existing `/Atlas` notes.
*   [ ] Automated update of cascading indexes (`Index.md` files).

### **Milestone 5: Resilience & Polish**
*   [ ] Implement robust error handling (API retries, timeouts).
*   [ ] Finalize Progress Persistence in the manifest.
*   [ ] Complete documentation (Contribution guide, CLI `--help`).

## **5. Contributing**

Instructions coming soon. This project follows strict architectural guidelines defined in `GEMINI.md` and ADRs.
