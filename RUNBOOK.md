# Runbook

## Purpose
This runbook defines a repeatable workflow for AI-assisted development in this repository. Use it for:
- New features
- Bug fixes
- Refactors
- Architecture changes

## Workflow (End-to-End)
### Step 1: Clarify the request
Before any code change, identify:
- What the user is trying to do (bookstore scenario).
- What outcome is expected (UI behavior, endpoint behavior, data updates).
- What constraints apply (time, backwards compatibility, UX requirements).

If requirements are ambiguous, ask targeted questions before proceeding.

### Step 2: Map the change to layers
Determine impacted layers:
- Frontend UI: pages/components/context/types
- Backend API: controller endpoints, request/response models
- Persistence: database tables/schema/migrations

List them explicitly in the response (or in the plan).

### Step 3: Check existing patterns
The assistant should:
- Search for similar endpoints/pages/components already implemented.
- Reuse naming conventions and structure.
- Avoid adding new patterns unless necessary.

### Step 4: Make the smallest safe change
Implement changes incrementally:
- Backend contract changes first (if any).
- Update frontend client/types.
- Update UI behavior and state management.

Avoid refactors that are not required to complete the user story.

### Step 5: Update documentation and decisions
If behavior changes or introduces a tradeoff:
- Add a decision to `DECISIONS.md`.
- Update relevant sections in `ARCHITECTURE.md` or `STRUCTURE.md` if the workflow or architecture constraints changed.

### Step 6: Verify
Use a verification checklist in every implementation:
- Frontend compiles and key routes render.
- Backend endpoints return expected JSON and status codes.
- Error paths return consistent payloads.
- Pagination/filtering works for list endpoints (when applicable).

If tests exist, run them; if not, run a small manual smoke test plan.

### Step 7: Rollback plan (always consider)
For risky changes:
- Document how to revert (which files/commits to roll back).
- Keep changes small so revert is feasible.

## Common Pitfalls
- Changing endpoint contracts without updating frontend types.
- Returning inconsistent error shapes across controllers.
- Breaking pagination/filtering by applying filters after `Skip/Take`.
- Adding optimistic UI updates without correct error rollback behavior.
- Over-permissioned CORS configuration in security-sensitive scenarios.

## Fallback Strategy
If the assistant cannot locate the relevant code:
- Ask for file paths or routing/endpoint names.
- Propose a narrowed search approach (what to look for).
- Avoid “guess-and-edit” when contracts are involved.

