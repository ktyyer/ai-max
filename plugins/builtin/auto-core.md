---
name: auto-core
version: 3.0.0
description: 智能路由大脑 - 统一路由协议、会话初始化、能力链、自动经验沉淀
author: ai-max
priority: 100
builtin: true
---

# 智能路由大脑 (auto-core v3.0)

> `/aimax:auto` 的核心路由引擎：一个大脑，统一调度所有能力

---

## 🚀 步骤0：强制会话初始化（每次必须先执行）

```
每次执行 /aimax:auto 前，必须完成以下检测：

1. 读取 CLAUDE.md（如存在）→ 加载项目规范、禁止事项、响应格式
2. 读取 REPO_MAP.md（如存在）→ 加载仓库符号地图，快速定位代码
3. 读取 .claude/rules/ 目录 → 加载适用规则（java-coding-style/security等）
4. 检测技术栈（详见下方语言/框架检测表）
5. 记录 session_context：{task_type, complexity, files_to_modify}

⚠️ 如果文件数量 > 50 且不存在 REPO_MAP.md：
   → 建议用户先运行 /aimax:update-codemaps 生成符号地图
```

---

## 📊 步骤1：任务复杂度评估

| 级别 | 预估 | 关键词信号 | 路由策略 |
|------|------|-----------|---------|
| 🟢 **简单** | <30分钟 | 修复、函数、方法、变量、样式 | 直接实现 |
| 🟡 **中等** | 30-120分钟 | 模块、接口、API、组件、服务 | TDD + 代码审查 + Focus Chain |
| 🔴 **复杂** | >120分钟 | 系统、架构、重构、迁移、微服务 | → 建议 `/aimax:deep-plan` 两阶段规划 |

**复杂度修正规则：**
- 有外部 API 调用 → +1 级
- 有数据库 Schema 变更 → +1 级
- 跨 5 个以上文件 → 提升至复杂

---

## ⛓️ 步骤2：能力链（单一职责，去重分层）

**每个业务域只有一条能力链：命令 → Agent → Skill**

```
功能开发:    /aimax:auto → tdd-guide(Agent) → tdd-workflow(Skill) + superpowers(触发)
代码审查:    /aimax:code-review → code-reviewer(Agent) → pr-review-toolkit(触发)
重构清理:    /aimax:refactor-clean → refactor-cleaner(Agent) → code-simplifier(触发)
安全审计:    /aimax:security-scan → security-reviewer(Agent) → security-review(Skill)
架构规划:    /aimax:deep-plan → architect(Agent) + planner(Agent)
文档更新:    /aimax:update-docs → doc-updater(Agent)
E2E测试:     /aimax:e2e → e2e-runner(Agent)
构建修复:    /aimax:build-fix → build-error-resolver(Agent)
持续演进:    /aimax:evolve → adaptive-evolution(触发) → evaluate → iterate
任务编排:    /aimax:loop → task-state-machine(触发) → checkpoint → resume

⚠️ 去重原则：
  - Agent 是执行者，读 Skill 获取知识（Skill 内容不在插件中重复）
  - 插件只做关键词触发和路由信号，不重复 Skill/Agent 的详细内容
  - Commands 是用户入口，内部调用对应 Agent
```

---

## 🔌 步骤3：意图信号路由表

根据用户输入关键词，自动激活对应能力：

| 信号关键词 | 触发能力 | 优先级 |
|-----------|---------|--------|
| 功能、特性、模块、实现、新增 | superpowers → TDD流程 + tdd-templates | 高 |
| 组件、界面、UI、页面、样式 | Frontend Design → 视觉规范 | 高 |
| 清理、重构、简化、代码质量 | code-simplifier → 重构 | 高 |
| 审查、review、检查、PR | code-reviewer → PR审查 | 高 |
| 安全、漏洞、扫描、密钥、注入 | security-reviewer → 安全审计 | 🔴紧急 |
| 可视化、工具、演示、看板 | Playground → HTML生成 | 中 |
| 浏览器、抓取、爬虫、自动化 | Chrome Automation → Playwright | 中 |
| 迭代、演进、回归、CI、基准 | adaptive-evolution → 评估门禁 | 中 |
| 状态机、分步、中断、编排、长任务 | task-state-machine → 检查点 | 中 |
| E2E、端到端、UI测试、集成测试 | e2e-runner → Playwright/Cypress | 中 |
| 构建失败、编译错误、依赖错误 | build-error-resolver → 构建修复 | 高 |
| 重构、迁移、微服务、架构重设计 | → 建议 `/aimax:deep-plan` | 特殊 |
| 大型项目、多模块、符号地图 | repo-map skill → 先建地图 | 前置 |
| 继续上次、对话太长、上下文满 | context-compression → 锚定摘要 | 前置 |
| 并行、多任务、独立功能 | git-worktree skill → 分支隔离 | 可选 |
| 省钱、优化成本、批量任务 | cost-optimizer → OpusPlan路由 | 可选 |

### 🧠 技能主动判断规则（无需关键词，自动检测条件触发）

