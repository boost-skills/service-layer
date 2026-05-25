# Transactions and Consistency

## Transaction policy

- Use `DB::transaction` at service layer for multi-step writes.
- Keep writes atomic and side-effect free until commit.
- Keep transaction body short and free from external IO.

## Side-effect policy

- Use `afterCommit` event/listener/job behavior for non-critical async effects.
- Use transactional outbox for critical inter-service integration events.

## Idempotency and retries

- Assign idempotency key for retry-prone command endpoints.
- Ensure handlers can safely run twice.
- Store dedup metadata for event consumers.

## Consistency decision rules

- **Single DB, same use case**: plain transaction is enough.
- **Cross-service consistency required**: outbox + retry worker.
- **Long-running process**: use saga/process manager with compensations.

## Definition of done checklist

- [ ] Transaction scope is explicit and tested.
- [ ] Side-effect ordering is after-commit or outbox-backed.
- [ ] Idempotency behavior is defined for retried paths.
- [ ] Failure handling policy (retry vs fail-fast) is explicit.
