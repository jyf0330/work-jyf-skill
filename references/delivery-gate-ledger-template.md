# Delivery Gate Ledger Template

用于让 JYF 交付证据在上下文丢失、重测和交接时保持可审计。

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

## Gate 与 JYF 阶段对应

| Gate | 对应 JYF 阶段 |
| --- | --- |
| Real program behavior implemented | implement |
| Main-thread review/integration complete | implement / delivery-ledger |
| Fresh automated verification passed | implement / tester |
| Human operation verification document exists | acceptance-doc |
| Tester followed document and passed | tester |

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
