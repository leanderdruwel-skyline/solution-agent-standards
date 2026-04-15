# solution-policies-hub

This repository is the **central source of truth** for all solution agents. It defines the standards, procedures, and personas that every agent must follow when working on DataMiner solutions.

## Contents

- [`policies/global-instructions.md`](policies/global-instructions.md) — General coding standards, conciseness rules, and error handling protocols.
- **CI/CD**:
  - [`policies/cicd/github-guidelines.md`](policies/cicd/github-guidelines.md) — Validation rules for GitHub repository setup and conventions.

## Severity System

All instructions use severity tags to indicate enforcement level:

- **[ERROR]** — Blocks the pipeline; must be fixed before proceeding
- **[WARNING]** — Should be addressed but does not block the pipeline  
- **[INFO]** — Informational guideline; no enforcement

See [`procedures/severity-enforcement.md`](procedures/severity-enforcement.md) for implementation details and CI/CD integration examples.


