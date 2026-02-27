# ai-max 整合 aimax-enhanced 功能实现计划

> **版本**: 2.0
> **创建日期**: 2026-02-26
> **更新日期**: 2026-02-26
> **目标**: 将 aimax-enhanced 的高价值功能整合到 ai-max 项目中（包含 Axiom 集成）

---

## 1. 项目背景

### 1.1 ai-max 现状

**优势**：
- 完整的 **Agent 系统**（9 个专业化 Agent）
- 丰富的 **规则系统**（8 个开发规范）
- 多样的 **命令系统**（10 个命令）
- 成熟的 **Hook 系统**

**不足**：
- 插件系统需要手动配置
- 缺少任务复杂度自动评估
- TDD 流程缺少多语言模板
- 智能路由较为简单
- 缺少长期记忆和工作流系统

### 1.2 aimax-enhanced 核心能力

| 功能 | 描述 | 价值 |
|------|------|------|
| **零配置插件系统** | 自动扫描和加载插件 | 易用性 |
| **任务复杂度评估** | 简单/中等/复杂自动判断 | 智能化 |
| **六大插件集成** | TDD、前端、清理、工具、浏览器、审查 | 能力扩展 |
| **多语言测试模板** | JS/Python/Java/Go 测试模板 | 开发效率 |
| **Axiom 集成** | 长期记忆 + 复杂工作流 | **核心功能** |

### 1.3 Axiom 系统详解

**Axiom** 是一个长期记忆和复杂工作流系统，提供以下核心能力：

#### 长期记忆系统

```
.agent/
├── memory/
│   ├── project_decisions.md    # 架构决策记录
│   ├── coding_patterns.md      # 编码模式
│   └── lessons_learned.md      # 经验教训
└── workflows/
    ├── start.md                # 完整工作流
    ├── feature-flow.md         # 功能开发流
    └── evolve.md               # 知识进化流
```

#### Axiom 工作流命令

| 命令 | 功能 | 适用场景 |
|------|------|----------|
| `/start` | 完整工作流 | 复杂任务（>120分钟） |
| `/feature-flow` | 功能开发流 | 中等复杂度功能 |
| `/status` | 任务状态 | 查看当前进度 |
| `/reflect` | 复盘总结 | 任务完成后 |
| `/evolve` | 知识进化 | 更新架构决策 |
| `/analyze-error` | 错误分析 | 调试问题 |

#### Axiom 与 auto 的协作

```
用户输入复杂任务 → /auto 检测 → 建议使用 /start (Axiom)
                                ↓
                         Axiom 工作流
                                ↓
                         调用 /auto 执行具体编码
                                ↓
                         Axiom 记录决策和模式
```

### 1.4 整合目标

保持 ai-max 的 **Agent + 规则 + 命令** 核心体系，从 aimax-enhanced 提取：

1. **零配置插件系统** - 最大易用性
2. **任务复杂度评估** - 智能化核心
3. **Axiom 集成** - 长期记忆 + 工作流 **（核心功能）**
4. **多语言测试模板** - 开发效率
5. **智能路由增强** - 更智能的任务分发

---

## 2. 功能对比分析

### 2.1 命令系统对比

| 命令 | ai-max | aimax-enhanced | 整合建议 |
|------|--------|----------------|----------|
| `/auto` | 基于关键词路由 | 项目上下文 + 复杂度评估 + Axiom | **增强** |
| `/tdd` | 有流程无模板 | 多语言模板 + 门禁 | **增强** |
| `/start` | 无 | Axiom 完整工作流 | **新增** |
| `/feature-flow` | 无 | Axiom 功能开发流 | **新增** |
| `/evolve` | 无 | Axiom 知识进化 | **新增** |
| `/code-review` | 有 | 有（PR Review Toolkit） | **保留** |
| `/build-fix` | 有 | 无 | **保留** |
| `/e2e` | 有 | 无 | **保留** |
| `/test-coverage` | 有 | 无 | **保留** |
| `/refactor-clean` | 有 | 有（Code Simplifier） | **保留** |

