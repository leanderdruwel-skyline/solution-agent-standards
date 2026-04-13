# Solution Architecture

## Scope

These guidelines apply to all agents working on **solution repositories**. If the repository name starts with `sol-`, agents **must** read and follow this file in addition to the [global instructions](global-instructions.md).

---

## Scalable Solution Design

- Design every solution to be horizontally scalable from the start; avoid hard-coded assumptions about a single instance.
- Separate concerns clearly: data ingestion, business logic, and presentation must not be mixed in the same component.
- Prefer loosely coupled, event-driven communication between components over direct synchronous calls where latency allows.
- Define explicit contracts (interfaces, API schemas, message formats) at every integration boundary.
- Avoid sharing mutable state between components; pass data explicitly.

## Modularity and Reusability

- Break large solutions into independently deployable modules or packages.
- Extract reusable logic into shared libraries rather than duplicating it across modules.
- Version shared libraries explicitly; never rely on an unversioned "latest" dependency in production.

## Configuration and Environment

- Externalise all environment-specific configuration (endpoints, credentials, feature flags) so that no code change is required to deploy to a different environment.
- Store secrets in a secrets manager or environment variables, never in source code or configuration files committed to version control.

## Testing and Validation

- Every module must have automated tests that cover the core business logic.
- Integration tests must be run in an environment that mirrors production as closely as possible.
- Validate end-to-end flows after every deployment, not just unit-level behaviour.

## Documentation

- Maintain an architecture decision record (ADR) for significant design choices.
- Keep solution-level README files up to date with setup, deployment, and operational instructions.
- Document all public APIs and integration points with examples.
