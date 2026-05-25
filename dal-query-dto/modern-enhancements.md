# Modern Enhancements

## High-impact upgrades

1. **CQRS-lite**: keep writes in repositories, move expensive reads to tailored query services.
2. **Specification objects**: compose advanced filtering without repository bloat.
3. **Strict Eloquent policy**: prevent lazy loading and missing attribute access in non-production.
4. **Performance budgets**: define max query count and latency per critical use case.
5. **Static analysis gates**: enforce architecture boundaries with PHPStan/Larastan rules.
6. **Contract tests**: lock repository port behavior across adapter implementations.

## How to strengthen this skill further

- Add project-specific examples from real incidents and postmortems.
- Add benchmark templates for top 5 heaviest queries.
- Add migration playbook from generic repositories to query objects.
- Add observability cookbook (correlation-id, span names, error tags).
- Add forbidden dependency map to prevent domain-to-infra leakage.

## Migration guidance

### Eloquent-first -> Repository+Query+DTO

- Start from the most unstable and expensive query path.
- Extract one query object and one output DTO.
- Add repository port only for write-side invariants.

### Repository+Query+DTO -> Hexagonal

- Move repository interfaces into domain ports.
- Shift Eloquent implementations fully into infrastructure adapters.
- Add contract tests to guarantee port stability.
