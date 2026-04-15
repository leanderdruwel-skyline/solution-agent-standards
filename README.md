# solution-policies-hub

This repository is the **central source of truth** for all solution agents. It defines the standards, procedures, and personas that every agent must follow when working on DataMiner solutions.

## Contents

- [`policies/global-instructions.md`](policies/global-instructions.md) — General coding standards, conciseness rules, and error handling protocols.
- [`policies/agent-persona.md`](policies/agent-persona.md) — Defines the "Senior Solution Architect" persona that all agents should adopt.
- [`policies/severity-enforcement.md`](policies/severity-enforcement.md) — **Defines how to distinguish between blocking errors and warnings** in all instruction files.
- [`policies/solution-architecture.md`](policies/solution-architecture.md) — Guidelines for building scalable solutions. Agents working on repositories whose name starts with `sol-` **must** check this file.
- [`policies/solution-naming.md`](policies/solution-naming.md) — Naming conventions for solution repositories. Agents working on repositories whose name starts with `ldr-` **must** check this file.
- **CI/CD**:
  - [`policies/cicd/github-guidelines.md`](policies/cicd/github-guidelines.md) — Validation rules for GitHub repository setup and conventions.

## Severity System

All instructions use severity tags to indicate enforcement level:

- **[ERROR]** — Blocks the pipeline; must be fixed before proceeding
- **[WARNING]** — Should be addressed but does not block the pipeline  
- **[INFO]** — Informational guideline; no enforcement

See [`procedures/severity-enforcement.md`](procedures/severity-enforcement.md) for implementation details and CI/CD integration examples.


