# solution-policies-hub

This repository is the **central source of truth** for all solution agents. It defines the standards, procedures, and personas that every agent must follow when working on DataMiner solutions.

## Contents

- [`policies/global-instructions.md`](policies/global-instructions.md) — General coding standards, conciseness rules, error handling protocols, and the **standard validation output format** used by all policy files.
- **CI/CD**:
  - [`policies/cicd/github-guidelines.md`](policies/cicd/github-guidelines.md) — Validation rules for GitHub repository setup and conventions.

## Severity System

All instructions use severity tags to indicate enforcement level:

- **[ERROR]** — Blocks the pipeline; must be fixed before proceeding
- **[WARNING]** — Should be addressed but does not block the pipeline  
- **[INFO]** — Informational guideline; no enforcement

See [`policies/severity-enforcement.md`](policies/severity-enforcement.md) for implementation details and CI/CD integration examples.

## Validation Output

Every policy file contains a numbered **Validation Process** section. When running a validation, results must be presented as a structured table — one block per policy applied, with a row for each numbered check.

The format (table structure, status values, and rules) is defined once in [`policies/global-instructions.md`](policies/global-instructions.md#validation-output-format) and applies to all policy files.


