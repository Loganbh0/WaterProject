# Decisions (ADR)

## Purpose
This file records important decisions so future work (including AI-assisted changes) can:
- Understand why choices were made
- Avoid repeating rejected alternatives
- Predict impact of future changes

Treat this as an append-only history. If you need to revise a decision, add a new entry referencing the superseded one.

## When to Add a Decision
Add an entry when a change introduces one or more of:
- A new or revised architecture pattern
- An API contract change with compatibility implications
- A security/reliability tradeoff
- A data model change that affects existing data
- A dependency/tooling choice that affects builds or runtime behavior

## ADR Template
Use the following format per decision:

### Title
YYYY-MM-DD - Short summary (for example: `2026-03-25 - Add cart pagination`)

#### Status
- Proposed | Accepted | Rejected

#### Context
What problem are we solving? What constraints exist (time, compatibility, performance, security)?

#### Decision
What did we choose and what is the exact rule/approach going forward?

#### Alternatives Considered
List other plausible approaches and why each was not chosen.

#### Consequences
Pros (benefits) and cons (downsides), including operational impact.

#### Rollback Strategy
What is the safe rollback path if this choice causes issues? Reference files/endpoints that would need to revert.

#### References
Optional: links to relevant issues/PRs or important file paths.

## How the Assistant Should Reference Decisions
When implementing a feature that relies on a decision, the assistant should:
- Mention the relevant decision title in the response
- Link or reference impacted files and contracts
- Ensure the implementation matches the decision rules

