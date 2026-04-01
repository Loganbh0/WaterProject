# Structure

## Goal
This file defines a repository structure and working conventions optimized for collaboration between a human developer and an AI coding assistant.

Use it to answer questions like:
- Where should a change go?
- What naming/folder conventions should be followed?
- How can the assistant avoid unintended edits?

## Repo Layout Template
Use this generic layout pattern (adapt names as needed for the bookstore domain):

- `frontend/`
  - UI entry point and routing.
  - Page components (route-level).
  - Reusable components.
  - Context/state management.
  - API client utilities (or a small API layer).
  - Types and shared models for frontend.
- `backend/`
  - API entry point (`Program`-style) and middleware configuration.
  - Controllers/endpoints.
  - Data/persistence layer (DbContext, repositories if present).
  - Domain models / DTOs (where appropriate).
  - Configuration (connection strings, CORS, etc.).
- Root-level docs
  - This set of AI-context Markdown files.
  - Any README or local run instructions.

## File Ownership Guidelines
When the assistant is asked to implement a feature, it should follow:

### Frontend changes go in `frontend/`
- UI or UX changes: route pages, components, CSS.
- State changes: context/store modules and their consumers.
- API integration: API client functions/utilities.
- Data model updates: frontend `types/` or DTO equivalents used by the UI.

### Backend changes go in `backend/`
- New endpoints, controller logic, request/response models.
- Validation changes and error response shape.
- Persistence changes: schema/model updates and migrations.

### Keep cross-layer changes consistent
If an endpoint contract changes (request/response shape, query params):
- Update backend first (or alongside).
- Update frontend API client and types immediately after.

## Naming and Folder Conventions
Follow these conventions to keep AI-generated code predictable:

Frontend:
- `src/pages/` for route-level pages.
- `src/components/` for reusable UI components.
- `src/context/` for global/shared state.
- `src/types/` for shared TypeScript types used across the UI.
- Prefer `PascalCase` for component/type names.
- Prefer `camelCase` for functions and variables.
- Keep CSS names stable and scoped by component where possible.

Backend:
- Controllers should be named by resource/domain (for example, `BooksController`, `CartController`, `OrdersController`).
- Route attributes should be consistent and readable.
- DTO/model names should clearly indicate intent (request vs response).
- Keep public APIs self-explanatory and avoid “mystery” fields.

## Change Safety Rules
The assistant must treat changes as potentially risky unless proven otherwise:
- Prefer minimal diffs (small focused commits/patches).
- If the change touches API contracts, verify end-to-end:
  - Backend endpoint works.
  - Frontend calls it with correct params/body.
  - UI renders expected state and error states.
- If tests exist:
  - Run them (or propose exactly how to run them).
- If tests do not exist:
  - Add lightweight verification steps in `RUNBOOK.md` (or in the response).
- Never assume an implementation detail; state assumptions explicitly.

## “No Surprises” Editing Rules
When generating code:
- Do not delete files unless asked.
- Do not remove existing routes/endpoints without documenting the migration/compat plan.
- Avoid broad refactors as a first step unless requested.

