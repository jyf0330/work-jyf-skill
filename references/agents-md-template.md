# AGENTS.md 初始化模板

`jyf init` 在新项目根目录创建或补齐 `AGENTS.md` 时使用此模板。
若目标项目已有 `AGENTS.md`，保留不冲突的既有规则，只补齐缺失的 JYF / Spec Kit / BDD / 验证约定。

```markdown
# AGENTS.md

## 项目工作协议

- 本文件约束当前目录及所有子目录。
- 更深层目录中的 `AGENTS.md` 可以覆盖本文件中同主题规则。
- 直接来自用户的最新明确指令优先于本文件。
- 保持改动小、可审查、可回退；不要顺手重构无关内容。
- 不要 revert 用户或其他 agent 的无关改动。
- 未经明确要求，不新增依赖，不执行破坏性 git 或文件系统操作。

## JYF / Spec Kit 流程

- 使用 `jyf` 处理初始化、规格、澄清、计划、任务、实现、验收和交付门禁路由。
- 标准阶段流：`init -> specify(BDD) -> clarify? -> human review(behavior BDD / test code / preconditions) -> plan -> tasks -> analyze? -> implement -> tester -> delivery-ledger PASS`。
- `jyf` 只负责路由和门禁，不维护第二套规格、计划、实现或测试流程。
- 路由到具体 `/speckit-*` 入口或 JYF `references/` 模板后，按对应入口执行。

## 人工审核门禁

- 正常流程中，人工只审核三项：操作型 BDD（用户如何操作、会得到什么）、每个 BDD 功能对应的测试代码、运行这些测试需要的前置/操作说明。
- `BDD-待审核.md` 存在时，禁止写实现代码；只允许根据 BDD 写或更新测试代码和前置说明，或输出待审核状态。
- 操作型 BDD、BDD 对应测试代码、测试前置说明三项均通过后，才允许进入实现。
- 只有用户或指定 reviewer 可以将 `BDD-待审核.md` 重命名为 `BDD-已通过.md`；agent 不得自行解锁，除非用户明确授权。
- 默认使用仓库级门禁：仓库内任意 `BDD-待审核.md` 会阻断整个仓库的 implement 路由。
- 若项目需要模块级门禁，必须在本文件或更深层 `AGENTS.md` 中明确模块边界和扫描规则。
- spec、plan、tasks、analyze、implement、delivery-ledger 默认由 agent 负责推进；只有用户明确要求或遇到阻塞时才请求人工介入。

## 文档基线

- 进入实现前必须存在 `AGENTS.md`，并且至少存在一份能说明目标行为的来源文档：BDD、spec、plan 或 tasks。
- 文档基线不足时，先路由到文档补齐流程，不让 agent 在没有来源文档时猜需求。
- `constitution` 由 `/speckit-constitution` 创建或更新；具体路径以该入口产物为准。

## 交付与验证

- 需要可审计交付时，使用 JYF delivery ledger 记录实现、主线程审查、自动验证、人工验收文档和 tester 验证证据。
- 验证方式根据项目类型选择：浏览器操作、CLI 命令、API 请求或文件输出检查。
- 最终报告必须说明改动文件、已验证内容、未验证风险和剩余阻塞。
```
