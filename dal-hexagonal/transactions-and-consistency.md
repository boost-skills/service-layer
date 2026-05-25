# Transactions and Consistency

## Consistency model

- Keep aggregate consistency in one transaction boundary per command use case.
- Use outbox for reliable cross-boundary integration events.
- Use saga/process manager for multi-step distributed workflows.

## Transaction boundary policy

- Application use case opens/closes transaction.
- Port operations inside use case are transactional when needed.
- Adapters must not open hidden nested transactions without clear policy.

## Outbox and messaging policy

- Persist domain state and outbox record atomically.
- Publish asynchronously with retry/backoff.
- Assume at-least-once delivery and enforce idempotent consumers.

## Concurrency policy

- Prefer optimistic concurrency for high-contention aggregates.
- Use explicit locks only when business rule requires strict serialization.

## Error semantics

- Domain errors are non-retryable business failures.
- Technical transient errors are retryable with bounded backoff.
- Technical permanent errors escalate and require operator action.

## Definition of done checklist

- [ ] Transaction boundary belongs to application layer.
- [ ] Cross-boundary side effects use outbox/reliable delivery.
- [ ] Idempotency strategy documented and tested.
- [ ] Concurrency strategy fits aggregate behavior.
