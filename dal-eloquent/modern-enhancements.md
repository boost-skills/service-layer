# Modern Enhancements

## High-impact upgrades

1. **Model strictness policy** with environment-aware guardrails.
2. **Custom Eloquent builders** for reusable query semantics.
3. **CQRS-lite read services** for report/search endpoints.
4. **Transactional outbox** for critical integration events.
5. **Performance budgets** with query count and p95 latency targets.
6. **Static analysis** via Larastan rules for model misuse.

## How to strengthen this skill further

- Add a project baseline for allowed relation loading patterns.
- Add profile-first playbook using Telescope/Debugbar in non-production.
- Add auto-fail checks for N+1 in CI on selected features.
- Add guide for progressive extraction from fat models to services/query objects.

## Migration guidance

### Eloquent-first -> Repository+Query+DTO

- Start where query object complexity exceeds readable scopes.
- Keep simple CRUD on models; extract only unstable/hot paths first.

### Eloquent-first -> Hexagonal

- Introduce domain ports around one critical aggregate.
- Wrap existing Eloquent usage inside adapter classes.
- Increase adoption incrementally per bounded context.
