# Principles and Boundaries

## Architecture intent

This variation separates write and read concerns:

- **Repository ports** own write-side persistence operations.
- **Query objects** own read-side filtering/projection logic.
- **DTO/VO** enforce typed contracts across layers.

## Responsibility split

- **Controller/Handler**: validate/authorize/map IO only.
- **Service (use case)**: orchestrate business flow.
- **Repository interface**: persistence behavior needed by use case.
- **Repository adapter**: Eloquent/SQL implementation details.
- **Query object**: optimized read model query and projection.

## SOLID application

### Single Responsibility

- One repository interface per aggregate or use-case cluster.
- One query object per read scenario.

### Open/Closed

- Extend behavior by adding query objects or adapter implementations.
- Avoid editing giant repository classes for every new filter.

### Liskov Substitution

- All repository implementations keep the same transactional and error guarantees.

### Interface Segregation

- Small ports: `CreateOrderRepository`, not `OrderRepositoryEverything`.

### Dependency Inversion

- Services depend on repository/query interfaces.
- Infrastructure adapters are bound in providers.

## Naming and packaging

- `app/Domain/<Context>/Contracts/Repositories/*Repository.php`
- `app/Domain/<Context>/Queries/*Query.php`
- `app/Domain/<Context>/DTO/*Data.php`
- `app/Infrastructure/Persistence/Eloquent/*Repository.php`

## Decision rules

Use a repository method when:

- operation mutates aggregate state,
- operation must apply invariants and concurrency checks.

Use a query object when:

- operation is read-only with dynamic filters,
- output shape differs from aggregate entity,
- SQL optimization (joins/window functions) is expected.
