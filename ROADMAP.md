# Roadmap

## Purpose
This document captures the evolution of your system and provides a shared planning format for AI-assisted development.

The goal is to help you:
- Break work into milestones.
- Track risks early.
- Ensure acceptance criteria are explicit and testable.

## Planning Format (Recommended)
### Milestones
Each milestone should include:
- Goal (what user value it delivers)
- Scope (features and what is explicitly not included)
- Dependencies (other features/tech that must exist first)
- Acceptance criteria (verifiable checklist)

### Backlog
The backlog stores ideas and tasks not scheduled in a milestone yet. Keep backlog items small:
- One user-visible behavior per item when possible.
- Link to relevant docs (endpoints, pages, data models) if known.

## AI Planning Rules
When asked to create or update a roadmap, the assistant must:
1. Identify the dominant risks first (data, compatibility, security, correctness).
2. Split work so each step:
   - includes verification,
   - changes only one primary slice of behavior,
   - can be reviewed and rolled back.
3. Provide tradeoffs when there are multiple ways to implement the same milestone.

## Acceptance Criteria Template
For each feature task, include:
- Expected behavior (what the user sees/does)
- Backend expectations (endpoints, status codes, JSON shape)
- Frontend expectations (state updates, error messaging)
- Verification steps (how to test manually or via scripts)

## Risk Register (Optional but Recommended)
Track risks as:
- Risk description
- Likelihood (Low/Med/High)
- Impact (Low/Med/High)
- Mitigation plan
- Trigger condition (what observation would indicate the risk is real)

