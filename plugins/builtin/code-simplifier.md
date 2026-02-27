---
name: code-simplifier
version: 1.0.0
description: 代码清理专家 - 提取魔法值、简化条件、消除重复
author: ai-max
triggers:
  - "清理"
  - "优化"
  - "重构"
  - "简化"
  - "整理"
priority: 70
builtin: true
---

# Code Simplifier - 代码清理专家

> 针对最近改动的文件，应用清理规则

## 触发条件

- 任务包含"清理"、"优化"、"重构"、"简化"
- 或：功能完成后自动建议

---

## 清理规则

### 1. 提取魔法值

```typescript
// ❌ 清理前
if (user.age >= 18 && user.age <= 65) {
  // ...
}

// ✅ 清理后
const ADULT_AGE_MIN = 18;
const ADULT_AGE_MAX = 65;

if (user.age >= ADULT_AGE_MIN && user.age <= ADULT_AGE_MAX) {
  // ...
}
```

### 2. 简化条件表达式

```typescript
// ❌ 清理前
if (user.isActive === true) {
  return true;
} else {
  return false;
}

// ✅ 清理后
return user.isActive;
```

```typescript
// ❌ 清理前
if (items.length > 0) {
  return true;
}
return false;

// ✅ 清理后
return items.length > 0;
```

### 3. 消除重复代码

```typescript
// ❌ 清理前
function getUserName(user: User) {
  if (user && user.profile && user.profile.name) {
    return user.profile.name;
  }
  return 'Unknown';
}

function getUserEmail(user: User) {
  if (user && user.profile && user.profile.email) {
    return user.profile.email;
  }
  return 'Unknown';
}

// ✅ 清理后
function getUserField<K extends keyof Profile>(
  user: User,
  field: K,
  defaultValue: string = 'Unknown'
): string {
  return user?.profile?.[field] ?? defaultValue;
}

const userName = getUserField(user, 'name');
const userEmail = getUserField(user, 'email');
```

### 4. 简化函数签名

```typescript
// ❌ 清理前
function createUser(
  name: string,
  email: string,
  age: number,
  city: string,
  country: string
) { ... }

// ✅ 清理后
interface CreateUserDTO {
  name: string;
  email: string;
  age: number;
  city: string;
  country: string;
}

function createUser(dto: CreateUserDTO) { ... }
```

### 5. 使用现代语法

```typescript
// ❌ 清理前
const names = [];
for (let i = 0; i < users.length; i++) {
  names.push(users[i].name);
}

// ✅ 清理后
const names = users.map(user => user.name);
```

```typescript
// ❌ 清理前
const activeUsers = users.filter(function(user) {
  return user.isActive === true;
});

// ✅ 清理后
const activeUsers = users.filter(user => user.isActive);
```

### 6. 使用可选链和空值合并

```typescript
// ❌ 清理前
const street = user && user.address && user.address.street
  ? user.address.street
  : 'Unknown';

// ✅ 清理后
const street = user?.address?.street ?? 'Unknown';
```

### 7. 简化异步代码

```typescript
// ❌ 清理前
async function getData() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error(error);
    throw error;
  }
}

// ✅ 清理后
async function getData() {
  const response = await fetch(url);
  return response.json();
}
```

---

## 清理流程

```
1. 识别最近改动的文件
   ↓
2. 应用清理规则
   ├─ 提取魔法值
   ├─ 简化条件
   ├─ 消除重复
   ├─ 使用现代语法
   └─ 简化签名
   ↓
3. 运行测试确保功能不变
   ↓
4. 代码审查
```

---

## 使用示例

```bash
# 清理最近改动的代码
/aimax:auto 清理最近改动的代码

# 清理特定文件
/aimax:auto 清理 UserService 的代码

# 优化并重构
/aimax:auto 优化 AuthController 的代码结构
```

---

## 注意事项

1. **保持功能不变** - 清理后必须通过所有测试
2. **小步重构** - 每次只做一种清理
3. **保留注释** - 重要的业务逻辑注释不要删除
4. **检查性能** - 确保清理不影响性能

---

**核心原则**：
1. **提取常量** - 消除魔法值
2. **简化条件** - 让代码更易读
3. **消除重复** - DRY 原则
4. **现代语法** - 使用最新特性
