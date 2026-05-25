# Anti-Patterns to Reject

Reject implementations containing these patterns.

## Structural Anti-Patterns

- Fat controllers implementing business orchestration.
- One mega-service with many unrelated public methods.
- Static utility classes masquerading as service layer.
- Transport objects (`Request`, `Response`) in service signatures.

## Dependency Anti-Patterns

- Hidden runtime lookups (`app()`, global container pulls) inside service logic.
- Over-coupling service to concrete provider classes without contract boundary.
- Facade-heavy orchestration when constructor injection is clearer and testable.

## Transaction and Side-Effect Anti-Patterns

- Long transactions around unrelated concerns.
- Network calls that hold DB locks unnecessarily.
- Emitting irreversible side effects before transaction commit.
- Ignoring duplicate submission/retry semantics.

## Error Handling Anti-Patterns

- Silent catch of `\Throwable` without report/rethrow.
- Returning ambiguous primitives instead of typed result/exception.
- Mixing domain failure and infrastructure failure handling without distinction.

## Testing Anti-Patterns

- No failure-path tests.
- No atomicity assertions.
- No duplicate/retry scenario for async operations.

## Naming and Maintainability Anti-Patterns

- Vague service names (`DataManagerService`, `CommonHelperService`).
- Use cases spread across controller, model, and service simultaneously.
- Service methods with unclear contracts and hidden side effects.
