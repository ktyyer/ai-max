# 开源能力对齐与升级清单

本文档记录“已落地能力”和“下一批可落地能力”，用于持续提升 AI 辅助开发、自主开发与自动进化能力。

## 已落地（本轮）

1. 自主演进插件：`plugins/builtin/adaptive-evolution.md`
2. 通用演进技能：`.aimax/skills/builtin/auto-evolution.md`
3. 专用命令：`commands/evolve.md`
4. CI 门禁模板：`templates/ci/aimax-evolution-gates.yml`
5. PR 自动评估注释模板：`templates/ci/aimax-pr-eval-comment.yml`
6. 任务状态机编排：`commands/loop.md` + `plugins/builtin/task-state-machine.md` + `src/loop-state-machine.js`
7. 自动路由接入：`commands/auto.md` + `README.md` + `auto-core` 映射

## 借鉴来源（开源）

- OpenAI Evals: https://github.com/openai/evals
- SWE-agent: https://github.com/SWE-agent/SWE-agent
- Aider: https://github.com/Aider-AI/aider
- LangGraph: https://github.com/langchain-ai/langgraph
- Continue: https://github.com/continuedev/continue
- Promptfoo: https://github.com/promptfoo/promptfoo
- LiteLLM: https://github.com/BerriAI/litellm
- MCP Servers: https://github.com/modelcontextprotocol/servers
- MCP git connector: https://github.com/modelcontextprotocol/servers/tree/main/src/git

## 下一批优先升级项（按价值排序）

1. `仓库地图缓存`
- 目标：为大仓库缓存模块关系图，减少重复上下文扫描
- 借鉴：Aider 的 repo map 思路

2. `多模型路由策略`
- 目标：根据任务类型自动选模型，失败时 fallback
- 借鉴：LiteLLM 的 routing/retry/fallback

3. `评估集分层`
- 目标：为不同项目建立 smoke/regression/perf 三层评估集
- 借鉴：OpenAI Evals 的评估驱动方法

## 建议推进节奏

1. 第 1 周：仓库地图缓存（低风险高收益）
2. 第 2 周：多模型路由（核心能力增强）
3. 第 3 周：分层评估集（高级能力）
