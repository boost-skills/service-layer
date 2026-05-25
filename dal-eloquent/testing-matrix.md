# Testing Matrix

## Unit tests

- Custom scope behavior and filter composition.
- DTO/resource mapping logic for query outputs.
- Domain rule checks in service orchestration.

## Integration tests

- Eloquent model persistence behavior.
- Query builder/scopes with realistic DB fixtures.
- Transaction rollback behavior for failures.

## Feature tests

- Full request-to-persistence workflow.
- Permission + validation + DAL interaction.

## Performance assertions

- Query count limits for critical endpoints.
- N+1 detection for relation-heavy views.
- Pagination correctness under large datasets.

## Quality gates

- One happy + one failure path per use case.
- Regression test for each DAL production incident.
- Coverage for strict mode guardrails where relevant.
