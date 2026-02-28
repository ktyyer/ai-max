---
name: adaptive-evolution
version: 2.0.0
description: 持续演进触发器 - 检测迭代/演进意图，调度 evolve 命令的评估驱动闭环
author: ai-max
triggers:
  - "迭代"
  - "演进"
  - "持续优化"
  - "评估"
  - "基准"
  - "回归"
  - "自动修复"
  - "CI"
priority: 65
builtin: true
---

# Adaptive Evolution — 持续演进触发器

> 触发器职责：检测到演进/迭代意图 → 调度评估驱动闭环

## 触发后执行

调度 `/aimax:evolve` 命令的评估门禁流程：

```
评估先行 → 建立基线 → 最小补丁 → 验证矩阵 → 门禁判定
```

**失败恢复（最多3轮）：**
1. 第1轮失败 → 微调方案
2. 第2轮失败 → 替代方案
3. 第3轮失败 → 回滚建议

**门禁维度：** 构建 / 测试 / 覆盖率 / 性能 / 安全

> 直接调用：`/aimax:evolve`
