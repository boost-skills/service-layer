# Refactoring Playbook

Use this sequence to extract service layer from existing code without breaking behavior.

## Step-by-Step

1. Pick one concrete use case from controller/job/listener.
2. Freeze expected behavior with tests (or add missing baseline tests first).
3. Introduce typed input DTO for that use case.
4. Extract business orchestration into `<UseCase>Service::handle()`.
5. Move external integrations behind contracts/interfaces.
6. Add/adjust transaction boundary for atomic writes.
7. Ensure side effects run at correct lifecycle point.
8. Replace old inline logic with service call.
9. Run targeted tests and confirm no behavior regression.

## Safe Refactor Constraints

- Preserve API contract and response semantics.
- Preserve authorization and validation behavior.
- Preserve event/job dispatch semantics (timing matters).
- Do not mix unrelated use cases into one service during refactor.

## Incremental Strategy

Prefer multiple small refactors over one big rewrite:

- first extraction: keep output shape and exceptions unchanged,
- second pass: improve contracts/naming,
- third pass: optimize boundaries and performance.

## Readiness Checklist

- [ ] old inline workflow removed from entry point
- [ ] service has one clear use case
- [ ] dependencies are explicit
- [ ] atomicity and side-effect order are verified
- [ ] tests cover happy + failure + consistency paths
