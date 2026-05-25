---
name: dal-eloquent
description: Build a pragmatic Laravel data access layer using Eloquent-first practices, strict model policies, and selective abstraction only where complexity exists. Use for CRUD-heavy products that still require SOLID boundaries, consistency, and predictable performance.
license: MIT
metadata:
  author: team
---

# Data Access Layer: Eloquent-first

Use this skill when the domain is mostly CRUD and Eloquent gives the best cost-to-value ratio.

## Outcome

Produce DAL code where:

- Eloquent remains the primary persistence interface,
- complex reads are isolated in query services/scopes,
- strict loading and attribute policies reduce runtime defects,
- transactions are explicit for multi-write use cases,
- abstractions are introduced only on real complexity.

## Quick Decision Rule

Choose this style when one or more are true:

- most features are standard create/read/update/delete,
- team velocity is harmed by excessive architectural layers,
- query complexity is moderate and can be handled by scopes/builders,
- portability across storage engines is not a hard requirement now.

Escalate to repository/hexagonal when business invariants and integrations outgrow direct model usage.

## Core Workflow

1. Keep controller thin and move orchestration to a service.
2. Use Eloquent model/scopes/custom builders for primary DAL behavior.
3. Extract query service only for complex read models.
4. Add explicit transactions for multi-aggregate writes.
5. Configure strict model policies in non-production environments.
6. Add tests for query behavior and loading strategy.
7. Track query count/latency for critical paths.

## Definition of Done

A DAL change is complete only if:

- Eloquent usage stays explicit and readable,
- no hidden N+1 is introduced,
- transactions and side effects are correctly ordered,
- complex queries are isolated and reusable,
- tests prove behavior under happy and failure paths,
- observability exists for hot DAL paths.

## Additional Resources

Read only what is needed for the current task:

- [Principles and boundaries](principles.md)
- [Transactions and consistency](transactions-and-consistency.md)
- [Testing matrix](testing-matrix.md)
- [Anti-patterns to reject](anti-patterns.md)
- [Examples and templates](examples.md)
- [Modern enhancements](modern-enhancements.md)
