# Data Access Layer Skill: Hexagonal

This skill helps AI agents build a strict Ports-and-Adapters DAL in Laravel with clear domain isolation and adapter replaceability.

## File map

- `SKILL.md` - entrypoint with decision criteria.
- `principles.md` - port design and dependency direction rules.
- `transactions-and-consistency.md` - consistency model and outbox strategy.
- `testing-matrix.md` - contract/integration/feature testing requirements.
- `anti-patterns.md` - leakage and over-engineering smells.
- `examples.md` - practical port and adapter templates.
- `modern-enhancements.md` - current best practices and evolution paths.

## How to use

1. Model domain ports before infrastructure code.
2. Implement application services against ports only.
3. Add adapters and bind them at infrastructure edge.
4. Verify with contract and integration tests.

## Scope

Backend Laravel systems with high complexity, long lifespan, and strict architecture needs.
