---
name: simple-harness-engineering
description: >
  用简洁方式将仓库转化为适合 AI 编程工具工作的 Harness Engineering 工作区。
  当用户想创建或改进项目级 Agent 指令、沉淀仓库知识、强化 AGENTS.md
  或 CLAUDE.md、添加可执行治理检查、减少隐藏上下文，或让 AI 应用项目
  更适合 Codex、Claude Code、OpenClaw 及类似编程 Agent 协作时，使用本技能。
metadata:
  primary_prompt: Agent.md
  safe_default: single-pass
  requires_human_approval_for:
    - destructive_file_operations
    - credential_or_secret_access
    - production_deployments
    - branch_protection_changes
---

# SimpleHarnessEngineering 技能

本技能将 `Agent.md` 中的通用系统提示词包装为 OpenClaw 风格入口。它刻意保持轻量：它帮助 Agent 改进项目周围的 harness（工程约束环境），但不声称宿主平台已经强制实现沙箱、工具路由、密钥脱敏或自治多 Agent 编排。

## 何时使用

当任务涉及以下情况时，使用本技能：

- 创建或改进 AI 编程 Agent 指令。
- 按 Harness Engineering 思路审计仓库缺口。
- 将关键项目知识从聊天记录迁移到仓库内文件。
- 创建 `AGENTS.md`、`CLAUDE.md`、架构文档、工作流文档、质量文档、产品规格或执行计划。
- 将只存在于文字中的规则升级为测试、脚本、CI 检查、schema、模板或 lint 规则。
- 让项目更适合 Codex、Claude Code、OpenClaw 或类似 AI 编程工具使用。

## 启动顺序

1. 根据目标工具读取 `Agent.md`。
2. 读取仓库已有指令，尤其是 `AGENTS.md`、`CLAUDE.md`、`README.md` 和顶层文档。
3. 先检查项目结构，再提出新结构。
4. 判断当前任务需要只改文档、添加可执行检查，还是两者都需要。

## 运行模式

默认使用 `single-pass` 模式：

- 端到端完成用户当前请求。
- 保持任务范围窄。
- 只添加能减少当前歧义或防止重复错误的 harness 工件。
- 除非宿主平台和用户都明确支持，否则不要启动连续自治循环。

对成熟仓库，应保留现有结构，并做增量加固。对空仓库，默认使用 `Agent.md` 中描述的首次启动脚手架。

## 安全边界

本技能以指令为主，无法单独强制工具权限、分支保护、沙箱或密钥脱敏。这些能力应由宿主平台负责。

在高影响工作之前，确认或提示以下边界：

- 不读取或提交密钥与凭据路径。
- 破坏性文件操作需要明确的人类批准。
- 生产部署需要明确的人类批准。
- main 或 trunk 分支变更必须经过审查。
- 任何连续自治或多 Agent 模式都必须有平台级监控和恢复机制。

如果这些保护不可用或不清楚，保持在人类监督的 `single-pass` 模式，并说明限制。

## 交付物

根据任务需要，产出以下一项或多项：

- 更新后的 `Agent.md`。
- 简短的工具专用 `AGENTS.md`、`CLAUDE.md` 或 OpenClaw 入口。
- 缺失的仓库内事实来源文档。
- 复杂工作的执行计划。
- 可复用的规格、计划、ADR、交接或审查模板。
- 能强制重要规则的验证脚本或 CI 检查。
- 简洁说明当前已经机械化约束了什么，以及哪些仍依赖人类或平台纪律。

## 内置审核清单

审计或复查仓库时，检查以下要点：

- `Agent.md` 是否可直接作为系统提示词使用。
- 目标项目是否已有简短的 `AGENTS.md` 或 `CLAUDE.md` 项目地图。
- 重要产品、架构、质量、安全和运维知识是否已经进入仓库。
- 重复规则是否有机会升级为测试、脚本、lint、schema、CI 或运行时 guardrail。
- 文档是否描述当前项目，而不是想象中的未来项目。
- 验证命令是否真实可运行，而不是占位符。
- 密钥、凭据、生产部署和破坏性操作是否有人类审批边界。
