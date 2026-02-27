# AI MAX

> 这是基于 [everything-claude-code](https://github.com/affaan-m/everything-claude-code) 进行二次开发，提供npm一键安装方式，协议沿用MIT

**Claude Code 增强配置，开箱即用。**

本仓库包含生产级 agents（代理）、skills（技能）、hooks（钩子）、commands（命令）、rules（规则）和 MCP 配置，帮助你快速提升 Claude Code 的使用体验。

---

## 快速开始

```bash
# 全局安装
npm install -g aimax

# 执行aimax，增强claude code智商
aimax                    # 终端执行aimax，进行交互式安装

# Claude Code 使用
/aimax:auto 你的问题      # 自动选择最优的aimax指令
```


CLI 提供交互式界面，让你选择要安装的组件：
- **Agents** - 专用子代理（planner, architect, tdd-guide 等）
- **Rules** - 必须遵循的准则（security, testing, coding-style 等）
- **Commands** - 斜杠命令（/aimax:plan, /aimax:tdd, /aimax:code-review 等）
- **Skills** - 工作流定义和领域知识

---

## 斜杠指令使用指南

安装 AI MAX 后，你可以在 Claude Code 中使用以下斜杠指令。

### 🚀 超级命令（推荐）

| 指令 | 用途 | 示例 |
|------|------|------|
| `/aimax:auto` | **智能超级命令** - 一站式完成需求分析、规划、编码、测试、审查全流程 | `/aimax:auto 用 Spring Boot 实现用户搜索 API` |

**一个命令搞定一切**：`/aimax:auto` 会自动检测项目上下文、评估任务复杂度、选择最佳策略、完成编码测试审查。

```
/aimax:auto 实现用户登录功能
↓ 自动完成
1. 检测项目上下文（语言、框架）
2. 评估复杂度（简单/中等/复杂）
3. 自动规划（复杂任务）
4. TDD 开发（先写测试）
5. 自动化门禁（构建、测试、覆盖率）
6. 代码审查（安全、质量）
7. 完成！
```

---

### 📦 单个命令（精细控制）

如果你需要精细控制某个环节，可以使用单个命令：

| 指令 | 用途 | 何时使用 |
|------|------|---------|
| `/aimax:plan` | 功能规划与实现方案 | 只需要设计方案 |
| `/aimax:tdd` | 测试驱动开发 | 已有明确方案，需要 TDD |
| `/aimax:code-review` | 代码质量与安全审查 | 代码已写好，需要审查 |
| `/aimax:build-fix` | 修复构建/类型错误 | 构建失败时 |
| `/aimax:e2e` | 端到端测试生成 | 需要端到端测试 |
| `/aimax:test-coverage` | 测试覆盖率分析 | 检查测试覆盖 |
| `/aimax:loop` | 状态机分步编排 | 需要中断恢复和可控重试 |
| `/aimax:evolve` | 持续迭代与回归门禁 | 需要评估驱动优化 |
| `/aimax:deep-plan` | 深度两阶段规划 | 复杂重构或架构迁移 |
| `/aimax:security-scan` | 安全审计扫描 | 检查配置和代码安全 |
| `/aimax:instinct-status` | 查看已学习的编码模式 | 查看 AI 学习进度 |
| `/aimax:refactor-clean` | 代码重构与清理 | 代码需要优化 |
| `/aimax:update-docs` | 更新项目文档 | 文档需要同步 |
| `/aimax:update-codemaps` | 更新代码架构图 | 架构图需要更新 |

---

### 详细说明

#### `/aimax:auto` - 智能超级命令

**一个命令，自动完成所有事情**。输入你的需求，它会自动：

1. **项目检测** - 自动识别语言、框架、加载插件
2. **复杂度评估** - 智能判断任务复杂度（简单/中等/复杂）
3. **插件调度** - 根据任务关键词自动调用八大插件
4. **TDD 开发** - 先写测试，再写代码
5. **自动化门禁** - 构建通过、测试通过、覆盖率达标
6. **代码审查** - 安全检查、质量检查
7. **知识更新** - 更新项目记忆（如有 Axiom）

**八大内置插件自动调度**：

| 插件 | 触发关键词 | 能力 |
|------|-----------|------|
| **Superpowers** | 功能、特性、模块、实现 | TDD 流程 + 系统化调试 |
| **Frontend Design** | 组件、界面、UI、页面 | 字体、间距、配色规范 |
| **Code Simplifier** | 清理、优化、重构、简化 | 提取常量、消除重复 |
| **Playground** | 可视化、工具、演示、看板 | HTML 工具生成 |
| **Chrome Automation** | 浏览器、网页、抓取、爬虫 | Playwright 自动化 |
| **PR Review Toolkit** | 审查、review、检查、PR | 多维度代码审查 |
| **Adaptive Evolution** | 迭代、演进、评估、基准、回归、CI | 评估门禁 + 回归防护闭环 |
| **Task State Machine** | 状态机、分步执行、中断恢复、重试、编排 | 任务分解 + 检查点恢复 |
| **Focus Chain** | 长任务、多步骤、保持专注、任务跟踪 | 任务焦点保持 + 偏离检测 |
| **Continuous Learning** | 学习、模式、习惯、instinct | 自动学习用户编码模式 |

```
# 简单任务 - 直接实现
/aimax:auto 修复登录按钮样式问题
→ 🟢 简单（5分钟）→ 直接修复

# 中等任务 - TDD + 审查
/aimax:auto 用 Spring Boot 实现用户搜索 API
→ 🟡 中等（45分钟）→ TDD + 审查

# 复杂任务 - 完整流程
/aimax:auto 实现用户认证系统
→ 🔴 复杂（2-3小时）→ 规划 + TDD + 审查 + 知识更新

# 前端组件 - 自动应用视觉规范
/aimax:auto 写一个登录表单组件
→ Frontend Design 插件 → 字体、间距、配色规范

# 代码审查 - 多维度检查
/aimax:auto 审查最近改动的代码
→ PR Review Toolkit → 测试、安全、质量、性能审查

# 自主演进 - 持续优化闭环
/aimax:auto 对支付模块做持续迭代优化并建立回归防护
→ Adaptive Evolution → 基线评估、门禁判定、失败恢复

# 状态机编排 - 中断可恢复
/aimax:auto 用状态机方式执行跨模块重构并可恢复
→ Task State Machine → 分步执行、检查点、恢复执行

# 深度规划 - 复杂架构重构
/aimax:auto 将订单系统拆分为微服务
→ Deep Plan → 两阶段规划（探索+执行）

# 安全审计 - 配置和代码安全
/aimax:auto 检查项目的安全漏洞
→ Security Scan → 密钥泄露、注入、配置审计
```

#### `/aimax:plan` - 实现规划

在编写代码之前创建详细的实现计划。适用于：
- 新功能开发
- 重大架构变更
- 复杂重构工作

```
/aimax:plan 添加实时通知功能
```

AI 会分析需求、识别风险、创建分步计划，**并等待你确认后才开始编码**。

#### `/aimax:tdd` - 测试驱动开发

强制执行 TDD 工作流：先写测试，再写实现。适用于：
- 新功能实现
- Bug 修复
- 关键业务逻辑

```
/aimax:tdd 实现价格计算器
```

遵循 **红-绿-重构** 循环，确保 80% 以上测试覆盖率。

#### `/aimax:code-review` - 代码审查

对未提交的更改进行全面审查，检查：
- 🔴 安全问题（凭证泄露、SQL 注入、XSS）
- 🟠 代码质量（函数过长、嵌套过深）
- 🟡 最佳实践（可变模式、缺少测试）

```
/aimax:code-review
```

#### `/aimax:build-fix` - 构建错误修复

快速修复构建和类型错误。适用于：
- TypeScript 类型错误
- 编译失败
- 构建流程问题

```
/aimax:build-fix
```

#### `/aimax:e2e` - 端到端测试

使用 Playwright 生成和运行 E2E 测试。适用于：
- 用户流程测试
- 跨页面功能验证
- UI 自动化测试

```
/aimax:e2e 测试用户登录到下单的完整流程
```

#### `/aimax:test-coverage` - 覆盖率分析

分析测试覆盖率，识别未覆盖的代码。

```
/aimax:test-coverage
```

#### `/aimax:loop` - 状态机分步编排

将复杂任务映射为可恢复状态机（INTAKE/CONTEXT/DECOMPOSE/EXECUTE/VERIFY/RECOVER），每步写检查点并支持恢复执行。

```
/aimax:loop 对订单结算链路做分步优化，支持中断恢复
```

也可以用终端执行器直接维护状态快照：

```bash
aimax loop init --task "重构订单结算" --steps "分析,重构,验证"
aimax loop status
aimax loop next --verify pass
aimax loop resume
```

#### `/aimax:evolve` - 自主演进闭环

以“评估驱动”的方式持续优化项目，适用于跨迭代提升质量和性能。核心流程：
- 建立基线（测试/覆盖率/性能）
- 生成最小补丁（可回滚）
- 执行门禁（构建、测试、审查、可选 LLM eval）
- PR 自动评估摘要（门禁结果自动回写评论）
- 失败恢复（最多 3 轮）

```
/aimax:evolve 对支付模块做持续优化，目标是 P95 降低 20%
```

#### `/aimax:refactor-clean` - 重构清理

移除死代码、优化结构、消除重复。

```
/aimax:refactor-clean 清理这个模块中未使用的代码
```

#### `/aimax:update-docs` - 文档更新

更新项目文档、README、API 文档。

```
/aimax:update-docs
```

#### `/aimax:update-codemaps` - 架构图更新

生成或更新代码架构图和模块依赖图。

```
/aimax:update-codemaps
```

### 推荐工作流

```
1. /aimax:plan        → 规划功能
2. /aimax:deep-plan   → 复杂任务深度规划
3. /aimax:loop        → 状态机编排与可恢复执行
4. /aimax:tdd         → 测试驱动实现
5. /aimax:code-review → 审查代码
6. /aimax:security-scan → 安全审计
7. /aimax:evolve      → 建立门禁并持续优化
8. /aimax:build-fix   → 修复构建问题（如有）
9. git commit         → 提交代码
```

---

## 核心概念

### Agents（代理）

子代理以有限的范围处理委派的任务。示例：

```markdown
---
name: code-reviewer
description: 审查代码的质量、安全性和可维护性
tools: Read, Grep, Glob, Bash
model: opus
---

你是一位资深代码审查员...
```

### Skills（技能）

技能是由命令或代理调用的工作流定义：

```markdown
# TDD 工作流

1. 首先定义接口
2. 编写失败的测试（红灯）
3. 实现最少代码（绿灯）
4. 重构（改进）
5. 验证 80%+ 覆盖率
```

### Hooks（钩子）

Hooks 在工具事件时触发。示例 - 警告 console.log：

```json
{
  "matcher": "tool == \"Edit\" && tool_input.file_path matches \"\\\\.(ts|tsx|js|jsx)$\"",
  "hooks": [{
    "type": "command",
    "command": "#!/bin/bash\ngrep -n 'console\\.log' \"$file_path\" && echo '[Hook] Remove console.log' >&2"
  }]
}
```

### Rules（规则）

规则是必须始终遵循的准则。保持模块化：

```
~/.claude/rules/
  security.md      # 禁止硬编码密钥
  coding-style.md  # 不可变性、文件限制
  testing.md       # TDD、覆盖率要求
```

---

## 重要说明

### 上下文窗口管理

**关键：** 不要同时启用所有 MCP。启用太多工具可能会使你的 200k 上下文窗口缩小到 70k。

经验法则：
- 配置 20-30 个 MCP
- 每个项目启用不超过 10 个
- 活动工具不超过 80 个

在项目配置中使用 `disabledMcpServers` 禁用未使用的工具。

### 定制化

这些配置适合我的工作流程。你应该：
1. 从与你产生共鸣的内容开始
2. 根据你的技术栈修改
3. 移除你不使用的内容
4. 添加你自己的模式

---

## 仓库内容

```
aimax/
|-- agents/           # 用于任务委派的专用子代理
|   |-- planner.md           # 功能实现规划
|   |-- architect.md         # 系统设计决策
|   |-- tdd-guide.md         # 测试驱动开发
|   |-- code-reviewer.md     # 质量和安全审查
|   |-- security-reviewer.md # 漏洞分析
|   |-- build-error-resolver.md
|   |-- e2e-runner.md        # Playwright E2E 测试
|   |-- refactor-cleaner.md  # 死代码清理
|   |-- doc-updater.md       # 文档同步
|
|-- skills/           # 工作流定义和领域知识
|   |-- coding-standards.md         # 编程语言最佳实践
|   |-- backend-patterns.md         # API、数据库、缓存模式
|   |-- frontend-patterns.md        # React、Next.js 模式
|   |-- project-guidelines-example.md # 项目特定技能示例
|   |-- tdd-workflow/               # TDD 方法论
|   |-- security-review/            # 安全检查清单
|   |-- clickhouse-io.md            # ClickHouse 分析
|
|-- commands/         # 用于快速执行的斜杠命令
|   |-- auto.md              # /aimax:auto - 智能超级命令
|   |-- tdd.md              # /aimax:tdd - 测试驱动开发
|   |-- plan.md             # /aimax:plan - 实现规划
|   |-- loop.md             # /aimax:loop - 状态机分步编排
|   |-- deep-plan.md        # /aimax:deep-plan - 深度两阶段规划
|   |-- security-scan.md    # /aimax:security-scan - 安全审计扫描
|   |-- evolve.md           # /aimax:evolve - 自主演进闭环
|   |-- e2e.md              # /aimax:e2e - E2E 测试生成
|   |-- code-review.md      # /aimax:code-review - 质量审查
|   |-- build-fix.md        # /aimax:build-fix - 修复构建错误
|   |-- refactor-clean.md   # /aimax:refactor-clean - 死代码移除
|   |-- test-coverage.md    # /aimax:test-coverage - 覆盖率分析
|   |-- update-codemaps.md  # /aimax:update-codemaps - 刷新文档
|   |-- update-docs.md      # /aimax:update-docs - 同步文档
|
|-- plugins/          # 插件系统
|   |-- builtin/             # 内置插件（八大插件）
|   |   |-- auto-core.md          # 自动路由核心
|   |   |-- superpowers.md        # TDD + 系统化调试
|   |   |-- frontend-design.md    # 前端视觉设计
|   |   |-- code-simplifier.md    # 代码清理
|   |   |-- playground.md         # HTML 工具生成
|   |   |-- chrome-automation.md  # 浏览器自动化
|   |   |-- pr-review-toolkit.md  # 代码审查
|   |   |-- adaptive-evolution.md # 自主演进闭环
|   |   |-- task-state-machine.md # 分步编排 + 中断恢复
|   |   |-- focus-chain.md       # 任务焦点保持
|   |   |-- tdd-templates.md      # 多语言测试模板
|   |-- framework/           # 框架插件
|   |   |-- java/
|   |   |   |-- spring.md         # Spring Boot 规范
|   |   |-- javascript/
|   |       |-- react.md          # React 组件规范
|
|-- rules/            # 必须遵循的准则
|   |-- security.md         # 强制性安全检查
|   |-- coding-style.md     # 不可变性、文件组织
|   |-- testing.md          # TDD、80% 覆盖率要求
|   |-- git-workflow.md     # 提交格式、PR 流程
|   |-- agents.md           # 何时委派给子代理
|   |-- performance.md      # 模型选择、上下文管理
|   |-- patterns.md         # API 响应格式、hooks
|   |-- hooks.md            # Hook 文档
|
|-- hooks/            # 基于触发器的自动化
|   |-- hooks.json          # PreToolUse、PostToolUse、Stop hooks
|
|-- mcp-configs/      # MCP 服务器配置
|   |-- mcp-servers.json    # GitHub、Supabase、Vercel、Railway 等
|
|-- lib/              # 核心库
|   |-- axiom-detector.md   # Axiom 集成检测
|
|-- templates/        # 可复用模板
|   |-- project-config/      # 项目 CLAUDE.md 模板
|   |   |-- aimax-loop-state-template.json # 状态机检查点模板
|   |-- ci/
|       |-- aimax-evolution-gates.yml # 持续迭代门禁模板
|       |-- aimax-pr-eval-comment.yml # PR 自动评估注释模板
|
|-- examples/         # 示例配置
    |-- CLAUDE.md           # 项目级配置示例
    |-- user-CLAUDE.md      # 用户级配置示例 (~/.claude/CLAUDE.md)
    |-- statusline.json     # 自定义状态栏配置
```

---

## 许可证

MIT - 自由使用，按需修改，如果可以请回馈贡献。

---

**如果有帮助请给这个仓库点星。阅读指南。构建伟大的东西。**