### 2.2 能力矩阵

| 能力 | ai-max | aimax-enhanced | 整合后 |
|------|--------|----------------|--------|
| Agent 系统 | ✅ 9 个 | ❌ | ✅ 保留 |
| 规则系统 | ✅ 8 个 | ❌ | ✅ 保留 |
| 零配置插件 | ❌ | ✅ | ✅ 添加 |
| 任务复杂度评估 | ❌ | ✅ | ✅ 添加 |
| 多语言测试模板 | ⚠️ 部分 | ✅ | ✅ 增强 |
| 六大插件集成 | ❌ | ✅ | ⚠️ 参考文档 |
| **Axiom 集成** | ❌ | ✅ | ✅ **核心功能** |
| **长期记忆** | ❌ | ✅ | ✅ **添加** |
| **复杂工作流** | ❌ | ✅ | ✅ **添加** |

---

## 3. 整合方案（分阶段）

### 阶段 1：核心增强（高优先级）

#### 3.1.1 零配置插件系统

**目标**：实现自动扫描和加载插件，无需手动配置

**目录结构**：
```
ai-max/
├── plugins/
│   ├── builtin/              # 内置插件（始终加载）
│   │   ├── auto-core.md      # 智能路由核心
│   │   ├── tdd-templates.md  # TDD 多语言模板
│   │   └── code-review.md    # 代码审查规范
│   └── framework/            # 框架插件（自动发现）
│       ├── javascript/
│       │   └── react.md
│       ├── python/
│       │   └── django.md
│       ├── java/
│       │   └── spring.md
│       └── go/
│           └── gin.md
```

**插件格式**：
```markdown
---
name: react-helper
version: 1.0.0
description: React 开发助手
triggers:
  - "React"
  - "Component"
  - "JSX"
priority: 50
language: javascript
framework: react
---

# React 助手

插件内容...
```

**实现步骤**：
1. 创建 `plugins/` 目录结构
2. 编写插件扫描逻辑（在 auto.md 中）
3. 迁移 aimax-enhanced 的插件文件
4. 更新 README 文档

**文件变更**：
- 新增：`plugins/builtin/auto-core.md`
- 新增：`plugins/builtin/tdd-templates.md`
- 修改：`commands/auto.md`（添加插件扫描逻辑）
- 新增：`plugins/framework/javascript/react.md`
- 新增：`plugins/framework/java/spring.md`

---

#### 3.1.2 任务复杂度评估

**目标**：自动评估任务复杂度，智能选择处理方式

**复杂度分级**：
| 级别 | 预估时间 | 处理方式 |
|------|---------|---------|
| 🟢 简单 | < 30 分钟 | 直接实现 |
| 🟡 中等 | 30-120 分钟 | TDD 流程 + Agent 协助 |
| 🔴 复杂 | > 120 分钟 | **Axiom /start** + Planner Agent |

**评估维度**：
1. **关键词分析**：功能、模块、系统 → 复杂
2. **文件数量预估**：单文件 → 简单，多文件 → 中等/复杂
3. **依赖复杂度**：有外部依赖 → 提升级别
4. **业务逻辑**：有复杂业务规则 → 提升级别

**实现步骤**：
1. 在 `commands/auto.md` 中添加复杂度评估逻辑
2. 添加 Axiom 检测和建议逻辑
3. 更新 Agent 调用逻辑

**文件变更**：
- 修改：`commands/auto.md`
- 新增：`lib/complexity-evaluator.md`

---

#### 3.1.3 Axiom 集成（核心功能）

**目标**：完整集成 Axiom 长期记忆和工作流系统

**Axiom 检测逻辑**：
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
    → 仅使用 /auto + Agent 系统
}
```
```

**Axiom 工作流集成**：

