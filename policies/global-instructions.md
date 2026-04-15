# Global Instructions

## Scope

These instructions apply to **all solution agents** across every repository. Every agent must follow these standards unless a more specific procedure explicitly overrides a rule for a particular context.

---

## Severity Levels

**All instructions across all procedure files** use the following severity indicators:

- **[ERROR]** — Blocks the pipeline; must be fixed before proceeding
- **[WARNING]** — Should be addressed but does not block the pipeline
- **[INFO]** — Informational guideline; no enforcement

**Default behavior**: When no severity tag is present, treat the instruction as **[WARNING]**.

See [`severity-enforcement.md`](severity-enforcement.md) for detailed implementation guidelines and CI/CD integration examples.

---

## Coding Standards

- **[WARNING]** Write clean, readable, and maintainable code.
- **[WARNING]** Follow the naming conventions of the target language and project (e.g., PascalCase for C# types, camelCase for JavaScript variables).
- **[INFO]** Keep functions and methods small and focused on a single responsibility.
- **[INFO]** Prefer explicit code over clever or overly terse constructs.
- **[WARNING]** Remove dead code and unused imports before finalising a change.
- **[INFO]** Always prefer existing libraries and utilities over writing custom implementations.

## Conciseness Rules

- Make the **smallest possible change** that fully addresses the requirement. Avoid touching unrelated code.
- Do not add comments unless they match the style of the surrounding code or are required to explain a non-obvious decision.
- Avoid unnecessary blank lines, trailing whitespace, or reformatting of unchanged code.
- Summaries, commit messages, and PR descriptions should be brief and to the point.

## Error Handling Protocols

- Never silently swallow exceptions. At minimum, log the error with enough context to diagnose the problem.
- Distinguish between recoverable errors (handle gracefully and continue) and unrecoverable errors (fail fast with a clear message).
- Validate inputs at the boundary of every public API or entry point; do not assume callers have sanitised data.
- Use structured error types or result objects rather than relying solely on generic exceptions where the language supports it.
- Always clean up resources (connections, file handles, locks) in a `finally` block or equivalent, regardless of whether an error occurred.

---

## Validation Output Format

This section defines the standard output format for **all policy validations** across every policy file in this repository. Every policy file contains a numbered **Validation Process** section; the output below is how those results must always be presented.

### Structure

For each policy file applied during a validation, output a block with:
1. A section header identifying the policy by its folder and file name
2. A results table with one row per numbered check from that policy's Validation Process section
3. A result line summarising the outcome for that policy

When multiple policy files are applied in a single validation run, output one block per policy in the order they were applied, followed by a single overall summary line.

### Table format

```
### {folder} / {filename}

| #  | Check                   | Severity | Status              | Notes                                   |
|----|-------------------------|----------|---------------------|-----------------------------------------|
| 1  | [check name]            | ERROR    | ✅ Compliant        |                                         |
| 2  | [check name]            | ERROR    | ❌ Non-compliant    | [reason]                                |
| 3  | [check name]            | WARNING  | ⚠️ Non-compliant   | [reason]                                |
| 4  | [check name]            | WARNING  | N/A                 | [why it does not apply]                 |

**Result: ❌ 1 error · 1 warning · 1 N/A**
```

### Status values

| Status | When to use |
|--------|-------------|
| ✅ Compliant | The check passes with no issues |
| ❌ Non-compliant | An `[ERROR]`-level rule is violated |
| ⚠️ Non-compliant | A `[WARNING]`-level rule is violated |
| N/A | The check does not apply to this repository |

### Rules

- The `#` column must use the same numbering as the **Validation Process** section of the policy file being applied.
- The **Notes** column is left empty for compliant rows; it must be filled in for every non-compliant or N/A row.
- The **Result** line counts only errors and warnings that are non-compliant; N/A items are listed separately.
- `[INFO]`-level findings may be appended below the table as a plain bullet list under an **Improvement suggestions** heading — they do not appear as rows in the table.
