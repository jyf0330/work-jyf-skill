---
name: jyf
description: Spec Kit 路由器 + 交付门禁。识别用户意图并路由到正确的 spec-kit 入口，强制 BDD 门禁，不重复实现 spec-kit 已有逻辑。
---

# JYF — Spec Kit 路由 + 交付门禁

`jyf` 只做两件事：**路由** 和 **门禁**。不维护独立的规格、计划、任务、实现、测试逻辑。

---

## 路由表

| 用户意图 | 路由目标 | 前置条件 |
|---------|---------|---------|
| spec / 规格 / 需求 / 定义 | `/speckit-specify` | constitution 存在 |
| plan / 方案 / 设计 / 架构 | `/speckit-plan` | spec.md 存在 |
| tasks / 任务 / 拆解 | `/speckit-tasks` | plan.md 存在 |
| clarify / 澄清 / 歧义 | `/speckit-clarify` | spec.md 存在 |
| analyze / 分析 / 检查 | `/speckit-analyze` | tasks.md 存在 |
| implement / 实现 / 写代码 | `/speckit-implement` | **BDD 门禁已通过** |
| test / 测试 / 验收 | 交付门禁流程 | 实现代码存在 |
| init / 初始化 | git init → AGENTS.md → `/speckit-constitution` | — |

路由不到时只说明需要 Spec Kit 接手，不展开第二套流程。

---

## BDD 门禁规则

```
BDD-待审核.md 存在 → 禁止写任何代码（含测试），只输出 BDD 或等待审核。
BDD 文件重命名为 BDD-已通过.md → 门禁解除 → 允许路由到 implement。
```

Agent 自动扫描 `**/BDD-待审核.md` 判断门禁状态。

---

## 文档基线检查

路由到实现类入口前，确认：`AGENTS.md` + 至少一份 BDD / spec / plan / tasks。

不足时先路由到文档补齐（使用 `references/` 模板），不让 agent 没文档猜着干活。

---

## 交付门禁流程

按顺序使用 references 模板：

| 阶段 | 模板 | 触发条件 |
|------|------|---------|
| 实现子线程 | `implementation-subagent-template.md` | 需多线程并行实现不同模块 |
| 人工验收 | `manual-acceptance-template.md` | 功能可运行、需真人操作验收 |
| 测试代理 | `tester-prompt-template.md` | 验收文档就绪、需自动化按文档验证 |
| 门禁账本 | `delivery-gate-ledger-template.md` | 贯穿全流程，每个 gate 变更时更新 |

验证方式根据项目类型自动适配：浏览器操作 / CLI 命令 / API 请求 / 文件输出检查，不强制假设 Web 项目。

---

## 额外约束

- 初始化：先确认 git 仓库，再写 `AGENTS.md`。
- 文档基线不足时优先补文档，再进入执行流。
- 优先用 `references/` 模板补齐文档，不临时自造格式。
- karpathy-guidelines：遵循 [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills/tree/main) 四原则。
- 不在这个 skill 里维护独立的项目规范或测试策略。
