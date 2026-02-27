---
name: pr-review-toolkit
version: 1.0.0
description: 代码审查工具 - 多维度代理审查
author: ai-max
triggers:
  - "审查"
  - "review"
  - "检查"
  - "PR"
  - "代码质量"
priority: 75
builtin: true
---

# PR Review Toolkit - 代码审查工具

> 多维度代理审查，全面检查代码质量

## 触发条件

- 任务包含"审查"、"review"、"检查"
- 或：代码提交前自动建议

---

## 审查维度

### 1. 测试覆盖率审查

```markdown
## 检查项

- [ ] 新代码是否有对应的测试
- [ ] 测试覆盖率是否 >= 80%
- [ ] 边界条件是否被测试
- [ ] 错误场景是否被测试
- [ ] 测试是否独立、可重复

## 输出

✅ 通过 / ⚠️ 警告 / ❌ 失败
```

### 2. 错误处理审查

```markdown
## 检查项

- [ ] 是否正确处理异常
- [ ] 错误信息是否清晰
- [ ] 是否有适当的重试机制
- [ ] 资源是否正确释放
- [ ] 是否有回退方案

## 常见问题

❌ 吞掉异常
try {
  // ...
} catch (e) {
  // 什么都没做
}

✅ 正确处理
try {
  // ...
} catch (e) {
  logger.error('操作失败', { error: e });
  throw new BusinessError('用户友好的错误信息');
}
```

### 3. 类型设计审查

```markdown
## 检查项

- [ ] 类型定义是否完整
- [ ] 是否避免 any 类型
- [ ] 是否使用严格模式
- [ ] 泛型使用是否合理
- [ ] 接口是否清晰

## 常见问题

❌ 过度使用 any
function process(data: any) { ... }

✅ 使用具体类型
interface UserData {
  id: string;
  name: string;
}
function process(data: UserData) { ... }
```

### 4. 代码质量审查

```markdown
## 检查项

- [ ] 函数长度是否合理（< 50 行）
- [ ] 是否有深层嵌套（< 4 层）
- [ ] 命名是否清晰
- [ ] 是否有重复代码
- [ ] 是否有魔法值

## 质量指标

| 指标 | 要求 |
|------|------|
| 函数长度 | < 50 行 |
| 文件长度 | < 300 行 |
| 圈复杂度 | < 10 |
| 嵌套深度 | < 4 层 |
| 参数数量 | < 5 个 |
```

### 5. 安全审查

```markdown
## 检查项

- [ ] 无硬编码密钥
- [ ] 用户输入已验证
- [ ] SQL 注入防护
- [ ] XSS 防护
- [ ] CSRF 保护

## 高危问题

🔴 硬编码密钥
const apiKey = "sk-xxxxx";

🔴 SQL 注入
const sql = `SELECT * FROM users WHERE id = ${userId}`;

🔴 XSS 漏洞
element.innerHTML = userInput;

## 正确做法

✅ 使用环境变量
const apiKey = process.env.API_KEY;

✅ 参数化查询
const sql = 'SELECT * FROM users WHERE id = ?';
db.query(sql, [userId]);

✅ 安全渲染
element.textContent = userInput;
```

### 6. 性能审查

```markdown
## 检查项

- [ ] 是否有不必要的循环
- [ ] 是否有内存泄漏风险
- [ ] 是否有 N+1 查询问题
- [ ] 是否正确使用缓存
- [ ] 是否有大型数据加载

## 常见问题

❌ N+1 查询
for (const user of users) {
  const orders = await getOrders(user.id);
}

✅ 批量查询
const userIds = users.map(u => u.id);
const orders = await getOrdersByUserIds(userIds);
```

---

## 审查流程

```
1. 收集变更文件
   ↓
2. 运行各维度审查
   ├─ 测试覆盖率审查
   ├─ 错误处理审查
   ├─ 类型设计审查
   ├─ 代码质量审查
   ├─ 安全审查
   └─ 性能审查
   ↓
3. 生成审查报告
   ↓
4. 提供修复建议
```

---

## 审查报告格式

```markdown
# 代码审查报告

## 📊 总体评分: B+ (85/100)

## 🔴 严重问题 (必须修复)

### 1. 硬编码 API 密钥
**文件**: src/api/client.ts:15
**问题**: 发现硬编码的 API 密钥
**建议**: 使用环境变量 `process.env.API_KEY`

## 🟠 重要问题 (建议修复)

### 2. 缺少错误处理
**文件**: src/services/user.ts:42
**问题**: fetch 调用没有错误处理
**建议**: 添加 try-catch 并处理网络错误

## 🟡 轻微问题 (可选修复)

### 3. 函数过长
**文件**: src/utils/parser.ts:100-180
**问题**: parseData 函数有 80 行
**建议**: 拆分为多个小函数

## ✅ 通过的检查

- 测试覆盖率: 85%
- 无 SQL 注入风险
- 类型定义完整
```

---

## 使用示例

```bash
# 审查最近改动的代码
/aimax:auto 审查最近改动的代码

# 审查特定文件
/aimax:auto 审查 UserService.ts

# 全面审查
/aimax:auto 对整个 PR 进行代码审查
```

---

## 审查建议优先级

| 级别 | 说明 | 处理方式 |
|------|------|---------|
| 🔴 严重 | 安全漏洞、数据丢失风险 | 必须立即修复 |
| 🟠 重要 | 功能缺陷、性能问题 | 建议修复后再合并 |
| 🟡 轻微 | 代码风格、可读性 | 可以后续优化 |
| 💡 建议 | 最佳实践、改进空间 | 可选采纳 |

---

## 与 code-reviewer Agent 的关系

PR Review Toolkit 是 **审查规范**，code-reviewer Agent 是 **执行者**。

```
/aimax:auto 审查代码
    ↓
加载 pr-review-toolkit.md（审查规范）
    ↓
调用 code-reviewer Agent（执行审查）
    ↓
生成审查报告
```

---

**核心原则**：
1. **全面覆盖** - 多维度检查
2. **优先级清晰** - 区分严重程度
3. **可操作** - 提供具体建议
4. **持续改进** - 更新审查规则
