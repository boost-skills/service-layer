# Boost Skills (PHP)

This repository contains a set of skills for AI agents that help produce higher-quality Laravel/PHP code.

## How to use

- Choose the skill that matches your task.
- Open its `README.md` to understand the structure.
- Start with `SKILL.md` inside the selected folder.

## Skills list

- `service-layer` - designing the service layer for business logic.  
  [Open README](service-layer/README.md)

- `dal-query-dto` - DAL approach using Repository + Query Objects + DTO.  
  [Open README](dal-query-dto/README.md)

- `dal-eloquent` - pragmatic Eloquent-first DAL approach.  
  [Open README](dal-eloquent/README.md)

- `dal-hexagonal` - strict Hexagonal (Ports & Adapters) DAL approach.  
  [Open README](dal-hexagonal/README.md)

- `data-access-layer-repo-query-dto` - extended DAL version: Repository + Query + DTO.  
  [Open README](data-access-layer-repo-query-dto/README.md)

- `data-access-layer-eloquent-first` - extended DAL version: Eloquent-first.  
  [Open README](data-access-layer-eloquent-first/README.md)

- `data-access-layer-hexagonal` - extended DAL version: Hexagonal.  
  [Open README](data-access-layer-hexagonal/README.md)

## DAL skill selection tips

- Use `dal-eloquent` for fast CRUD/LOB tasks.
- Use `dal-query-dto` for complex queries and explicit contracts.
- Use `dal-hexagonal` for long-lived complex domains and replaceable infrastructure.
