# Principles and Boundaries

## Dependency rule

Code dependencies point inward:

- Domain <- Application <- Infrastructure

Domain and application layers must not import Eloquent or framework persistence APIs.

## Responsibility split

- **Domain**: entities, value objects, invariants, domain services.
- **Application**: use-case orchestration and transaction policy.
- **Port interfaces**: persistence and external interaction contracts.
- **Adapters**: concrete Eloquent/SQL/cache/search implementations.

## SOLID in hexagonal DAL

### Single Responsibility

- Each port expresses one coherent capability.
- Each adapter implements one port family.

### Open/Closed

- Add new adapters without changing domain/application code.

### Liskov Substitution

- Adapter substitution must preserve domain-visible behavior.

### Interface Segregation

- Separate command/write ports from query/read ports.

### Dependency Inversion

- Application depends on ports, not adapter classes.

## Port design rules

- Keep ports small, explicit, and use-case oriented.
- Specify error contract and consistency expectations.
- Use DTO/VO for stable inputs and outputs.

## Packaging suggestion

- `app/Domain/<Context>/...`
- `app/Application/<Context>/UseCases/...`
- `app/Application/<Context>/Ports/...`
- `app/Infrastructure/Persistence/Eloquent/...`

## Decision rules

Create a new port when:

- capability changes independently from existing port contracts,
- adapter variability is expected.

Create a new adapter when:

- infrastructure implementation differs while contract stays stable.
