# Transactions and Side Effects

## Core Rules

- Group state-changing DB operations in one transaction when atomicity is required.
- Keep transactions short to reduce lock contention.
- Avoid slow network calls inside long DB transactions.
- Ensure asynchronous side effects are dispatched after commit when consistency matters.
- Design retryable workflows to be idempotent.

## Safe Pattern

1. Validate input and permissions.
2. Open transaction.
3. Persist core domain state.
4. Persist integration metadata if needed.
5. Commit.
6. Dispatch async side effects (`after_commit` semantics when available).

## Idempotency Guidance

Use one or more:

- unique keys / unique DB constraints,
- idempotency token on command/request,
- upsert/conflict-aware writes,
- deduplication by business key.

Service behavior on duplicates should be explicit:

- return existing result, or
- throw dedicated domain exception.

## Failure Categories

1. **Domain failures**: business rule violations (e.g., insufficient balance).
2. **Infrastructure failures**: external provider timeout/failure.
3. **Unexpected failures**: unknown runtime/system errors.

Never swallow exceptions silently. Report unexpected failures with context.

## Laravel-Oriented Notes

- Use `DB::transaction()` for atomic writes.
- Queue/event side effects should respect post-commit semantics when required.
- If job dispatch happens inside transactions, ensure execution does not start before commit.

## Consistency Checklist

- [ ] No partial DB writes on service failure.
- [ ] Side effects are not emitted for rolled back operations.
- [ ] Duplicate submissions do not produce duplicate external actions.
- [ ] Retry strategy cannot corrupt business state.