| 条件检测 | 自动激活技能 |
|---------|------------|
| 当前对话轮次 > 15 或上下文 > 70% | **context-compression** — 自动锚定摘要 |
| 项目文件数 > 50 且无 REPO_MAP.md | **repo-map** — 建议先生成符号地图 |
| 任务复杂度=复杂 且有多个独立子模块 | **git-worktree** — 提示并行 worktree 隔离 |
| 任务使用 Opus 且预估 > 3000 tokens | **cost-optimizer** — 自动降级到 Sonnet 执行 |
| 复杂度 ≥ 中等（始终触发） | **focus-chain** — 强制开启专注保持模式 |

---

## 🏗️ 步骤4：框架插件 + 规则自动加载

**技术栈检测 → 自动加载对应规范：**

| 检测文件 | 框架 | 加载插件 | 加载规则 |
|---------|------|---------|---------|
| `pom.xml` 含 spring-boot | Java/Spring Boot | spring.md | java-coding-style.md |
| `package.json` 含 react/next | TypeScript/React | react.md | coding-style.md |
| `requirements.txt` 含 django | Python/Django | django.md | — |
| `requirements.txt` 含 fastapi | Python/FastAPI | django.md | — |
| `go.mod` 含 gin | Go/Gin | gin.md | — |

**始终自动加载的通用规则（所有项目）：**

| 规则文件 | 何时激活 | 内容 |
|---------|---------|------|
| `rules/security.md` | **始终加载** | 密钥/注入/XSS 安全基线 |
| `rules/testing.md` | **始终加载** | 测试策略、覆盖率标准 |
| `rules/patterns.md` | **始终加载** | 代码组织模式、设计模式 |
| `rules/performance.md` | 中等/复杂任务 | N+1/内存泄漏/缓存规范 |
| `rules/git-workflow.md` | 涉及提交/分支时 | 提交规范、分支策略 |
| `rules/agents.md` | 多 Agent 调度时 | Agent 协作协议 |
| `rules/hooks.md` | 代码变更后 | PostToolUse 自动检查 |

**代码优先原则：** 项目现有代码风格 > 框架插件规范 > 通用规则默认值

---

## 🤖 步骤5：Agent 调度规则

| 任务类型 | Agent 链 | 并行/串行 |
|---------|---------|---------|
| 新功能（简单） | tdd-guide | 串行 |
| 新功能（中等） | planner → tdd-guide → code-reviewer | 串行 |
| 新功能（复杂） | architect → planner → tdd-guide → code-reviewer | 串行 |
| Bug 修复 | tdd-guide → code-reviewer | 串行 |
| 代码重构 | refactor-cleaner → code-reviewer | 串行 |
| 架构变更 | architect → planner | 串行 |
| 安全敏感 | +security-reviewer（并行审查） | 并行 |
| 文档更新 | doc-updater | 独立 |
| E2E测试 | e2e-runner | 独立 |
| 构建错误 | build-error-resolver | 独立 |
| 大型项目 | multi-agent-orchestrator 统筹 | 并行分发 |

---

## ✅ 步骤6：自动化门禁（严格执行，不可跳过）

```
1. 编译/构建  → 必须0错误
2. 单元测试   → 必须全部通过
3. 测试覆盖率 → 必须 >= 80%（Java项目: mvn test; JS: npm test）
4. 代码规范   → hooks.json 自动检查格式和质量
5. 安全扫描   → 检测硬编码密钥、SQL拼接、注入风险

任一失败 → 自动重试，最多3次，每次调整策略：
  第1次失败: 分析错误，调整实现
  第2次失败: 替代方案
  第3次失败: 报告给用户，等待干预
```

---

## 🧠 步骤7：自动经验沉淀（每次任务完成后必须触发，无需关键词）

```
任务完成后，始终执行：

1. 提取本次编码特征：
   - 使用了哪些框架模式？
   - 解决了哪类问题？
   - 采用了哪种架构决策？

2. 写入 .claude/instincts/（如 continuous-learning skill 已激活）
   或输出简短总结格式：
   [Instinct] 任务类型: xxx | 使用模式: xxx | 结果: 成功/失败

3. 如果修改了项目结构（新增模块、改变架构）：
   → 提示用户运行 /aimax:update-codemaps 更新 REPO_MAP.md

4. 如果生产环境相关（发布、部署）：
   → 自动触发 /aimax:security-scan 安全审计
```

---

## 🔄 完整闭环图

```
用户输入
    ↓
[步骤0] 会话初始化 (CLAUDE.md + REPO_MAP.md + rules)
    ↓
[步骤1] 复杂度评估 (简单/中等/复杂)
    ↓
[步骤2] 能力链选择 (命令→Agent→Skill)
    ↓
[步骤3] 意图信号→插件触发
    ↓
[步骤4] 框架插件加载 (Spring/React/Django/Gin)
    ↓
[步骤5] Agent 调度执行
    ↓
[步骤6] 自动化门禁 (编译+测试+安全)
    ↓
[步骤7] 经验沉淀 (始终自动触发)
    ↓
输出完成
```

---

**核心原则：**
1. **单一大脑** — 路由逻辑只在此文件，不分散
2. **分层清晰** — 触发(插件) → 决策(Agent) → 知识(Skill)
3. **闭环自动** — 每次完成都沉淀经验，无需用户触发
4. **项目优先** — 现有代码风格 > 插件规范 > 框架默认
5. **门禁严格** — 没有通过测试的代码不交付
