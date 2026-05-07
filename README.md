# SimpleHarnessEngineering

简易 Harness Engineering 提示词项目。它的目标是保持使用足够简单：把 `Agent.md` 加载(粘贴）到 Codex、Claude Code 或其他 AI 编程工具的系统提示词中，就能让工具按 Harness Engineering 的方式辅助项目开发。

## 最小使用方式

必须做的只有两件事：

1. 打开目标项目。
2. 将 [Agent.md](Agent.md) 的完整内容粘贴到编程工具的系统提示词、自定义指令或项目级指令中。

然后直接提出任务即可，例如：

```text
请按照 SimpleHarnessEngineering 的方式审计这个项目，找出最影响 Agent 开发效率的 3 个缺口，并给出最小改进方案。
```

不强制你提前创建 `AGENTS.md`、`CLAUDE.md`、架构文档、测试脚本或 CI。Agent 会在任务需要时建议或创建这些文件。

## 文件说明

- `Agent.md`：核心系统提示词。日常使用只需要它。
- `SKILL.md`：OpenClaw 风格技能入口。只有在 OpenClaw/ClawHub 场景下需要。

## 如何在 Codex 中使用

1. 打开目标项目仓库。
2. 将 `Agent.md` 的内容放入 Codex 的系统提示词、自定义指令或项目级指令。
3. 直接描述目标任务。
4. 如果是已有项目，要求增量改进，不要重建项目结构。
5. 如果是空项目，让 Codex 根据 `Agent.md` 的“新项目默认建议”提出最小脚手架。

## 如何在 Claude Code 中使用

1. 将 `Agent.md` 的内容放入 Claude Code 的项目级指令。
2. 如果目标项目已有 `CLAUDE.md`，让它保持简短，只作为项目地图。
3. 对复杂任务，要求 Claude Code 创建执行计划并在完成前汇报真实运行过的验证命令。

## 如何在 OpenClaw 中使用

1. 将本项目作为技能包使用，入口是 `SKILL.md`。
2. OpenClaw 激活技能后，应先读取 `SKILL.md`，再读取 `Agent.md`。
3. 默认保持 `single-pass` 模式。除非宿主平台能确认沙箱、权限控制、密钥屏蔽、人类审批、监控和恢复机制，否则不要开启连续自治或多 Agent 自治模式。

## 什么时候需要更多文件

一开始不需要。只有当它们能减少歧义、降低重复沟通或支撑验证时，才创建更多文件：

- `AGENTS.md` 或 `CLAUDE.md`：目标项目的简短地图。
- `ARCHITECTURE.md`：架构边界和关键技术选择。
- `WORKFLOW.md`：任务、验证、审查和发布流程。
- `docs/plans/`：复杂任务的执行计划。
- 测试脚本或 CI：把重复规则机械化。

## 这个项目不是什么

- 不是完整自治运行时。
- 不包含平台级沙箱、工具路由、权限系统或多 Agent 调度器。
- 不要求一次性生成大量文档。
- 不替代目标项目自己的测试、构建、部署和安全机制。

## 维护原则

- 保持 `Agent.md` 足够短，能直接复制粘贴。
- `SKILL.md` 只服务 OpenClaw 风格技能打包，不承载大量重复内容。
- 新增文件前先确认它是否真的能降低使用成本。
