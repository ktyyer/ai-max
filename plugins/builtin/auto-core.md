---
name: auto-core
version: 2.0.0
description: 智能路由核心 - 集成 Axiom + Agent + 插件系统
author: ai-max
priority: 100
builtin: true
---

# 智能路由核心 (auto-core)

> ai-max 的核心路由引擎，集成 Axiom 长期记忆、Agent 系统和插件系统

## 核心能力

### 1. Axiom 集成

```markdown
## Axiom 能力检测

在执行任务前，检查是否存在 Axiom：

```bash
# 检查 .agent/ 目录
if (存在 .agent/workflows/start.md) {
    ✅ 项目有 Axiom
    → 可以调用 /start
    → 可以读取 .agent/memory/project_decisions.md
    → 可以使用知识进化 /evolve
} else {
    ❌ 项目无 Axiom
    → 仅使用 /aimax:auto + Agent 系统
}
```

## 在执行任何任务前读取 Axiom 记忆

if (存在 .agent/memory/project_decisions.md) {
    读取架构决策
    读取编码规范
    读取项目模式
}

# 确保 /aimax:auto 生成的代码符合项目既定规范
```

### 2. 任务复杂度评估

| 级别 | 预估时间 | 处理方式 |
|------|---------|---------|
| 🟢 简单 | < 30 分钟 | 直接实现 + 语言规范 |
| 🟡 中等 | 30-120 分钟 | TDD Agent + 代码审查 |
| 🔴 复杂 | > 120 分钟 | 检测 Axiom → 建议 /start 或 Planner Agent |

#### 复杂度评估维度

1. **关键词分析**
   - 简单：函数、方法、变量、修复、添加
   - 中等：模块、组件、接口、服务、API
   - 复杂：系统、架构、集成、重构、迁移、演进、评估、基准

2. **文件数量预估**
   - 简单：单文件修改
   - 中等：2-5 个文件
   - 复杂：>5 个文件或跨模块

3. **依赖复杂度**
   - 无外部依赖 → 保持原级别
   - 有外部 API 调用 → 提升一级
   - 有数据库变更 → 提升一级

4. **业务逻辑**
   - CRUD 操作 → 保持原级别
   - 有业务规则 → 提升一级
   - 有复杂算法 → 提升一级

5. **演进任务信号**
   - 包含“迭代、演进、回归、持续优化、CI” → 额外加载 `adaptive-evolution` 插件

6. **状态机任务信号**
   - 包含“状态机、分步执行、中断恢复、重试、编排” → 额外加载 `task-state-machine` 插件

7. **深度规划信号**
   - 包含“重构、迁移、拆分、微服务、架构重设计” → 建议使用 `/aimax:deep-plan`

8. **安全审计信号**
   - 包含“安全、审计、漏洞、扫描、密钥、注入” → 额外加载安全扫描

9. **焦点保持信号**
   - 复杂度 >= 中等时自动激活 `focus-chain` 插件

10. **持续学习信号**
    - 包含“学习、模式、习惯、instinct” → 加载 continuous-learning 技能

### 3. 插件自动发现

```markdown
## 插件扫描规则

### 扫描目录

1. `plugins/builtin/` - 内置插件（始终加载）
2. `plugins/framework/` - 框架插件（按需加载）

### 插件匹配逻辑

```bash
# 1. 检测项目语言/框架
language = detect_language()  # js, python, java, go
framework = detect_framework() # react, spring, django, gin

# 2. 加载匹配插件
plugins = []
plugins += load_builtin_plugins()
plugins += load_framework_plugins(language, framework)

# 3. 根据关键词匹配
for plugin in plugins:
    if any(keyword in user_input for keyword in plugin.triggers):
        load_plugin(plugin)
```

### 插件优先级

- 优先级范围：0-100（越高越优先）
- 内置插件：100
- 框架插件：50
- 用户插件：0-49
```

### 4. Agent 自动调度

```markdown
## Agent 调度规则

### 按任务类型调度

| 任务类型 | 调度 Agent |
|---------|-----------|
| 新功能开发 | planner → tdd-guide → code-reviewer |
| Bug 修复 | tdd-guide → code-reviewer |
| 代码重构 | refactor-cleaner → code-reviewer |
| 架构设计 | architect → planner |
| 安全审查 | security-reviewer |
| 文档更新 | doc-updater |
| E2E 测试 | e2e-runner |
| 构建错误 | build-error-resolver |

### 按复杂度调度

| 复杂度 | 调度策略 |
|--------|---------|
| 简单 | 直接执行，无需 Agent |
| 中等 | 单 Agent 协助 |
| 复杂（有 Axiom） | **建议 /start（Axiom 工作流）** |
| 复杂（无 Axiom） | planner → 多 Agent 协作 |
```

## 完整路由流程