| 场景 | 检测条件 | 行为 |
|------|---------|------|
| 简单任务 | < 30 分钟 | 直接 /auto 执行 |
| 中等任务 | 30-120 分钟 | /auto + TDD Agent |
| **复杂任务** | > 120 分钟 + 有 Axiom | **建议 /start** |
| **复杂任务** | > 120 分钟 + 无 Axiom | Planner Agent 多 Agent 协作 |

**Axiom 记忆读取**：
```markdown
## 在执行任何任务前读取 Axiom 记忆

if (存在 .agent/memory/project_decisions.md) {
    读取架构决策
    读取编码规范
    读取项目模式
}

# 确保 /auto 生成的代码符合项目既定规范
```

**实现步骤**：
1. 创建 Axiom 检测模块
2. 在 auto.md 中添加 Axiom 集成逻辑
3. 创建 Axiom 工作流命令（/start, /feature-flow, /evolve）
4. 创建 Axiom 安装脚本
5. 编写 Axiom 使用文档

**文件变更**：
- 新增：`commands/axiom-start.md`
- 新增：`commands/axiom-feature-flow.md`
- 新增：`commands/axiom-evolve.md`
- 新增：`lib/axiom-detector.md`
- 新增：`scripts/install-axiom.ps1`
- 新增：`docs/axiom-integration.md`
- 修改：`commands/auto.md`（添加 Axiom 检测和建议）

---

### 阶段 2：功能增强（中优先级）

#### 3.2.1 多语言测试模板

**目标**：为 TDD 流程添加 JS/Python/Java/Go 测试模板

**模板结构**：
```markdown
## 测试模板

### JavaScript (Jest)
```javascript
describe('Feature', () => {
  test('should do something', () => {
    // Given
    // When
    // Then
  });
});
```

### Python (pytest)
```python
def test_feature():
    # Given
    # When
    # Then
    pass
```

### Java (JUnit)
```java
@Test
@DisplayName("应该...")
void testFeature() {
    // Given
    // When
    // Then
}
```

### Go
```go
func TestFeature(t *testing.T) {
    // Given
    // When
    // Then
}
```
```

**实现步骤**：
1. 创建 `plugins/builtin/tdd-templates.md`
2. 更新 `skills/tdd-workflow/SKILL.md` 引用模板
3. 添加语言自动检测逻辑

**文件变更**：
- 新增：`plugins/builtin/tdd-templates.md`
- 修改：`skills/tdd-workflow/SKILL.md`

---

#### 3.2.2 智能路由增强

**目标**：增强 auto 命令的路由能力

**新增功能**：
1. **项目上下文检测**：自动检测语言/框架
2. **Axiom 检测**：检测项目是否有 Axiom
3. **插件自动匹配**：根据关键词加载插件
4. **Agent 自动调度**：根据任务类型选择 Agent

**路由决策树**：
```
用户输入
  ↓
第1步：项目上下文检测
  ├─ 检测语言/框架
  ├─ 检测 Axiom（.agent/）
  └─ 读取 Axiom 记忆（如有）
  ↓
第2步：复杂度评估
  ├─ 🟢 简单 → 直接实现 + 语言规范
  ├─ 🟡 中等 → TDD Agent + 代码审查
  └─ 🔴 复杂 → 检测 Axiom
               ├─ 有 Axiom → 建议 /start
               └─ 无 Axiom → Planner Agent
  ↓
第3步：插件匹配
  ├─ 检测关键词
  ├─ 加载匹配插件
  └─ 应用框架规范
  ↓
第4步：执行任务
```

**实现步骤**：
1. 重构 `commands/auto.md` 路由逻辑
2. 添加 Axiom 检测和记忆读取
3. 集成插件系统
4. 更新 Agent 调用

**文件变更**：
- 重构：`commands/auto.md`
- 新增：`lib/context-detector.md`（项目检测逻辑）
- 新增：`lib/axiom-detector.md`（Axiom 检测逻辑）

---

