# Prompts

## Purpose
This file provides prompt templates your AI assistant should use to produce consistent, high-quality outputs in this repository.

It is written for AI context (not for end users). Treat it as an internal contract:
- The assistant should follow the template structure.
- The assistant should fill placeholders accurately.
- The assistant should include verification steps in every implementation/debugging response.

## Required Conventions
In every assistant response that proposes code changes:
- State assumptions explicitly.
- List touched layers (frontend, API, persistence).
- Include a verification checklist.
- Mention risks and how to mitigate them.

In every assistant response that proposes a new behavior:
- Describe the user-visible impact.
- Describe the API contract impact (if any).
- Describe the data/persistence impact (if any).

## Template: Implementation Request
Use this when the user asks for a new feature or endpoint:

### Assistant Response Format
1. Summary (1-3 sentences)
2. Assumptions
3. Plan (small steps, ordered)
4. Files/Layers to change
5. API Contract changes (if any)
6. Frontend/UI behavior changes (if any)
7. Verification checklist
8. Risks and mitigations

### Placeholders
- `BookstoreDomain`: catalog | book details | cart | checkout | orders | admin
- `AffectedEndpoints`: list route paths and methods
- `ResponseShapes`: describe JSON shape and error shape expectations

## Template: Debugging Request
Use this when the user reports a bug or failing behavior:

### Assistant Response Format
1. Observed symptoms (what is failing)
2. Most likely causes (ranked)
3. Diagnostic steps (what to inspect, in what order)
4. Proposed fix (smallest diff first)
5. Verification checklist
6. Rollback plan (how to revert if it worsens things)
7. Follow-ups (tests/logging improvements if needed)

### Diagnostic Rules
- Check frontend contract usage first (wrong params/types).
- Check backend validation and status codes next.
- Check persistence queries last (filter/pagination/relationships).

## Template: Refactor Proposal (No Behavior Change)
Use this when the user asks to improve structure without changing outputs:

### Assistant Response Format
1. What is being improved (readability, maintainability, duplication)
2. Confirmed non-goals (what must not change)
3. Expected invariants (contracts, endpoints, data shape)
4. Plan (incremental, safe steps)
5. Verification checklist
6. Risks (mostly around accidental behavior change)

## Template: Documentation Update
Use this when changes require doc updates:

### Assistant Response Format
1. What changed in the code (brief)
2. What doc file(s) must be updated (link to paths)
3. What sections to revise
4. Verification checklist (docs match reality)

## Template: Decision Record (ADR-style)
When adding a decision to `DECISIONS.md`:

### Required Fields
- Title
- Status (Proposed | Accepted | Rejected)
- Context (what problem is being solved)
- Decision (the chosen approach)
- Alternatives considered (and why they were not chosen)
- Consequences (pros/cons)
- Rollback strategy (how to revert safely)

## Verification Template
Every code change proposal should include a short checklist like:
- Frontend builds (`npm` scripts relevant to the project)
- Backend builds (`dotnet` build/run relevant commands)
- Manual smoke test:
  - open key page(s)
  - add an item to cart (if applicable)
  - call at least one updated endpoint
- Error path test:
  - provide invalid input and confirm status code + message

