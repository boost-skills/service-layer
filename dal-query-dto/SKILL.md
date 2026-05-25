---
name: dal-query-dto
description: Design and implement a Laravel data access layer using Repository, Query Objects, and DTO/Value Objects with SOLID boundaries, transaction safety, and high testability. Use when domain logic needs stable persistence contracts, complex reads, or multi-source orchestration.
license: MIT
metadata:
  author: team
---

# Data Access Layer: Repository + Query Objects + DTO

Use this skill when Eloquent models alone no longer provide a clear and stable boundary for persistence-heavy use cases.

## Outcome

Produce DAL code where:

- write operations are isolated behind repository contracts,
- read operations are explicit query objects with clear inputs,
- service layer depends on abstractions, not storage details,
- transactions and side effects are predictable and safe,
- behavior is measurable and covered by tests.

## Quick Decision Rule

Choose this style when one or more are true:

- many complex filters/sorts/projections are repeated across features,
- query logic starts leaking into controllers/services,
- use case needs to switch between SQL, search, cache, or external storage,
- you need deterministic DAL contracts for long-lived business workflows.

Prefer Eloquent-first if logic is simple CRUD and query complexity is low.

## Core Workflow

1. Define use case boundary in the service layer.
2. Create focused repository port for write model behavior.
3. Model complex read scenarios as dedicated query objects.
4. Use typed DTO/VO for input and output contracts.
5. Add explicit transaction boundary and after-commit side effects.
6. Add integration tests for repositories and query objects.
7. Verify performance budget for hot queries.

## Definition of Done

A DAL change is complete only if:

- repository interfaces are use-case-oriented and not generic CRUD dumps,
- query objects own read concerns and return explicit typed shapes,
- side effects are after-commit or outbox-driven when consistency matters,
- no transport concerns leak into DAL contracts,
- tests cover happy path, domain rule failures, and query edge cases,
- observability exists for critical operations.

## Additional Resources

Read only what is needed for the current task:

- [Principles and boundaries](principles.md)
- [Transactions and consistency](transactions-and-consistency.md)
- [Testing matrix](testing-matrix.md)
- [Anti-patterns to reject](anti-patterns.md)
- [Examples and templates](examples.md)
- [Modern enhancements](modern-enhancements.md)
