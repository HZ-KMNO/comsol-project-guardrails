# 🛡️ COMSOL 项目护栏技能

🖼️ <img src="assets/logo.png" alt="COMSOL 项目护栏徽标" width="220">

🌐 [阅读英文说明](README.md)

🤖 这是一个面向所有人工智能代理的 COMSOL Multiphysics 项目护栏型技能。

🧭 它适用于 MPH 文件、COMSOL Java API 脚本、参数扫描、求解器调试、粒子追踪、冲蚀与腐蚀模拟、结果导出、报告生成、演示文稿制作以及项目文件清理等任务。

## 🚧 这个技能主要避免什么问题

🧪 避免误用旧的 COMSOL 结果或过时导出图片。

🏷️ 避免直接假设 `std1`、`pg1`、`er1`、`comp1` 等模型标签存在。

🧩 避免混淆“结果数据集”和“绘图视图”。

📏 避免把工程代理量当成真实求解出的物理量。

🗂️ 避免把旧 CSV、旧图片、旧标题和新报告内容混在一起。

🎞️ 避免用同一张图片或动画代表多个仿真工况。

📝 避免覆盖用户已经手工调整好的 DOCX 或 PPTX 排版。

🧹 避免在没有检查脚本引用关系前删除文件。

## 📦 仓库内容

📄 `SKILL.md` 是真正的技能核心内容。

🌍 `README.md` 是英文项目说明。

🇨🇳 `README.zh-CN.md` 是中文项目说明。

⚙️ `agents/openai.yaml` 是给 Codex 和 OpenAI 风格技能界面使用的可选展示配置。

🖼️ `assets/logo.png` 是本仓库说明中使用的徽标。

🧩 其他人工智能代理可以忽略 `agents/openai.yaml`，直接使用 `SKILL.md`。

## 💻 在 Codex 中使用

📁 将整个文件夹放到 `~/.codex/skills/comsol-project-guardrails/`。

🚀 之后 Codex 在处理 COMSOL 自动化、结果导出、报告生成或文件清理任务时，就可以使用这个技能。

## 🧠 在 Claude Code 中使用

📁 如果要在 Claude Code 中使用，可以把文件夹放到 `~/.claude/skills/comsol-project-guardrails/`。

📌 Claude Code 只需要 `SKILL.md`，可以忽略 `agents/openai.yaml`。

## 🤝 在其他人工智能代理中使用

📘 如果使用其他人工智能代理系统，可以直接复制或引用 `SKILL.md` 作为操作指南。

🧭 这个技能是平台中立的，重点是 COMSOL 工作流、验证、交付物追踪和风险规避，而不是某一个特定代理平台。

## ✅ 推荐使用场景

🔧 在人工智能代理修改 COMSOL MPH 文件前使用。

☕ 在人工智能代理编写或运行 COMSOL Java API 脚本前使用。

📊 在人工智能代理执行参数扫描或优化前使用。

🧯 在人工智能代理调试 COMSOL 求解器收敛、变量缺失或数据集错误前使用。

🖼️ 在人工智能代理导出 COMSOL 图片、GIF、CSV、DOCX 或 PPTX 前使用。

🧹 在人工智能代理清理 COMSOL 项目文件夹前使用。

🧾 在人工智能代理总结多阶段仿真结果前使用。

🧱 这个技能是通用工作流护栏，不包含任何具体项目的仿真数据。

## 📝 说明

📚 这个仓库不能替代 COMSOL 官方文档或工程判断。

🔎 遇到不确定的 COMSOL API、求解器或物理设置时，仍应先检查模型树、求解日志和官方文档。
