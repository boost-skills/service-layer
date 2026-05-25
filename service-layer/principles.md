# Principles and Boundaries

## Architecture Mental Model

Treat each feature as one use case:

1. Input enters the system (HTTP / CLI / Job / Event).
2. Validation and authorization happen before service invocation.
3. Service executes business orchestration.
4. Persistence happens atomically where required.
5. Side effects run at the correct lifecycle moment.
6. Caller maps output to transport format.

## Responsibility Split

- **Controller / Handler**: parse input, authorize, call service, map output.
- **Service**: business orchestration for one use case.
- **Domain model / Value object**: invariants and core behavior.
- **Repository / Gateway / Client**: storage and external IO boundaries.

## SOLID in Service Layer

### Single Responsibility

- One service class should represent one use case.
- Default to one public method: `handle()`.

### Open/Closed

- Extend via strategy classes, listeners, policies, and new implementations.
- Avoid massive branching for provider-specific behavior.

### Liskov Substitution

- Implementations of one contract must preserve behavior guarantees.

### Interface Segregation

- Use focused interfaces (`PaymentGateway`, `ImageProvider`).
- Avoid broad "do everything" contracts.

### Dependency Inversion

- Depend on abstractions in services.
- Bind implementations in service providers.
- Use constructor injection; avoid runtime container lookups in method bodies.

## Input / Output Contracts

- Prefer typed DTO input over raw arrays.
- Return explicit output type: entity, DTO, or result object.
- Throw specific domain exceptions for expected rule violations.
- Avoid mixed output contracts (`true|string|array`).

## Validation and Authorization Placement

- Validation: Form Requests for HTTP, dedicated validators for other entry points.
- Authorization: policy/gate before service invocation.
- Service enforces domain invariants independent of transport/user agent details.

Keep services transport-agnostic: no `Request` or `Response` in service signatures.

## Naming and Packaging

Recommended structure:

- `app/Services/<Domain>/<UseCase>Service.php`
- `app/Contracts/<Area>/<Contract>.php`
- `app/DataTransferObjects/<Area>/<Data>.php`
- `app/Exceptions/Domain/<Exception>.php`

Naming guidelines:

- Prefer use-case verbs (`PublishArticleService`, `SyncCatalogService`).
- Reject vague suffixes (`Helper`, `Manager`, `Processor`) unless strictly contextual.
