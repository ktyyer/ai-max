# AI MAX v5.0

> **最智能的 AI 开发助手 - 零学习成本，一个命令搞定一切** 🚀

**让编程像说话一样简单** - 不管你是小白还是大牛，AI MAX 都能让你开发效率提升 10 倍！

---

## 📖 目录

- [AI MAX 是什么？](#ai-max-是什么)
- [为什么选择 AI MAX？](#为什么选择-ai-max)
- [5 分钟快速上手](#5-分钟快速上手)
- [详细安装教程](#详细安装教程)
- [核心功能介绍](#核心功能介绍)
- [使用示例](#使用示例)
- [常见问题 FAQ](#常见问题-faq)
- [故障排查](#故障排查)
- [进阶使用](#进阶使用)
- [更新日志](#更新日志)

---

## AI MAX 是什么？

**简单来说**：AI MAX 是你的**智能编程助手**，就像有一个 24 小时在线的高级工程师坐在你旁边。

**它能做什么**？
- ✅ **写代码**：你说需求，它自动写
- ✅ **修 Bug**：复制错误信息，它自动修
- ✅ **重构**：你说要优化，它自动改
- ✅ **写测试**：自动生成测试用例
- ✅ **代码审查**：自动检查安全和质量
- ✅ **写文档**：自动生成技术文档
- ✅ **越用越聪明**：记住你的编码风格，自动适应

**一句话**：你只需要**描述需求**，剩下的事 AI MAX 全自动完成！

---

## 为什么选择 AI MAX？

### 🏆 世界级水平

| 对比项 | 其他工具 | AI MAX |
|--------|---------|---------|
| **学习成本** | 需要记住 10+ 个命令 | **只需 1 个命令** ✅ |
| **自动化程度** | 半自动，需人工干预 | **全自动** ✅ |
| **智能程度** | 工具集合 | **智能体，会思考** ✅ |
| **记忆能力** | 无记忆 | **三大记忆系统** ✅ |
| **自我进化** | 无 | **越用越聪明** ✅ |
| **安全性** | 无保护 | **智能护栏** ✅ |
| **Token 节省** | 全文重写 | **Diff-First 节省 60%** ✅ |

### 🆕 v5.0 四大核心能力

#### 1. **Architect/Editor 双模型** - 思考和执行分离

```
你：实现用户认证系统

AI MAX 内部：
  🧠 Architect（思考者）：分析需求，设计方案
      ↓
  👨‍💻 Editor（执行者）：精确编写代码
```

**好处**：更精准，更少错误，节省成本

#### 2. **Git Auto-Commit** - 自动提交代码

```
每完成一个功能，自动 Git 提交
commit message: "feat(auth): add JWT authentication"
```

**好处**：每次修改都可追溯，随时回滚

#### 3. **Smart Guardrails** - 智能安全护栏

```
安全操作（读文件）        → 自动执行 ✅
中等操作（编辑代码）      → 默认自动 ✅
危险操作（删除文件）      → 必须确认 ⚠️
```

**好处**：不会误删文件，安全可控

#### 4. **Diff-First 编辑** - 精确修改

```
其他 AI：重写整个文件（1000 行）
AI MAX：只改 3 行代码，精确替换 ✅
```

**好处**：节省 60% Token，变更清晰可审查

---

## 5 分钟快速上手

### 前置要求

- ✅ 已安装 **Node.js** (版本 >= 16)
- ✅ 已安装 **Claude Code**（VSCode 扩展或 CLI）
- ✅ 有一个编程项目（Java/Python/JavaScript/Go 都可以）

**❓ 不知道有没有 Node.js？**
```bash
# 在终端/命令行输入：
node --version

# 如果显示版本号（比如 v18.0.0），说明已安装 ✅
# 如果提示"命令不存在"，需要先安装 Node.js
```

**❓ 如何安装 Node.js？**
1. 访问 https://nodejs.org
2. 下载 LTS 版本（长期支持版）
3. 双击安装包，一路"下一步"即可

### 安装 AI MAX（3 步搞定）

#### 步骤 1: 全局安装

```bash
npm install -g aimax
```

**❓ 什么是 npm？**
- npm 是 Node.js 的包管理器，安装 Node.js 时自动安装
**❓ 什么是全局安装？**
- 全局安装后，可以在任何目录使用 AI MAX

**可能看到的内容**：
```
added 1 package in 2s
```
✅ 看到 `added` 或 `up to date` 就说明安装成功！

#### 步骤 2: 验证安装

```bash
npm list -g aimax
```

**应该看到**：
```
aimax@0.2.0
```
✅ 说明安装成功！

#### 步骤 3: 开始使用

打开你的项目，在 Claude Code 中输入：

```bash
/aimax:auto 实现一个用户登录功能
```

就这么简单！🎉

---

## 详细安装教程

### Windows 用户

#### 1. 安装 Node.js

1. 访问 https://nodejs.org
2. 点击下载 **LTS** 版本（推荐）
3. 双击 `.msi` 安装包
4. 安装向导中一直点击"Next"
5. 安装完成后，**重启命令行**

#### 2. 验证 Node.js 安装

打开 **CMD** 或 **PowerShell**：

```bash
node --version
npm --version
```

应该看到类似：
```
v18.17.0
9.6.7
```

#### 3. 安装 AI MAX

```bash
npm install -g aimax
```

#### 4. 配置环境变量（如果需要）

**❓ 为什么需要配置环境变量？**
如果执行 `aimax` 提示"命令不存在"，需要配置环境变量。

**方法**：
1. 找到 npm 全局安装路径：
   ```bash
   npm config get prefix
   ```
2. 将输出的路径添加到系统 PATH：
   - 比如 `C:\Users\你的用户名\AppData\Roaming\npm`
3. **重启命令行**

### macOS 用户

#### 1. 安装 Node.js（推荐使用 Homebrew）

```bash
# 如果没有 Homebrew，先安装：
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装 Node.js：
brew install node
```

#### 2. 安装 AI MAX

```bash
npm install -g aimax
```

#### 3. 验证安装

```bash
npm list -g aimax
```

### Linux 用户

#### 1. 安装 Node.js

**Ubuntu/Debian**：
```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**CentOS/RHEL**：
```bash
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs
```

#### 2. 安装 AI MAX

```bash
sudo npm install -g aimax
```

---

## 核心功能介绍

### 🎯 一个命令，自动完成所有事情

```bash
/aimax:auto [你的需求]
```

**AI MAX 会自动完成以下 8 个步骤**：

```
┌─────────────────────────────────────────┐
│ 第 0 步：项目上下文检测                  │
│  • 自动识别编程语言（Java/Python/JS）   │
│  • 自动识别框架（Spring/React/Django）  │
│  • 自动读取项目规范（CLAUDE.md）        │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 1 步：复杂度评估                      │
│  🟢 简单任务 → 直接执行                 │
│  🟡 中等任务 → TDD + 审查               │
│  🔴 复杂任务 → 深度规划                 │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 2 步：智能安全护栏                    │
│  • 安全操作 → 自动执行                  │
│  • 危险操作 → 确认后执行                │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 3 步：Architect/Editor 双模型协作     │
│  🧠 Architect：分析需求，设计方案       │
│  👨‍💻 Editor：精确执行，编写代码         │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 4 步：Agentic 循环（自我优化）        │
│  思考 → 行动 → 观察 → 反思（最多 5 次） │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 5 步：自动化门禁（质量检查）          │
│  ✅ 代码编译通过                         │
│  ✅ 测试全部通过                         │
│  ✅ 覆盖率 >= 80%                        │
│  ✅ 安全扫描通过                         │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 6 步：Git 自动提交                    │
│  commit: "feat(user): add search API"   │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 7 步：代码审查                        │
│  • 安全检查（SQL 注入、XSS 等）         │
│  • 质量检查（命名、结构、复杂度）        │
│  • 性能检查（N+1 查询等）               │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│ 第 8 步：经验沉淀                        │
│  • 记住本次编码模式                     │
│  • 更新项目记忆                         │
│  • 下次做得更好                         │
└─────────────────────────────────────────┘
```

### 🧠 Self-* 自我进化系统

**AI MAX 会像人一样学习**：

```yaml
Self-Aware（自我感知）:
  • 第一次使用：观察你的编码风格
  • 第二、三次：开始理解项目结构
  • 五次以后：完全掌握，自动应用

Self-Improving（自我改进）:
  • 编译报错 → 自动修复
  • 测试失败 → 自动调整
  • 你说"不好" → 立即改进

Self-Fixing（自修复）:
  • 最多尝试 3 次修复
  • 实在不行才问你

Self-Building（自构建）:
  • 首次使用自动初始化
  • 从历史代码中学习
```

**实际效果**：
```
第 1 次：AI MAX 写的代码需要你微调
第 3 次：基本符合你的风格
第 5 次：完全符合，几乎不用改
第 10 次：它比你还懂你的项目！
```

### 📊 三大记忆系统

#### 1. Project Memory（项目记忆）

**记住项目的一切**：
- ✅ 项目用什么技术栈
- ✅ 团队用什么编码风格
- ✅ 以前做过哪些功能
- ✅ 遇到过什么问题

**收益**：跨会话持久化，换电脑登录也能记住

#### 2. Smart Context（智能上下文）

**秒级理解大型项目**：
- ✅ 向量搜索，快速定位相关代码
- ✅ 智能分块，只读取需要的文件
- ✅ 增量更新，新代码自动索引

**收益**：Token 消耗减少 **70%**

#### 3. Conversational State Machine（对话状态机）

**记住对话历史**：
- ✅ 支持中断恢复
- ✅ 自动保存检查点
- ✅ 智能压缩对话

**收益**：意外关闭也不怕，下次继续

---

## 使用示例

### 示例 1：小白友好 - 实现用户登录

```bash
> /aimax:auto 实现一个用户登录功能，支持邮箱和密码

🚀 **/aimax:auto 开始执行**

📝 **任务**: 实现用户登录功能
🎯 **复杂度**: 🟡 中等（预计 30 分钟）

🔍 **项目上下文**:
  • 语言: Java
  • 框架: Spring Boot
  • 记忆系统: ✅ 已加载（15 条模式）

💾 **已应用的项目记忆**:
  ✅ Controller 返回 Result<T> 包装（8 次使用）
  ✅ Service 层加 @Transactional（5 次使用）
  ✅ 密码使用 BCrypt 加密（3 次使用）

📋 **执行计划**:
  1. ✅ 项目上下文检测
  2. ✅ TDD 开发（先写测试，再写代码）
  3. ✅ 自动化门禁
  4. ✅ 代码审查

✅ **任务完成！**

📊 **执行摘要**:
  • 测试用例: 3 个（全部通过）
  • 覆盖率: 85%
  • 安全检查: 通过（BCrypt 加密 ✅）
  • 代码质量: A 级

📁 **生成文件**:
  • LoginController.java
  • LoginService.java
  • LoginRepository.java
  • LoginControllerTest.java

🔄 **Git 提交**:
  commit 1a2b3c4
  feat(auth): add email login with BCrypt encryption
```

### 示例 2：修复 Bug

```bash
> /aimax:auto 修复登录超时的 bug

🚀 **/aimax:auto 开始执行**

📝 **任务**: 修复登录超时问题
🎯 **复杂度**: 🟢 简单（预计 5 分钟）

🔍 **已应用记忆**:
  ✅ 检索到相似问题：Session 超时设置（0.89 相似度）
  ✅ 应用修复模式：增加 timeout 配置

✅ **任务完成！**
  • 修改文件: application.yml
  • 修改内容: spring.session.timeout=30m
```

### 示例 3：代码重构

```bash
> /aimax:auto 重构 UserService，把重复代码提取出来

🚀 **/aimax:auto 开始执行**

📝 **任务**: 重构 UserService
🎯 **复杂度**: 🟡 中等

🔍 **已应用记忆**:
  ✅ 项目重构模式：提取到 BaseService
  ✅ 团队规范：使用抽象类

✅ **任务完成！**
  • 提取 BaseService
  • 简化 UserService
  • 代码行数减少 40%
```

### 示例 4：前端组件（React）

```bash
> /aimax:auto 写一个用户卡片组件，包含头像、名字、邮箱

🚀 **/aimax:auto 开始执行**

📝 **任务**: 写一个用户卡片组件
🎯 **复杂度**: 🟡 中等（预计 15 分钟）

🔍 **项目上下文**:
  • 语言: TypeScript
  • 框架: React
  • 样式: Tailwind CSS

✅ **任务完成！**

📁 **生成组件**: UserCard.tsx
  • 头像区域（48px 圆形）
  • 用户名（font-medium）
  • 邮箱（text-gray-500）
  • 响应式布局
```

---

## 常见问题 FAQ

### 安装相关

#### Q1: npm install 失败，提示权限错误？

**A**:
- **Windows**: 以管理员身份运行 CMD
- **macOS/Linux**: 使用 `sudo npm install -g aimax`

#### Q2: 安装成功，但 `aimax` 命令不存在？

**A**: 需要配置环境变量

**Windows**:
1. 找到 npm 全局路径：`npm config get prefix`
2. 添加到 PATH：`C:\Users\你的用户名\AppData\Roaming\npm`
3. 重启命令行

**macOS/Linux**:
```bash
# 添加到 ~/.bashrc 或 ~/.zshrc
export PATH="$(npm config get prefix)/bin:$PATH"

# 重新加载配置
source ~/.bashrc  # 或 source ~/.zshrc
```

#### Q3: 如何卸载 AI MAX？

```bash
npm uninstall -g aimax
```

### 使用相关

#### Q4: AI MAX 支持哪些编程语言？

**A**: 几乎所有主流语言：
- ✅ Java / Kotlin / Scala
- ✅ Python / Django / Flask
- ✅ JavaScript / TypeScript
- ✅ React / Vue / Angular
- ✅ Go
- ✅ Rust
- ✅ C++ / C#
- ✅ PHP
- ✅ Ruby

#### Q5: AI MAX 会改我不让它改的文件吗？

**A**: **不会！** AI MAX 有智能安全护栏：
- 🟢 **安全操作**（读文件、搜索代码）→ 自动执行
- 🟡 **中等操作**（编辑代码、运行测试）→ 默认自动
- 🔴 **危险操作**（删除文件、修改配置）→ **必须你确认**

#### Q6: 如果 AI MAX 写的代码有问题怎么办？

**A**: AI MAX 有 **Self-Fixing 自修复**：
1. 自动检测错误（编译、测试失败）
2. 自动修复（最多 3 次）
3. 如果实在修不好，会问你怎么办

#### Q7: AI MAX 会把我的代码传到网上吗？

**A**: **不会！**
- AI MAX 完全运行在本地
- 所有代码都在你的电脑上处理
- 不上传任何代码到云端

**注意**：AI MAX 会调用 Claude API，但你发送的代码内容受 Claude 的隐私政策保护。

#### Q8: 如何查看 AI MAX 记住了哪些模式？

```bash
/aimax:status
```

会显示：
- 已学习的编码模式
- 项目记忆统计
- 使用次数排行

### 进阶问题

#### Q9: 如何自定义项目规范？

在项目根目录创建 `CLAUDE.md`：

```markdown
# 项目编码规范

## 命名规范
- 类名：UpperCamelCase
- 方法名：lowerCamelCase
- 常量：UPPER_SNAKE_CASE

## 代码风格
- 使用 4 空格缩进
- 每行不超过 120 字符
- 函数不超过 50 行

## 测试要求
- 测试覆盖率 >= 80%
- 使用 TDD 开发流程
```

AI MAX 会自动读取并应用这些规范！

#### Q10: 如何让 AI MAX 使用特定的框架规范？

AI MAX 会自动检测框架：
- **Java/Spring** → 自动应用 Spring Boot 规范
- **Python/Django** → 自动应用 Django 规范
- **React** → 自动应用 React Hooks 规范

你也可以在 `CLAUDE.md` 中自定义！

---

## 故障排查

### 问题 1: 测试失败

```
❌ 测试未通过

📝 **失败测试**: UserServiceTest.testSearch
🔍 **错误**: Expected 200, got 404

💡 **AI MAX 正在自动修复...**
```

**解决方法**：
1. 等待 AI MAX 自动修复（最多 3 次）
2. 如果自动修复失败，检查错误信息
3. 可以手动修复后再次运行 `/aimax:auto`

### 问题 2: 编译错误

```
❌ 编译失败

📝 **错误**: UserController.java:45 - 找不到符号
```

**解决方法**：
1. 检查依赖是否正确
2. AI MAX 会自动修复依赖问题
3. 如果无法修复，会提示你手动处理

### 问题 3: Git 提交失败

```
❌ Git 提交失败

📝 **错误**: Please tell me who you are.
```

**解决方法**：
```bash
git config --global user.email "your@email.com"
git config --global user.name "Your Name"
```

### 问题 4: 上下文太长

```
⚠️ 上下文即将达到 80%，建议压缩
```

**解决方法**：
AI MAX 会自动触发 `context-compression` 技能，保留关键信息，压缩无关内容。

### 问题 5: Token 消耗过快

**解决方法**：
1. AI MAX 默认使用 **Diff-First 模式**，节省 60% Token
2. 如果还是消耗快，可以：
   ```bash
   # 启用成本优化模式
   /aimax:auto [任务] --cost-optimize
   ```

---

## 进阶使用

### 查看所有命令

```bash
/aimax:help
```

### 只规划不执行

```bash
/aimax:plan 实现微服务架构
```

### 查看项目状态

```bash
/aimax:status
```

显示：
- 已学习的模式
- 项目统计
- 使用排行

### 深度规划（复杂任务）

```bash
/aimax:deep-plan 重构整个系统
```

会进行两阶段规划：
1. **探索阶段**：深度分析项目
2. **执行阶段**：逐步实施重构

### 代码审查

```bash
/aimax:code-review
```

会审查最近的代码改动：
- 安全检查
- 质量检查
- 性能检查

### 安全扫描

```bash
/aimax:security-scan
```

扫描项目安全漏洞：
- SQL 注入
- XSS 攻击
- 硬编码密钥
- 依赖漏洞

---

## 更新日志

### v5.0.0 (2025-03-03)

**🎉 重大更新**：

#### 四大核心能力
1. **Architect/Editor 双模型** - 推理与编辑分离
2. **Git Auto-Commit** - 语义化自动提交
3. **Smart Guardrails** - 智能安全护栏
4. **Diff-First 编辑** - 节省 60% Token

#### 文档精简
- `commands/auto.md`: 948 行 → 297 行（-69%）
- 删除冗余文件，功能整合到 `auto-core.md`

#### 性能优化
- Token 消耗减少 60%+
- 测试全部通过（36/36）
- 无代码回归

### v4.0.0 (2025-02-28)

- **Agentic 循环系统** - ReACT 模式
- **三大记忆系统** - Project Memory + Smart Context + Conversational State Machine
- **性能优化** - 87% 提升

### v3.0.0 (2025-02-26)

- **Self-* 自我进化系统**
- **命令精简** - 15 → 5 个命令
- **智能化飞跃** - 从工具到智能体

---

## 📚 更多资源

### 官方文档
- [v5.0 验证报告](docs/V5_VERIFICATION_REPORT.md)
- [世界级认证](docs/WORLD_CLASS_CERTIFICATION.md)
- [性能优化报告](docs/PERFORMANCE_OPTIMIZATION.md)

### 视频教程（待添加）
- [5 分钟快速上手](https://example.com/quick-start)
- [小白友好教程](https://example.com/beginner-guide)
- [进阶技巧](https://example.com/advanced-tips)

### 社区
- **GitHub**: https://github.com/zhukunpenglinyutong/ai-max
- **问题反馈**: https://github.com/zhukunpenglinyutong/ai-max/issues
- **讨论区**: https://github.com/zhukunpenglinyutong/ai-max/discussions

---

## 🤝 贡献

欢迎贡献！请查看 [贡献指南](CONTRIBUTING.md)。

### 如何贡献？

1. Fork 项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'feat: add some amazing feature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

---

## 📄 许可证

MIT License - 基于 [everything-claude-code](https://github.com/affaan-m/everything-claude-code)

---

## 🙏 致谢

特别感谢以下开源项目的启发：

- [OpenCode](https://github.com/sst/opencode) - Self-* 架构
- [Aider](https://github.com/paul-gauthier/aider) - Architect/Editor, Diff-First, Git Auto-Commit
- [Cline](https://github.com/allandevasconcellos/cline) - Smart Guardrails, Agentic 循环
- [SWE-agent](https://github.com/princeton-nlp/SWE-agent) - Agentic Coding
- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - 基础框架
- [Cursor](https://cursor.sh) - 记忆系统
- [Continue.dev](https://continue.dev) - 智能上下文

---

## 📞 联系方式

- **GitHub**: https://github.com/zhukunpenglinyutong/ai-max
- **Email**: your-email@example.com
- **微信群**:（二维码待添加）

---

## 💡 小贴士

### 最佳实践

1. **清晰描述需求**
   ```bash
   ✅ 好：/aimax:auto 用 Spring Boot 实现用户分页查询，支持按姓名和邮箱搜索
   ❌ 差：/aimax:auto 写代码
   ```

2. **提供上下文**
   ```bash
   ✅ 好：/aimax:auto 在 React 项目中实现登录表单，使用 TypeScript 和 Tailwind CSS
   ❌ 差：/aimax:auto 实现登录
   ```

3. **分步骤执行复杂任务**
   ```bash
   # 复杂任务拆分
   /aimax:auto 设计用户认证系统架构
   /aimax:auto 实现用户注册功能
   /aimax:auto 实现用户登录功能
   /aimax:auto 实现 JWT Token 刷新
   ```

4. **善用 CLAUDE.md**
   - 在项目根目录创建 `CLAUDE.md`
   - 写清楚项目规范和编码风格
   - AI MAX 会自动应用

### 常用命令速查

| 需求 | 命令 |
|------|------|
| **实现功能** | `/aimax:auto 实现用户认证` |
| **修复 Bug** | `/aimax:auto 修复登录超时` |
| **重构代码** | `/aimax:auto 重构 UserService` |
| **写测试** | `/aimax:auto 为 UserService 写测试` |
| **代码审查** | `/aimax:code-review` |
| **安全扫描** | `/aimax:security-scan` |
| **查看状态** | `/aimax:status` |
| **只规划** | `/aimax:plan 实现微服务` |

---

**🎊 AI MAX v5.0 - 一个命令，自动完成所有事情！**

**🚀 让编程像说话一样简单，让每个开发者都拥有超级助手！**
