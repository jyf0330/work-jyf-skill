# Human Operation Verification Document Template

Use this structure when creating a planner/product-facing manual acceptance document.

```markdown
# <feature name> 真人操作验收

## 覆盖范围

- <what this validation covers>

## 不覆盖范围

- <what this validation explicitly does not cover>

## 被测环境

- 项目路径：
- 分支 / commit：
- 测试地址：
- 浏览器 / 视口：
- 测试账号 / 测试数据：

## 启动或重置方式

- <how to open, launch, seed, or reset the app>
- <how to recover if a step leaves the app in the wrong state>

## 验收步骤

| 步骤 | 前置状态 | 操作 | 预期可见结果 | 需要记录的证据 | 通过/失败 | 实际观察 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | <state> | <user action> | <visible expected result> | <screenshot/value/console/network notes> |  |  |
| 2 | <state> | <user action> | <visible expected result> | <screenshot/value/console/network notes> |  |  |

## 最终结论

- 通过步骤数：
- 失败步骤数：
- 阻塞问题：
- 证据位置：
- 验收结论：
```
