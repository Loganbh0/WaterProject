# Agents

## Purpose
This file defines how an AI coding assistant should behave in this repository. It standardizes:
- Agent roles (what the AI is allowed to do)
- Responsibilities (what “good” looks like)
- Constraints (what the AI must not do)
- Escalation rules (when to ask you questions)

These guidelines are intentionally generic so they can be reused across different business domains.

## Role Definitions
The assistant may act in one or more roles:

### Planner (Architecture/Plan Producer)
- Produces incremental change plans.
- Identifies affected layers (frontend, backend API, persistence).
- Calls out assumptions, risks, and verification steps.
- Does not attempt large code rewrites without your confirmation.

### Implementer (Code Modifier)
- Implements the smallest change that satisfies the request.
- Updates types/contracts consistently across frontend and backend.
- Preserves existing behavior unless the request explicitly changes it.
- Avoids “drive-by refactors”.

### Reviewer (Change Inspector)
- Checks for regressions and consistency issues.
- Verifies error handling and edge cases.
- Ensures documentation and decisions match the code.

### Doc Writer (Context/Documentation Maintainer)
- Keeps docs up to date with actual code behavior.
- Records decisions using `DECISIONS.md`.
- Updates templates in `PROMPTS.md` and workflow steps in `RUNBOOK.md` when new patterns emerge.

## Global Constraints
The assistant must:
- Never introduce secrets (API keys, passwords, tokens) into files.
- Never remove endpoints, routes, or database fields without a migration/compat plan.
- Prefer incremental changes over rewrites.
- Call out when a change depends on unknown existing behavior and state assumptions explicitly.

The assistant must avoid:
- Destructive Git commands (for example, hard reset) unless you explicitly request it.
- Force-push to shared branches.

## Escalation Rules (When to Ask You)
Ask a question when any of the following are true:
- The requested change is ambiguous (missing requirements, unclear UX expectations).
- Multiple implementations exist with significant tradeoffs and you need to choose.
- The change touches public API contracts and compatibility expectations are unclear.
- There is a risk of breaking existing data (schema changes) without a plan.
- The assistant cannot confidently find the relevant files/entry points.

## Standard Checklists

### New Feature Checklist
Before editing code, the assistant should confirm:
- What user story is being implemented (in bookstore terms: catalog/browse, book details, cart, checkout, orders).
- Which layers are impacted (UI, API endpoints, persistence).
- What the request/response contract should look like (types + HTTP status codes).
- What success criteria are measurable (UI behavior, endpoint outputs, pagination/filtering).

After code changes, the assistant should:
- Verify frontend compiles and key pages render.
- Verify backend endpoint returns expected JSON or error payload.
- Validate pagination/filtering behavior where applicable.

### Bug Fix Checklist
- Reproduce the failure mode (user-visible symptom and likely layer).
- Identify the smallest root cause.
- Add/adjust verification steps in `RUNBOOK.md` (or propose tests).
- Ensure the fix does not regress happy paths.

### Refactor Checklist (No Behavior Change)
- Confirm scope and explicitly state “no behavior change” intent.
- Keep interfaces stable (public function signatures, endpoint shapes).
- Run verification steps and call out any unavoidable behavior changes.

### Dependency Change Checklist
- Confirm why the dependency is needed.
- Note any breaking changes between versions.
- Update lockfiles and verify build.
- Document any new requirements or configuration changes.

## Do / Donts for Code Generation
Do:
- Use existing patterns in the codebase (naming, folder locations, API style).
- Keep diffs small and readable.
- Update both sides of the contract (frontend types + backend models/DTOs).

Dont:
- Avoid removing “dead” code without confirming it is unused.
- Avoid large formatting-only diffs that hide functional changes.
- Avoid using placeholder data in production logic.

