# Delivery Gate Ledger Template

Use this template to keep JYF completion evidence auditable across context loss, retests, and handoffs.

```markdown
# <feature/task> JYF Delivery Gate Ledger

## Task Identity

- Project path:
- Branch / commit:
- Timestamp:
- Latest user request:

## Source Scope

| Source | Path or reference | Used for | Notes |
| --- | --- | --- | --- |
| User request | <thread/current message> | Scope priority 1 |  |
| Project instructions | <AGENTS.md path> | Constraints |  |
| Product/BDD/GDD/plan | <path> | Expected behavior |  |
| Code/tests | <path(s)> | Current behavior |  |

## Gate Status

| Gate | Status | Evidence |
| --- | --- | --- |
| Real program behavior implemented | pending/pass/fail/blocked |  |
| Main-thread review/integration complete | pending/pass/fail/blocked |  |
| Fresh automated verification passed | pending/pass/fail/blocked | Command, result, pass count |
| Human operation verification document exists | pending/pass/fail/blocked | Document path |
| Tester followed document and passed | pending/pass/fail/blocked | Tester report summary |

## Implementation Evidence

- Changed files:
- Implemented behavior:
- Compatibility notes:
- Known non-goals:

## Automated Verification

- Command:
- Result:
- Pass count / relevant output:
- Not run / unavailable reason:

## Manual Verification Document

- Path:
- Covers:
- Does not cover:

## Tester Acceptance

- Tester identity/run:
- Verification method (browser / CLI / API / file):
- Entry point / launch command:
- Passed steps:
- Failed steps:
- Blockers:
- Evidence locations:
- Final conclusion:

## Retest Log

| Attempt | Reason | Fix made | Automated evidence | Tester conclusion |
| --- | --- | --- | --- | --- |
| 1 | Initial run |  |  |  |

## Remaining Risks

- 
```
