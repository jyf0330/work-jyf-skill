# AGENTS.md Template

Use this template when `jyf init` needs to create or update a project's `AGENTS.md`.

```markdown
# AGENTS.md

Agents working in this repo follow the rules below.

## Project context

- Project path: <absolute project root>
- Project type: <web / CLI / library / mobile / other>
- Primary tech stack: <language / framework / database>

## Workflow: Spec Kit

All development follows the Spec-Driven Development workflow:

1. `/speckit-constitution` — Project principles and governance
2. `/speckit-specify` — Feature specification with user stories and requirements
3. `/speckit-clarify` — Optional: resolve ambiguities before planning
4. `/speckit-plan` — Technical implementation plan
5. `/speckit-tasks` — Ordered, actionable task breakdown
6. `/speckit-implement` — Execute tasks and generate code

## BDD gate

- If `**/BDD-待审核.md` exists anywhere in the repo, implementation is BLOCKED.
- Only human reviewer renames `BDD-待审核.md` → `BDD-已通过.md`.
- Once renamed, the gate is cleared and implementation can proceed.
- While the gate is closed: write or update tests only, do not write implementation code.

## Delivery gates

- `implementation-subagent-template.md`: For multi-module parallel implementation
- `manual-acceptance-template.md`: For human operation verification
- `tester-prompt-template.md`: For automated verification following acceptance doc
- `delivery-gate-ledger-template.md`: Audit trail across all gates

## Quality overlay (UI projects only)

- `/impeccable teach` — Generate DESIGN.md from design context (before spec/plan)
- `/impeccable audit` — Technical quality check (after implement)
- `/impeccable critique` — UX review (after implement)
- `/impeccable polish` — Final design alignment (before delivery)
- Non-UI projects skip quality overlay.

## Rules

- No implementation code before spec approval.
- No implementation code while BDD gate is closed.
- Read existing documentation before proposing changes.
- Commit messages: `<type>: <description>`.
- Do not fabricate information not present in source documents.
- Do not access external sites beyond the project's declared data sources.
```

Note: When updating an existing `AGENTS.md`, preserve any project-specific sections the user has added and only update the template-managed sections.
