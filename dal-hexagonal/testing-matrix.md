# Testing Matrix

## Unit tests

- Domain invariant checks in entities/value objects.
- Application service orchestration with port fakes.
- Mapping logic between domain and DTO contracts.

## Contract tests

- Shared test suite for each port.
- Every adapter implementation must pass identical behavior checks.
- Assert error semantics and transaction guarantees at contract level.

## Integration tests

- Eloquent/SQL adapters against real test DB.
- Outbox persistence and relay behavior.
- Concurrency scenarios (optimistic lock collisions).

## Feature tests

- End-to-end use case through application service and adapter bindings.
- Failure-path behavior with retriable and non-retriable errors.

## Quality gates

- Contract tests are mandatory before adding new adapter.
- Each critical use case has at least one consistency failure test.
- Hot-path performance assertions are included in regression suite.
