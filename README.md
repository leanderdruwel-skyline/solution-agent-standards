# solution-policies-hub

This repository is the **central source of truth** for all solution agents. It defines the standards, procedures, and personas that every agent must follow when working on DataMiner solutions.

## Contents

- [`procedures/global-instructions.md`](procedures/global-instructions.md) — General coding standards, conciseness rules, and error handling protocols.
- [`procedures/solution-architecture.md`](procedures/solution-architecture.md) — Guidelines for building scalable solutions. Agents working on repositories whose name starts with `sol-` **must** check this file.
- [`procedures/solution-naming.md`](procedures/solution-naming.md) — Naming conventions for solution repositories. Agents working on repositories whose name starts with `ldr-` **must** check this file.
- **Catalog Item Validation** — Procedures for validating Catalog items:
  - [`procedures/catalog/overview.md`](procedures/catalog/overview.md) — Overview of Catalog item validation procedures.
  - [`procedures/catalog/manifest-validation.md`](procedures/catalog/manifest-validation.md) — Validation rules for manifest.yml files.
  - [`procedures/catalog/documentation-validation.md`](procedures/catalog/documentation-validation.md) — Documentation guidelines for CatalogInformation README.
  - [`procedures/catalog/repository-validation.md`](procedures/catalog/repository-validation.md) — GitHub repository configuration validation.
  - [`procedures/catalog/readme-validation.md`](procedures/catalog/readme-validation.md) — Repository and project README validation.
- [`procedures/agent-persona.md`](procedures/agent-persona.md) — Defines the "Senior Solution Architect" persona that all agents should adopt.
- [`procedures/severity-enforcement.md`](procedures/severity-enforcement.md) — **Defines how to distinguish between blocking errors and warnings** in all instruction files.

## Severity System

All instructions use severity tags to indicate enforcement level:

- **[ERROR]** — Blocks the pipeline; must be fixed before proceeding
- **[WARNING]** — Should be addressed but does not block the pipeline  
- **[INFO]** — Informational guideline; no enforcement

See [`procedures/severity-enforcement.md`](procedures/severity-enforcement.md) for implementation details and CI/CD integration examples.


