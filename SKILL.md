---
name: service-layer
description: "Design and implement a robust Laravel service layer with clear boundaries, SOLID principles, transaction safety, testability, and maintainable architecture. Use when creating or refactoring business logic in controllers, jobs, listeners, commands, or domain workflows."
license: MIT
metadata:
  author: team
---

# Service Layer for Laravel

Use this skill when business logic grows beyond trivial CRUD or when a workflow is reused across multiple entry points.

## Outcome

Produce code where:

- controllers/handlers stay thin,
- services own one use case each,
- dependencies are explicit and replaceable,
- transactions and side effects are safe,
- behavior is testable at unit and feature levels.

## Quick Decision Rule

Create a service when one or more is true:

- flow spans multiple models/tables,
- logic is reused from HTTP + jobs + commands/listeners,
- operation needs transaction and side-effect ordering,
- business rules are too complex for model/controller methods.

Skip service extraction for obvious one-line CRUD that is already clear.

## Core Workflow

1. Name one concrete use case (`VerbNounService`).
2. Define input/output contracts (DTO/result/entity).
3. Inject dependencies by interface where possible.
4. Implement orchestration in a single `handle()` method.
5. Apply transaction boundaries and after-commit side effects.
6. Keep transport concerns out of service (`Request`, `Response`).
7. Cover happy path + key failure paths with tests.

## Definition of Done

A service-layer change is complete only if:

- service owns business orchestration for one use case,
- transaction boundaries are explicit where needed,
- domain and infrastructure failures are handled intentionally,
- no HTTP/transport concerns leak into service,
- tests cover happy path and critical failure scenarios.

## Additional Resources

Read only what is needed for the current task:

- [Principles and boundaries](principles.md)
- [Transactions and side effects](transactions-and-side-effects.md)
- [Testing matrix](testing-matrix.md)
- [Anti-patterns to reject](anti-patterns.md)
- [Service templates and examples](examples.md)
- [Refactoring playbook](refactoring-playbook.md)
