---
name: superpowers
version: 1.0.0
description: TDD 流程 + 系统化调试 - 复杂任务的完整解决方案
author: ai-max
triggers:
  - "功能"
  - "特性"
  - "模块"
  - "系统"
  - "实现"
  - "TDD"
priority: 80
builtin: true
---

# Superpowers - TDD + 系统化调试

> 适用于复杂任务的完整开发流程

## 触发条件

- 任务包含"功能"、"特性"、"模块"
- 任务复杂度评估 > 30 分钟
- 用户显式请求 TDD 流程

---

## TDD 流程（红灯 → 绿灯 → 重构）

### Phase 1: 🔴 红灯 - 编写失败的测试

**目标**：先写测试，代码还不存在

```typescript
// 示例：实现用户搜索功能
describe('searchUsers', () => {
  test('should return users matching query', async () => {
    // Given
    const query = 'john';

    // When
    const result = await searchUsers(query);

    // Then
    expect(result).toHaveLength(2);
    expect(result[0].name).toContain('John');
  });

  test('should return empty array when no match', async () => {
    const result = await searchUsers('nonexistent');
    expect(result).toEqual([]);
  });
});
```

**执行**：`npm test` → 测试失败（函数不存在）

### Phase 2: 🟢 绿灯 - 最小实现

**目标**：编写最少代码让测试通过

```typescript
export async function searchUsers(query: string): Promise<User[]> {
  const allUsers = await userRepository.findAll();
  return allUsers.filter(user =>
    user.name.toLowerCase().includes(query.toLowerCase())
  );
}
```

**执行**：`npm test` → 测试通过

### Phase 3: 🧹 重构 - 优化代码

**目标**：在测试保护下优化代码质量

```typescript
export async function searchUsers(query: string): Promise<User[]> {
  const normalizedQuery = normalizeQuery(query);
  const allUsers = await userRepository.findAll();

  return allUsers.filter(user =>
    matchesQuery(user.name, normalizedQuery)
  );
}

function normalizeQuery(query: string): string {
  return query.toLowerCase().trim();
}

function matchesQuery(text: string, query: string): boolean {
  return text.toLowerCase().includes(query);
}
```

**执行**：`npm test` → 测试仍然通过

---

## 系统化调试流程

### 1. 问题定位

```markdown
## 调试步骤

1. **复现问题**
   - 记录复现步骤
   - 确认错误信息
   - 检查日志

2. **缩小范围**
   - 二分法定位
   - 排除无关代码
   - 识别问题模块

3. **分析根因**
   - 检查数据流
   - 验证假设
   - 确认修复方案
```

### 2. 修复验证

```markdown
## 修复流程

1. **编写回归测试**
   - 捕获 bug 的测试用例
   - 确保测试失败

2. **实施修复**
   - 最小化修改
   - 保持代码一致性

3. **验证修复**
   - 运行测试
   - 检查副作用
   - 代码审查
```

### 3. 自动重试机制

```
最多自动重试 3 次：

第 1 次失败 → 分析错误 → 调整方案 → 重试
第 2 次失败 → 深入分析 → 寻求帮助 → 重试
第 3 次失败 → 人工介入 → 报告问题
```

---

## 子代理调研

对于复杂任务，启动子代理进行调研：

| Agent | 职责 |
|-------|------|
| Explore | 探索代码库，收集上下文 |
| Architect | 设计架构方案 |
| Code Reviewer | 审查代码质量 |

---

## 使用示例

```bash
# 自动触发 TDD 流程
/aimax:auto 实现用户认证功能

# 显式请求
/aimax:auto 用 TDD 方式实现购物车

# 调试问题
/aimax:auto 修复登录接口返回 500 错误
```

---

## 门禁检查

| 检查项 | 要求 |
|--------|------|
| 编译 | ✅ 通过 |
| 测试 | ✅ 全部通过 |
| 覆盖率 | ✅ >= 80% |
| Lint | ✅ 无错误 |

---

**核心原则**：
1. **先写测试** - 红灯 → 绿灯 → 重构
2. **最小实现** - 只写必要的代码
3. **持续重构** - 在测试保护下优化
4. **系统调试** - 有条不紊地定位问题
