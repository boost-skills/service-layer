# Anti-Patterns to Reject

- Introducing repository interfaces for trivial one-query CRUD.
- Business orchestration directly in models/controllers.
- Repeating long query chains across services/controllers.
- Ignoring N+1 and relying on accidental eager loading.
- Massive `with()` graphs loaded blindly on every endpoint.
- Using transactions around external HTTP/queue calls.
- Returning untyped mixed arrays from DAL helpers.

## Smell-based refactor triggers

- One Eloquent model owns unrelated domain concerns.
- Same complex query appears in multiple endpoints.
- Performance regressions recur due to missing loading strategy.
- Team spends more time debugging query side effects than adding features.
