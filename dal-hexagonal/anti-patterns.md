# Anti-Patterns to Reject

- Domain layer importing Eloquent, DB facade, or framework helpers.
- Ports exposing ORM-specific query builders.
- Adapter-specific exceptions leaking into application/domain layers.
- Giant generic repository interfaces crossing bounded contexts.
- Mixing read model concerns into write-side aggregate ports.
- Side effects dispatched before transaction commit.
- Contract changes without adapter-wide contract test updates.

## Smell-based refactor triggers

- Application service references adapter concrete class.
- Port methods keep expanding with unrelated use cases.
- Adapter swap requires domain/application changes.
- Same consistency bug reappears in integration boundaries.