### 阶段 3：可选增强（低优先级）

#### 3.3.1 六大插件文档

**目标**：将 aimax-enhanced 的六大插件作为参考文档

| 插件 | 文档位置 | 用途 |
|------|---------|------|
| Superpowers | `docs/plugins/superpowers.md` | TDD + 调试参考 |
| Frontend Design | `docs/plugins/frontend-design.md` | 前端规范参考 |
| Code Simplifier | `docs/plugins/code-simplifier.md` | 清理规则参考 |
| Playground | `docs/plugins/playground.md` | HTML 工具参考 |
| Claude in Chrome | `docs/plugins/chrome.md` | 浏览器自动化参考 |
| PR Review Toolkit | `docs/plugins/pr-review.md` | 审查清单参考 |

**文件变更**：
- 新增：`docs/plugins/*.md`（6 个文档）

---

## 4. 详细实现步骤

### 4.1 阶段 1 实现（预计 3-4 小时）

#### Step 1：创建插件目录结构

```bash
# 在 ai-max 项目根目录执行
mkdir -p plugins/builtin
mkdir -p plugins/framework/javascript
mkdir -p plugins/framework/python
mkdir -p plugins/framework/java
mkdir -p plugins/framework/go
mkdir -p lib
mkdir -p scripts
```

#### Step 2：创建核心插件文件

**文件 1**：`plugins/builtin/auto-core.md`

从 aimax-enhanced 复制并适配：
- 集成 ai-max Agent 系统
- 保留插件扫描逻辑
- **添加 Axiom 检测和集成**

**文件 2**：`plugins/builtin/tdd-templates.md`

从 aimax-enhanced/skills/builtin/super-tdd.md 提取：
- 多语言测试模板
- 门禁检查
- 最佳实践

#### Step 3：创建 Axiom 集成文件

**文件 1**：`lib/axiom-detector.md`
```markdown
# Axiom 检测模块

## 检测逻辑

1. 检查 `.agent/workflows/start.md` 是否存在
2. 检查 `.agent/memory/` 目录是否存在
3. 返回 Axiom 状态

## 记忆读取

如果 Axiom 存在，读取：
- `.agent/memory/project_decisions.md`
- `.agent/memory/coding_patterns.md`
- `.agent/memory/lessons_learned.md`
```

**文件 2**：`commands/axiom-start.md`
```markdown
---
name: axiom-start
description: Axiom 完整工作流 - 复杂任务（>120分钟）
---

# /start — Axiom 完整工作流

## 触发条件

- 任务复杂度 > 120 分钟
- 项目有 Axiom（.agent/）
- 用户显式调用

## 工作流步骤

1. **需求分析** - Requirement Analyst Agent
2. **架构设计** - System Architect Agent
3. **编码实现** - 调用 /auto 技能
4. **代码审查** - Review Aggregator
5. **知识进化** - Evolution Engine
```

**文件 3**：`scripts/install-axiom.ps1`
```powershell
# Axiom 安装脚本
# 从 GitHub 克隆 Axiom 到工作空间
# 初始化 .agent/ 目录结构
```

#### Step 4：创建框架插件

**文件**：`plugins/framework/java/spring.md`

从 aimax-enhanced 复制：
- Spring Boot 代码规范
- Entity/Repository/Service/Controller 模板
- DTO 规范
- 测试规范

#### Step 5：修改 auto.md

添加以下逻辑：
1. Axiom 检测
2. 记忆读取
3. 插件扫描和加载
4. 任务复杂度评估
5. Agent 自动调度
6. Axiom 工作流建议

---

### 4.2 阶段 2 实现（预计 1-2 小时）

#### Step 1：更新 TDD Skill

修改 `skills/tdd-workflow/SKILL.md`：
- 添加对 tdd-templates.md 的引用
- 增加多语言支持说明

#### Step 2：创建项目检测文档

**文件**：`lib/context-detector.md`

