---
name: task-state-machine
version: 1.0.0
description: 任务分解执行状态机 - 支持中断恢复、可控重试和检查点恢复
author: ai-max
triggers:
  - "状态机"
  - "分步执行"
  - "中断恢复"
  - "恢复执行"
  - "重试"
  - "编排"
  - "长任务"
  - "checkpoint"
  - "resume"
  - "loop"
priority: 77
builtin: true
---

# Task State Machine - 任务分解执行状态机

> 面向复杂长任务的可恢复执行模型

## 触发条件

- 任务跨多个阶段，需要中间检查点
- 任务执行周期长，可能被中断
- 需要失败后“可控重试”，而不是无限重跑
- 用户明确要求“状态机/编排/恢复执行”

---

## 状态定义

| 状态 | 说明 | 进入条件 | 退出条件 |
|------|------|----------|----------|
| `INTAKE` | 接收任务与边界 | 收到任务输入 | 目标明确 |
| `CONTEXT` | 收集上下文 | 已确认目标 | 关键依赖已识别 |
| `DECOMPOSE` | 任务拆解 | 上下文齐备 | 步骤可执行 |
| `EXECUTE` | 执行子任务 | 有步骤计划 | 有执行结果 |
| `VERIFY` | 验证门禁 | 已有变更 | 门禁通过或失败 |
| `RECOVER` | 失败恢复 | 门禁失败 | 重试成功或放弃 |
| `SUMMARIZE` | 结果汇总 | 全部步骤完成 | 总结可交付 |
| `PERSIST` | 状态持久化 | 任意关键节点 | 快照已写入 |

---

## 转移规则

```text
INTAKE -> CONTEXT -> DECOMPOSE -> EXECUTE -> VERIFY

VERIFY(pass) -> SUMMARIZE -> PERSIST -> END
VERIFY(fail) -> RECOVER -> EXECUTE

任意状态中断 -> PERSIST -> STOP
恢复执行 -> 读取快照 -> 回到上次状态
```

---

## 检查点策略

### 持久化位置

- 默认：`.aimax/state/loop-state.json`
- 每个子步骤完成后必须更新快照

### 快照最小字段

```json
{
  "run_id": "loop-20260226-001",
  "task": "对支付模块做持续优化",
  "current_state": "VERIFY",
  "current_step_index": 3,
  "steps_total": 6,
  "retries": { "step-3": 1 },
  "gates": {
    "build": "pass",
    "tests": "pass",
    "lint": "fail"
  },
  "next_action": "进入 RECOVER，修复 lint 失败",
  "updated_at": "2026-02-26T12:00:00Z"
}
```

---

## 重试策略

1. 每个步骤默认最多重试 `3` 次
2. 重试路径：
   - 第 1 次：微调当前方案
   - 第 2 次：替代实现路径
   - 第 3 次：回滚并输出人工决策建议
3. 若连续失败达到阈值，必须进入 `SUMMARIZE` 输出失败报告，禁止静默重试

---

## 输出格式

```markdown
## 🔄 状态机执行报告

- run_id: loop-20260226-001
- 当前状态: VERIFY
- 当前步骤: 4/6
- 门禁: build✅ test✅ lint❌
- 重试次数: step-4 -> 1/3
- 下一步: 进入 RECOVER 修复 lint 错误
```

---

## 协作建议

- 与 `/aimax:evolve` 配合：状态机负责编排，evolve 负责评估收敛
- 与 `/aimax:tdd` 配合：在 `EXECUTE` 阶段保障最小回归风险
- 与 `/aimax:code-review` 配合：在 `VERIFY` 阶段增加质量审查
