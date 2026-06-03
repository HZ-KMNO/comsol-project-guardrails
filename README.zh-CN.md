# COMSOL Project Guardrails Skill

这是一个面向 AI agent 的 COMSOL 项目护栏型 skill，用于帮助 agent 在处理 COMSOL Multiphysics 项目时减少常见错误。

它适用于 MPH 文件、COMSOL Java API 脚本、参数扫描、粒子追踪、冲蚀/腐蚀模拟、结果导出、报告生成、PPT 制作以及项目文件清理等任务。

[English README](README.md)

## 这个 Skill 主要避免什么问题

- 误用旧的 COMSOL 结果或过时导出图片
- 直接假设 `std1`、`pg1`、`er1`、`comp1` 等模型标签存在
- 混淆“结果数据集”和“绘图视图”
- 把工程代理量当成真实求解出的物理量
- 把旧 CSV、旧图片、旧标题和新报告内容混在一起
- 覆盖用户已经手工调整好的 DOCX 或 PPTX 排版
- 在没有检查脚本引用关系前删除文件

## 仓库内容

```text
comsol-project-guardrails/
├── SKILL.md
├── README.md
├── README.zh-CN.md
└── agents/
    └── openai.yaml
```

`SKILL.md` 是真正的 skill 核心内容。

`agents/openai.yaml` 是给 Codex/OpenAI 风格 skill 界面使用的可选展示配置。Claude Code 不需要这个文件。

## 在 Codex 中使用

将整个文件夹放到 Codex skills 目录中，例如：

```text
~/.codex/skills/comsol-project-guardrails/
```

之后 Codex 在处理 COMSOL 自动化、结果导出、报告生成或文件清理任务时，就可以使用这个 skill。

## 在 Claude Code 中使用

Claude Code 的 skill 也基于 `SKILL.md`。如果要在 Claude Code 中使用，可以把文件夹放到：

```text
~/.claude/skills/comsol-project-guardrails/
```

Claude Code 只需要 `SKILL.md`。`agents/openai.yaml` 可以忽略。

## 推荐使用场景

建议在以下任务开始前使用这个 skill：

- 修改 COMSOL MPH 文件
- 编写或运行 COMSOL Java API 脚本
- 执行参数扫描或多工况计算
- 导出 COMSOL 图片、GIF、CSV、DOCX 或 PPTX
- 清理 COMSOL 项目文件夹
- 总结多阶段仿真结果

## 说明

这个 skill 是通用工作流护栏，不包含任何具体项目的仿真数据。

它不能替代 COMSOL 官方文档或工程判断。遇到不确定的 COMSOL API、求解器或物理设置时，仍应先检查模型树、求解日志和官方文档。