```
用户输入
  ↓
┌─────────────────────────────────────┐
│ 第1步：项目上下文检测                │
├─────────────────────────────────────┤
│  • 检测语言/框架                     │
│  • 检测 Axiom（.agent/）             │
│  • 读取 Axiom 记忆（如有）           │
└─────────────────────────────────────┘
  ↓
┌─────────────────────────────────────┐
│ 第2步：复杂度评估                    │
├─────────────────────────────────────┤
│  🟢 简单 → 直接实现                  │
│  🟡 中等 → Agent 协助                │
│  🔴 复杂 →                           │
│      ├─ 有 Axiom → 建议 /start       │
│      └─ 无 Axiom → Planner Agent     │
└─────────────────────────────────────┘
  ↓
┌─────────────────────────────────────┐
│ 第3步：插件匹配                      │
├─────────────────────────────────────┤
│  • 检测关键词                        │
│  • 加载匹配插件                      │
│  • 对齐项目现有风格（优先于插件默认） │
└─────────────────────────────────────┘
  ↓
┌─────────────────────────────────────┐
│ 第4步：执行任务                      │
├─────────────────────────────────────┤
│  • 调用 Agent（如需）                │
│  • 生成代码                          │
│  • 运行测试                          │
│  • 代码审查                          │
└─────────────────────────────────────┘
  ↓
┌─────────────────────────────────────┐
│ 第5步：知识进化（如有 Axiom）        │
├─────────────────────────────────────┤
│  • 更新项目记忆                      │
│  • 记录新模式                        │
│  • 提取经验教训                      │
└─────────────────────────────────────┘
```

## 与 Axiom 的协作

### /aimax:auto 检测到复杂任务时

```markdown
## 复杂任务建议

当 /aimax:auto 检测到复杂任务（>120分钟）且项目有 Axiom 时：

1. 显示建议：
   "检测到复杂任务，建议使用 Axiom /start 工作流"
   "是否切换到 /start？(y/n)"

2. 用户确认后：
   - 切换到 /start 工作流
   - Axiom 负责整体流程
   - /aimax:auto 负责具体编码

3. 用户拒绝：
   - 使用 Planner Agent + 多 Agent 协作
   - 保持 /aimax:auto 流程
```

### Axiom 调用 /aimax:auto

```markdown
## Axiom 工作流中的 /aimax:auto

在 Axiom 的编码实现阶段：

1. Axiom 调用 /aimax:auto 执行具体编码
2. /aimax:auto 读取 Axiom 记忆中的项目规范
3. /aimax:auto 生成符合规范的代码
4. Axiom 更新记忆

形成闭环：
Axiom → /aimax:auto → 代码 → Axiom 记忆 → /aimax:auto
```

## 项目上下文检测

### 语言检测

| 语言 | 检测文件 |
|------|---------|
| JavaScript/TypeScript | package.json |
| Python | requirements.txt, pyproject.toml |
| Java | pom.xml, build.gradle |
| Go | go.mod |
| Rust | Cargo.toml |

### 框架检测

| 框架 | 检测特征 |
|------|---------|
| React | package.json 有 "react" |
| Vue | package.json 有 "vue" |
| Angular | package.json 有 "@angular" |
| Spring | pom.xml 有 "spring-boot" |
| Django | requirements.txt 有 "django" |
| FastAPI | requirements.txt 有 "fastapi" |
| Gin | go.mod 有 "github.com/gin-gonic/gin" |

### Axiom 检测

| 检测项 | 路径 |
|--------|------|
| Axiom 工作流 | `.agent/workflows/start.md` |
| 长期记忆 | `.agent/memory/project_decisions.md` |
| 编码模式 | `.agent/memory/coding_patterns.md` |
| 经验教训 | `.agent/memory/lessons_learned.md` |

## 输出格式

### 任务分析输出

```markdown
📊 任务分析

🎯 **复杂度**: 🟡 中等（预计 45 分钟）
📝 **语言**: Java + Spring Boot
🔌 **插件**: spring-helper
🤖 **Agent**: tdd-guide → code-reviewer

📋 **执行计划**:
1. 使用 TDD 流程实现功能
2. 生成单元测试
3. 代码审查

⏳ 开始执行...
```

### 复杂任务建议

```markdown
⚠️ 检测到复杂任务

🎯 **复杂度**: 🔴 复杂（预计 >120 分钟）
📝 **建议**: 使用 Axiom /start 工作流

Axiom 提供完整的复杂任务处理流程：
- 需求分析
- 架构设计
- 编码实现
- 代码审查
- 知识进化

是否切换到 /start？(y/n)
```

---

**核心原则**：
1. **智能检测** - 自动识别项目上下文
2. **Axiom 优先** - 复杂任务建议使用 Axiom
3. **项目优先** - 先遵循项目现有代码风格，再用插件兜底
4. **Agent 协作** - 智能调度专业化 Agent
5. **插件扩展** - 自动加载匹配插件
