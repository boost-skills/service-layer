# Service Layer Skill

This skill helps AI agents design and implement a clean Laravel service layer using SOLID principles, safe transaction boundaries, and test-first thinking.

## What this skill is for

Use this skill when business logic is non-trivial, reused across multiple entry points, or requires strict consistency and clear architecture boundaries.

## File map

- `SKILL.md` - compact entrypoint with workflow and definition of done.
- `principles.md` - service-layer boundaries, SOLID, contracts, naming.
- `transactions-and-side-effects.md` - atomicity, idempotency, failure handling.
- `testing-matrix.md` - required test coverage for service-oriented changes.
- `anti-patterns.md` - patterns to reject during implementation/review.
- `examples.md` - service, DTO, contract, controller, provider templates.
- `refactoring-playbook.md` - safe extraction path from fat controllers/jobs.

## How to use

1. Start with `SKILL.md`.
2. Read only the referenced document needed for the current task.
3. Implement one use case per service and verify with targeted tests.

## Scope

This skill focuses on backend Laravel application logic and service-layer architecture. It is not a frontend/UI skill.
