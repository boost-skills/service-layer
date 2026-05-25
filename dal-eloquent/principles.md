# Principles and Boundaries

## Architecture intent

Eloquent is the default DAL tool. Additional abstraction is introduced only for clear and recurring complexity.

## Responsibility split

- **Controller/Handler**: input, auth, response mapping.
- **Service**: business orchestration and transaction boundary.
- **Eloquent model/scopes/custom builder**: persistence behavior.
- **Query service**: complex report-like reads and projections.

## SOLID in Eloquent-first

### Single Responsibility

- Services should represent one use case.
- Models should avoid becoming god objects; move heavy orchestration to services.

### Open/Closed

- Add scopes/builders/query services instead of editing one giant query chain everywhere.

### Liskov Substitution

- If multiple model adapters exist, preserve loading and error semantics.

### Interface Segregation

- Introduce interfaces only for parts that truly vary (external stores, search engines, billing).

### Dependency Inversion

- Keep services independent of transport and infrastructure concerns.

## Strict mode policy

Enable strict guards in non-production:

- prevent lazy loading violations,
- prevent silently discarded attributes,
- prevent missing attribute access.

Use explicit eager loading strategy on critical paths.

## Decision rules

Stay Eloquent-first when:

- query remains understandable in model scope/builder,
- no cross-store abstraction is required.

Extract repository/query service when:

- query is reused across bounded contexts,
- SQL optimization or projection needs exceed model readability.