```markdown
# 项目上下文检测

## 语言检测

| 语言 | 检测文件 |
|------|---------|
| JavaScript/TypeScript | package.json |
| Python | requirements.txt, pyproject.toml |
| Java | pom.xml, build.gradle |
| Go | go.mod |
| Rust | Cargo.toml |

## 框架检测

| 框架 | 检测特征 |
|------|---------|
| React | package.json 有 "react" |
| Vue | package.json 有 "vue" |
| Spring | pom.xml 有 "spring-boot" |
| Django | requirements.txt 有 "django" |

## Axiom 检测

| 检测项 | 路径 |
|--------|------|
| Axiom 工作流 | `.agent/workflows/start.md` |
| 长期记忆 | `.agent/memory/project_decisions.md` |
```

---

### 4.3 阶段 3 实现（预计 1 小时）

#### Step 1：创建插件文档

在 `docs/plugins/` 目录下创建 6 个参考文档。

#### Step 2：创建 Axiom 集成文档

**文件**：`docs/axiom-integration.md`

完整的 Axiom 集成指南：
- Axiom 系统介绍
- 安装步骤
- 工作流使用
- 记忆管理
- 最佳实践

---

## 5. 文件变更清单

### 新增文件

| 文件路径 | 描述 | 优先级 |
|---------|------|--------|
| `plugins/builtin/auto-core.md` | 智能路由核心 | P0 |
| `plugins/builtin/tdd-templates.md` | TDD 多语言模板 | P0 |
| `plugins/framework/javascript/react.md` | React 插件 | P0 |
| `plugins/framework/python/django.md` | Django 插件 | P1 |
| `plugins/framework/java/spring.md` | Spring 插件 | P0 |
| `plugins/framework/go/gin.md` | Gin 插件 | P1 |
| `lib/context-detector.md` | 项目检测逻辑 | P1 |
| `lib/axiom-detector.md` | Axiom 检测逻辑 | **P0** |
| `lib/complexity-evaluator.md` | 复杂度评估逻辑 | P0 |
| `commands/axiom-start.md` | Axiom /start 命令 | **P0** |
| `commands/axiom-feature-flow.md` | Axiom /feature-flow 命令 | **P1** |
| `commands/axiom-evolve.md` | Axiom /evolve 命令 | **P1** |
| `scripts/install-axiom.ps1` | Axiom 安装脚本 | **P0** |
| `docs/axiom-integration.md` | Axiom 集成文档 | **P0** |
| `docs/plugins/*.md` | 插件参考文档（6 个） | P2 |

### 修改文件

| 文件路径 | 修改内容 |
|---------|---------|
| `commands/auto.md` | 添加 Axiom 检测、插件扫描、复杂度评估、Agent 调度 |
| `skills/tdd-workflow/SKILL.md` | 添加多语言模板引用 |
| `README.md` | 更新功能说明，添加 Axiom 部分 |

---

## 6. 测试计划

### 6.1 功能测试

| 测试项 | 测试方法 | 预期结果 |
|--------|---------|---------|
| 插件自动扫描 | 创建新插件文件 | 自动被 auto 命令识别 |
| 任务复杂度评估 | 输入不同复杂度任务 | 正确评估并选择处理方式 |
| **Axiom 检测** | 在有 .agent/ 的项目运行 | 正确检测并建议 /start |
| **Axiom 记忆读取** | 有记忆文件时运行任务 | 自动应用项目规范 |
| 多语言测试模板 | 在不同项目运行 TDD | 使用正确的测试模板 |
| Agent 自动调度 | 输入复杂任务 | 自动调用 Planner Agent |

### 6.2 集成测试

| 测试项 | 测试方法 | 预期结果 |
|--------|---------|---------|
| auto + Agent | 运行 /auto 命令 | 正确调度 Agent |
| auto + 插件 | 在 Spring 项目运行 | 加载 spring.md 插件 |
| **auto + Axiom** | 在有 Axiom 的项目运行复杂任务 | 建议 /start |
| **Axiom /start** | 运行 /start 命令 | 完整工作流执行 |
| TDD + 模板 | 在 Java 项目运行 TDD | 使用 JUnit 模板 |

