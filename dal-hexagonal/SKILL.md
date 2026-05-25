---
name: dal-hexagonal
description: Implement a Laravel data access layer with strict Hexagonal architecture (Ports and Adapters), isolating domain logic from infrastructure and enabling replaceable persistence adapters with contract-level confidence.
license: MIT
metadata:
  author: team
---

# Data Access Layer: Hexagonal (Ports and Adapters)

Use this skill when long-term domain integrity and infrastructure replaceability are strategic requirements.

## Outcome

Produce DAL code where:

- domain layer depends only on port interfaces,
- infrastructure adapters implement persistence details,
- command/write and query/read flows are explicitly separated,
- transaction and messaging consistency are engineered intentionally,
- adapter changes do not break domain use cases.

## Quick Decision Rule

Choose this style when one or more are true:

- multiple storage/adapters are expected (SQL + search + external systems),
- domain must remain independent from framework internals,
- business workflows are long-lived and mission-critical,
- team needs high-confidence adapter substitution via contract tests.

Avoid strict hexagonal for small apps where cost exceeds benefit.

## Core Workflow

1. Define domain use case and aggregate invariants.
2. Define input/output contracts and domain ports.
3. Implement application service against ports only.
4. Implement infrastructure adapters (Eloquent/SQL/etc).
5. Bind ports to adapters in infrastructure providers.
6. Add transaction, outbox, and idempotency policy.
7. Validate with contract + integration + feature tests.

## Definition of Done

A DAL change is complete only if:

- domain/application layers are infra-agnostic,
- each port has explicit behavior guarantees,
- adapters pass contract tests and integration tests,
- side effects are safely coordinated with persistence,
- observability and performance constraints are defined.

## Additional Resources

Read only what is needed for the current task:

- [Principles and boundaries](principles.md)
- [Transactions and consistency](transactions-and-consistency.md)
- [Testing matrix](testing-matrix.md)
- [Anti-patterns to reject](anti-patterns.md)
- [Examples and templates](examples.md)
- [Modern enhancements](modern-enhancements.md)
