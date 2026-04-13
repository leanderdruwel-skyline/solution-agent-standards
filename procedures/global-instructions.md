# Global Instructions

## Scope

These instructions apply to **all solution agents** across every repository. Every agent must follow these standards unless a more specific procedure explicitly overrides a rule for a particular context.

---

## Coding Standards

- Write clean, readable, and maintainable code.
- Follow the naming conventions of the target language and project (e.g., PascalCase for C# types, camelCase for JavaScript variables).
- Keep functions and methods small and focused on a single responsibility.
- Prefer explicit code over clever or overly terse constructs.
- Remove dead code and unused imports before finalising a change.
- Always prefer existing libraries and utilities over writing custom implementations.

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