---

## 7. 风险评估

| 风险 | 可能性 | 影响 | 缓解措施 |
|------|--------|------|---------|
| 插件冲突 | 低 | 中 | 优先级机制 + 命名空间 |
| 复杂度评估不准确 | 中 | 低 | 允许用户手动指定 |
| Agent 调度错误 | 低 | 高 | 保留手动命令 |
| **Axiom 未安装** | 中 | 中 | 提供优雅降级，无 Axiom 时使用 Agent |
| **Axiom 记忆格式不兼容** | 低 | 中 | 提供记忆迁移脚本 |
| 文件结构变更 | 低 | 中 | 保持向后兼容 |

---

## 8. 验收标准

### 阶段 1 验收

- [ ] `plugins/` 目录结构创建完成
- [ ] 核心插件文件创建完成
- [ ] auto.md 包含插件扫描逻辑
- [ ] 任务复杂度评估功能正常
- [ ] **Axiom 检测功能正常**
- [ ] **Axiom /start 命令可用**
- [ ] **Axiom 记忆读取功能正常**

### 阶段 2 验收

- [ ] TDD 流程支持多语言模板
- [ ] 项目上下文检测功能正常
- [ ] Agent 自动调度功能正常
- [ ] **Axiom /feature-flow 命令可用**
- [ ] **Axiom /evolve 命令可用**

### 阶段 3 验收

- [ ] 插件参考文档创建完成
- [ ] Axiom 集成文档完善

---

## 9. Axiom 集成详细设计

### 9.1 Axiom 目录结构

```
项目根目录/
├── .agent/                        # Axiom 配置目录
│   ├── memory/                    # 长期记忆
│   │   ├── project_decisions.md   # 架构决策
│   │   ├── coding_patterns.md     # 编码模式
│   │   ├── lessons_learned.md     # 经验教训
│   │   └── api_contracts.md       # API 契约
│   ├── workflows/                 # 工作流定义
│   │   ├── start.md               # 完整工作流
│   │   ├── feature-flow.md        # 功能开发流
│   │   └── evolve.md              # 知识进化流
│   └── config.md                  # Axiom 配置
```

### 9.2 Axiom 工作流命令

#### /start — 完整工作流

```markdown
# /start — Axiom 完整工作流

## 触发条件
- 任务复杂度 > 120 分钟
- 用户显式调用
- 项目有 Axiom

## 工作流阶段

### Phase 1: 需求分析（5%）
- 分析用户需求
- 识别关键功能
- 生成用户故事

### Phase 2: 架构设计（15%）
- 设计系统架构
- 识别模块边界
- 记录架构决策

### Phase 3: 编码实现（60%）
- 调用 /auto 执行编码
- 应用项目规范
- 生成测试

### Phase 4: 代码审查（15%）
- 多维度审查
- 安全检查
- 性能分析

### Phase 5: 知识进化（5%）
- 更新项目记忆
- 记录新模式
- 提取经验教训
```

#### /feature-flow — 功能开发流

```markdown
# /feature-flow — 功能开发流

## 适用场景
- 中等复杂度功能（30-120 分钟）
- 需要结构化开发流程

## 工作流阶段

### Phase 1: 设计（20%）
- 设计接口
- 规划数据结构

### Phase 2: 实现（60%）
- 调用 /auto 编码
- 生成测试

### Phase 3: 审查（20%）
- 代码审查
- 更新记忆
```

#### /evolve — 知识进化

```markdown
# /evolve — 知识进化

## 触发时机
- 完成复杂任务后
- 发现新模式时
- 架构变更时

## 进化内容
- 更新 project_decisions.md
- 添加 coding_patterns.md
- 记录 lessons_learned.md
```

