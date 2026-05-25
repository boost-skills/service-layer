# Modern Enhancements

## High-impact upgrades

1. **Contract test harness** auto-run for every adapter implementation.
2. **Read/write split (CQRS-lite)** with dedicated query adapters.
3. **Transactional outbox** with retry/backoff and dead-letter policy.
4. **Architecture linting** to enforce inward dependencies.
5. **Observability by design** with tracing around each port call.
6. **Performance budgets** for top command/query use cases.

## How to strengthen this skill further

- Add project-specific ADR templates for port evolution decisions.
- Add migration guide from legacy active-record style modules.
- Add standardized error taxonomy for all adapter failures.
- Add chaos testing recipes for retry/outbox resilience.
- Add package/module boundary checks in CI.

## Migration guidance

### Repository+Query+DTO -> Hexagonal

- Move interfaces from infrastructure namespace into application/domain ports.
- Keep existing implementation as first adapter.
- Introduce contract tests before adding second adapter.

### Eloquent-first -> Hexagonal

- Start with one critical bounded context only.
- Introduce ports around unstable integration boundaries first.
- Keep low-risk CRUD contexts in Eloquent-first mode until needed.
