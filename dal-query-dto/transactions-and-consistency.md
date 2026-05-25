# Transactions and Consistency

## Transaction policy

- Wrap each write use case in one explicit `DB::transaction`.
- Keep transaction body small and deterministic.
- Avoid network IO inside active transaction.

## Side-effect ordering

1. Persist aggregate changes.
2. Persist outbox messages in the same transaction for critical integrations.
3. Publish/process async side effects after commit.

## Outbox guidance

Use transactional outbox when:

- event delivery must not be lost,
- downstream systems require reliable retries,
- you need auditability for dispatched integration events.

Expect at-least-once delivery and design consumers as idempotent.

## Concurrency and idempotency

- Use idempotency keys for create-like commands exposed to retries.
- Use optimistic locking/version checks on contention-prone aggregates.
- Implement dedup storage for reprocessed messages.

## Error taxonomy

- Domain rule violations: typed domain exceptions.
- Transient infrastructure errors: retryable errors with backoff.
- Permanent infrastructure errors: fail fast with clear diagnostics.

## Definition of done checklist

- [ ] Explicit transaction boundary exists for write operation.
- [ ] Side effects are after-commit or outbox-based.
- [ ] Retry policy and idempotency behavior are documented.
- [ ] Failure classes are mapped to expected handling.
