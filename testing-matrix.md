# Testing Matrix

Every non-trivial service change requires programmatic tests.

## Minimum Scenario Coverage

1. Happy path.
2. Domain rule violation.
3. Infrastructure failure path (if external dependencies exist).
4. Transaction consistency (no partial writes on failure).
5. Idempotency or duplicate-submission behavior (if retries/replays are possible).

## Test Levels

### Unit Tests (Service Orchestration)

Use unit tests to verify:

- service calls dependencies in correct order,
- branching logic for domain rules,
- mapped exceptions and returned contract type.

Mock/fake only external boundaries (gateways, clients, repositories if needed).

### Feature/Integration Tests (Entry Point)

Use feature tests to verify:

- request -> validation/authorization -> service -> persistence -> response,
- proper status code and payload for expected failures,
- key side effects (events/jobs/notifications) are emitted or suppressed correctly.

## Assertions to Prefer

- explicit database assertions for atomicity checks,
- explicit assertion that failure path does not persist half-finished state,
- assertion that duplicate request path is stable and deterministic.

## Example Test Checklist for a New Service

- [ ] `test_it_completes_use_case_successfully`
- [ ] `test_it_rejects_invalid_business_state`
- [ ] `test_it_rolls_back_on_failure`
- [ ] `test_it_handles_external_provider_failure`
- [ ] `test_it_is_idempotent_for_duplicate_command`

## Common Testing Pitfalls

- only testing happy path,
- mocking too much and missing integration regressions,
- asserting response only without checking persistence invariants,
- skipping duplicate/retry scenario for async workflows.
