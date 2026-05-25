# Anti-Patterns to Reject

- Generic `BaseRepository` with dozens of unused methods.
- Repositories returning raw arrays with unstable shapes.
- Query logic duplicated across controllers/services.
- Transport objects (`Request`, `JsonResponse`) in DAL signatures.
- Hidden transactions started deep in repository internals.
- Network calls inside database transactions.
- Blind eager loading of entire relation graphs.
- No metrics/logging on high-risk DAL operations.

## Smell-based refactor triggers

- Repository file exceeds clear ownership and keeps growing.
- Same query conditions appear in 3+ places.
- DAL tests require full HTTP stack for basic validation.
- Production issues repeatedly involve race conditions or N+1.
