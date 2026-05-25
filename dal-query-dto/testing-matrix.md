# Testing Matrix

## Test levels

### Unit tests

- Query object filter composition.
- DTO mapping and validation rules.
- Domain-specific repository contract behavior via fakes.

### Integration tests

- Real repository adapters against test database.
- Query object SQL behavior with realistic fixtures.
- Transaction rollback and concurrency edge cases.

### Feature tests

- End-to-end use case path through service and DAL.
- Error mapping to API/CLI response contracts.

## Mandatory scenarios

- Happy path for each DAL operation.
- Zero-result and pagination boundaries for read queries.
- Duplicate request/idempotency behavior.
- Retry-safe processing for outbox/event consumers.

## Quality gates

- Cover at least one negative path per use case.
- Assert query count or loading strategy for hot paths.
- Add regression tests for every production DAL bug.
