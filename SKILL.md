---
name: jyf
description: Spec Kit 路由器 + 交付门禁。识别用户意图并路由到正确的 spec-kit 入口，强制 BDD 门禁，不重复实现 spec-kit 已有逻辑。
---

# JYF — Spec Kit 路由 + 交付门禁

`jyf` 只做两件事：**路由** 和 **门禁**。不维护独立的规格、计划、任务、实现、测试逻辑。

---

## 阶段流

```
init → specify/BDD → [clarify?] → plan → tasks → [BDD 通过?] → implement → acceptance-doc → tester → delivery-ledger PASS → 完成
```

每个阶段依赖前一阶段的交付物；jyf 在每次路由前先定位当前所在阶段。
BDD 文件应在 spec 阶段产出或同步更新；BDD 门禁只阻断 implement 路由，不阻断 clarify / plan / tasks。
clarify 触发条件：spec.md 中存在会影响方案、任务拆解、验收标准或实现边界的 `[NEEDS CLARIFICATION]` 标记时，先路由到 `/speckit-clarify`；无阻断性歧义时可跳过。

---

## 路由表

路由目标可以是 `/speckit-*` 命令，也可以是 JYF `references/` 模板；模板入口属于交付门禁，不伪装成 Spec Kit 命令。
`constitution` 指 Spec Kit 项目宪章，由 `/speckit-constitution` 创建或更新；具体文件名和路径以该入口的实际产物为准。

| 用户意图 | 路由目标 | 前置条件 | 前置不满足时 |
|---------|---------|----------|-------------|
| spec / 规格 / 需求 / 定义 | `/speckit-specify` | constitution 存在 | 先执行 `init` 流程 |
| plan / 方案 / 设计 / 架构 | `/speckit-plan` | spec.md 存在 | 先路由到 `specify` |
| tasks / 任务 / 拆解 | `/speckit-tasks` | plan.md 存在 | 先路由到 `plan` |
| clarify / 澄清 / 歧义 | `/speckit-clarify` | spec.md 存在 | 先路由到 `specify` |
| analyze / 分析 / 检查 | `/speckit-analyze` | tasks.md 存在 | 先路由到 `tasks` |
| implement / 实现 / 写代码 | `/speckit-implement` | **BDD 门禁已通过** | 告知门禁状态，禁止路由 |
| acceptance-doc / 验收文档 / 人工验收步骤 | `manual-acceptance-template.md` | 实现代码可运行 | 先路由到 `implement` |
| tester / 测试代理 / 按文档验证 | `tester-prompt-template.md` | 验收文档存在 | 先生成验收文档 |
| delivery-ledger / 门禁账本 / 交付证据 | `delivery-gate-ledger-template.md` | 需要审计交付状态 | 先明确交付范围 |
| init / 初始化 | 确认 git 仓库（无则 git init）→ AGENTS.md → `/speckit-constitution` | 无（自动创建） | — |

**关键词冲突消解**：同一句话命中多个行时，按阶段流顺序选择最靠后（最晚阶段）的匹配项。例如"分析需求"同时命中 `analyze` 和 `specify`，优先路由到 `analyze`（阶段更晚），但需确认 tasks.md 存在；若不存在则回退到 `specify`。

路由命中后，先输出一行 `路由到 {目标}`，再按该入口执行；只有遇到不可逆、破坏性或权限不足事项时才停下确认。

若请求明确不属于 Spec Kit / JYF 门禁范围，不列阶段选项；直接说明不属于 jyf 职责，建议按普通任务处理。

路由不到但仍可能属于 Spec Kit 范围时，向用户列举阶段选项（init / specify / clarify / plan / tasks / analyze / implement / acceptance-doc / tester / delivery-ledger），请其确认当前所处阶段，不展开第二套流程。

---

## BDD 门禁规则

```
BDD-待审核.md 存在 → 禁止写实现代码；只允许根据 BDD 写/更新测试，或输出待审核状态。
BDD 文件重命名为 BDD-已通过.md → 门禁解除 → 允许路由到 implement。
```

Agent 自动扫描 `**/BDD-待审核.md` 判断门禁状态。

**门禁作用域**：仓库级。仓库内任意路径下存在 `BDD-待审核.md`，则整个仓库的 implement 路由被阻断，不区分模块。若项目需要模块级独立门禁，需在 `AGENTS.md` 中显式声明，jyf 再按声明的模块边界扫描。

**重命名责任方**：由人工审核者（用户或指定 reviewer）负责将 `BDD-待审核.md` 重命名为 `BDD-已通过.md`；agent 不得自行执行此重命名，除非用户明确授权。

## 交付门禁流程

按需选择 references 模板；门禁账本贯穿需要审计的交付流程：
共同门禁原则：实现子线程和验收测试子线程都不得伪造证据、绕过真实流程、直接篡改状态或隐藏错误；各模板可在此基础上增加角色专属禁令。

| 阶段 | 模板 | 触发条件 |
|------|------|---------|
| 实现子线程 | `implementation-subagent-template.md` | 需要委派实现任务，尤其是多模块并行时 |
| 人工验收 | `manual-acceptance-template.md` | 功能可运行、需真人操作验收 |
| 测试代理 | `tester-prompt-template.md` | 验收文档就绪、需自动化按文档验证 |
| 门禁账本 | `delivery-gate-ledger-template.md` | 贯穿全流程，每个 gate 变更时更新 |

验证方式根据项目类型自动适配：浏览器操作 / CLI 命令 / API 请求 / 文件输出检查，不强制假设 Web 项目。

---

## 品质叠加（可选）

当项目涉及前端 UI 且需要设计品质管控时，可叠加使用同目录下的 `impeccable` 技能（`../impeccable/SKILL.md`，36 个设计参考文件，23 条命令）。产品级设计上下文由 impeccable 初始化流程生成；品质叠加依赖 DESIGN.md 或 PRODUCT.md，由 impeccable 在对应阶段产出或接入。

| 时机 | 叠加命令 | 效果 |
|------|---------|------|
| spec / plan 前 | `/impeccable teach` | 分析设计上下文，生成 DESIGN.md |
| 从已有代码逆向 | `/impeccable document` | 从现有项目代码生成 DESIGN.md |
| plan 阶段 | `/impeccable shape` | UX/UI 规划，写代码前定设计方向 |
| implement 后 | `/impeccable audit` | 技术质量检查（a11y / 性能 / 响应式） |
| implement 后 | `/impeccable critique` | UX 设计审查（层级 / 清晰度 / 情感共鸣） |
| 交付前 | `/impeccable polish` | 最终打磨，设计系统对齐 |

这些不是 jyf 的门禁步骤，但可以在门禁账本中记录品质检查结果。对非 UI 项目（CLI、库、后端）不触发。

---

## 额外约束

- 文档基线不足时优先补文档，再进入执行流。
- 优先用 `references/` 模板补齐文档，不临时自造格式。
- karpathy-guidelines：遵循 [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills/tree/main) 四原则。
- 不在这个 skill 里维护独立的项目规范或测试策略。