### 9.3 Axiom 与 Agent 系统集成

```
┌─────────────────────────────────────────────────────────────┐
│                      /auto 命令                              │
├─────────────────────────────────────────────────────────────┤
│  1. 检测项目上下文                                           │
│     ├─ 语言/框架检测                                         │
│     └─ Axiom 检测                                            │
│                                                              │
│  2. 读取 Axiom 记忆（如有）                                  │
│     ├─ project_decisions.md                                  │
│     ├─ coding_patterns.md                                    │
│     └─ lessons_learned.md                                    │
│                                                              │
│  3. 评估任务复杂度                                           │
│     ├─ 简单 → 直接实现                                       │
│     ├─ 中等 → Agent 协助                                     │
│     └─ 复杂 →                                                │
│         ├─ 有 Axiom → 建议 /start                            │
│         └─ 无 Axiom → Planner Agent                          │
│                                                              │
│  4. 执行任务                                                 │
│     ├─ 加载匹配插件                                          │
│     ├─ 应用项目规范                                          │
│     └─ 调用 Agent                                            │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                    /start (Axiom)                           │
├─────────────────────────────────────────────────────────────┤
│  Phase 1: 需求分析                                           │
│     └─ 可能调用 Explore Agent                                │
│                                                              │
│  Phase 2: 架构设计                                           │
│     └─ 调用 Architect Agent                                  │
│                                                              │
│  Phase 3: 编码实现                                           │
│     └─ 调用 /auto（递归）                                    │
│                                                              │
│  Phase 4: 代码审查                                           │
│     └─ 调用 Code Reviewer Agent                              │
│                                                              │
│  Phase 5: 知识进化                                           │
│     └─ 更新 .agent/memory/                                   │
└─────────────────────────────────────────────────────────────┘
```

---

## 10. 后续维护

### 版本管理

- 遵循语义化版本规范
- 每次更新记录 CHANGELOG
- 保持与 aimax-enhanced 的同步（可选）

### 扩展方向

1. 添加更多框架插件（Vue、Angular、FastAPI 等）
2. 增强 Agent 协作能力
3. 支持自定义插件开发
4. **增强 Axiom 记忆能力**
5. **添加 Axiom 工作流可视化**
6. 集成更多开发工具

---

## 11. 附录

### A. aimax-enhanced 文件清单

```
aimax-enhanced/
├── skills/
│   ├── builtin/
│   │   ├── aimax-auto-core.md    # 智能路由核心
│   │   ├── auto.md               # auto 命令
│   │   ├── super-tdd.md          # TDD 流程
│   │   ├── auto-tdd.md           # TDD 命令
│   │   ├── code-simplifier.md    # 代码清理
│   │   ├── auto-simplify.md      # 清理命令
│   │   ├── pr-review.md          # PR 审查
│   │   └── auto-review.md        # 审查命令
│   └── plugins/
│       ├── javascript/react.md
│       ├── python/django.md
│       ├── java/spring.md
│       ├── go/gin.md
│       └── custom/example-plugin.md
```

### B. 整合优先级

| 优先级 | 功能 | 原因 |
|--------|------|------|
| P0 | 零配置插件系统 | 最大易用性提升 |
| P0 | 任务复杂度评估 | 智能化核心 |
| **P0** | **Axiom 集成** | **长期记忆 + 工作流核心能力** |
| P1 | 多语言测试模板 | 开发效率 |
| P1 | 智能路由增强 | 整体体验 |
| P2 | 六大插件文档 | 参考价值 |

### C. Axiom GitHub 仓库

- **地址**: https://github.com/Boundary-Correction/Axiom
- **用途**: 长期记忆和工作流系统
- **安装**: `git clone https://github.com/Boundary-Correction/Axiom D:\workSpace\Axiom`

---

**文档结束**

> **下一步**：用户确认后，开始执行阶段 1 的实现（包含 Axiom 集成）
