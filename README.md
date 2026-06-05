# 🛡️ COMSOL Project Guardrails Skill

🖼️ <img src="assets/logo.png" alt="COMSOL Project Guardrails logo" width="220">

🌐 [Read the Chinese README](README.zh-CN.md)

🤖 A vendor-neutral skill for AI agents working on COMSOL Multiphysics projects.

🧭 It provides practical guardrails for MPH files, COMSOL Java API scripts, parameter sweeps, solver debugging, particle tracing, erosion/corrosion simulations, result exports, reports, slide decks, and project cleanup.

## 🚧 What This Skill Helps Prevent

🧪 Reusing stale COMSOL results or old exported figures.

🏷️ Assuming wrong model tags such as `std1`, `pg1`, `er1`, or `comp1`.

🧩 Confusing plot views with solution datasets.

📏 Presenting engineering proxy values as directly solved physical quantities.

🗂️ Mixing old CSV data, figures, captions, and report conclusions.

🎞️ Reusing one case image or animation for multiple simulation cases.

📝 Overwriting manually adjusted reports or PPT layouts.

🧹 Deleting files before checking whether scripts or reports still reference them.

## 📦 Repository Contents

📄 `SKILL.md` contains the actual skill instructions.

🌍 `README.md` provides the English project overview.

🇨🇳 `README.zh-CN.md` provides the Chinese project overview.

⚙️ `agents/openai.yaml` is optional metadata for Codex/OpenAI-style skill interfaces.

🖼️ `assets/logo.png` is the repository logo used in this README.

🧩 Other agents can ignore `agents/openai.yaml` and use `SKILL.md` directly.

## 💻 Use With Codex

📁 Place this folder under `~/.codex/skills/comsol-project-guardrails/`.

🚀 Codex can then use the skill when working on COMSOL automation, exports, reports, or cleanup tasks.

## 🧠 Use With Claude Code

📁 Place this folder under `~/.claude/skills/comsol-project-guardrails/` if you want to use it with Claude Code.

📌 Only `SKILL.md` is required for Claude Code, and `agents/openai.yaml` can be ignored.

## 🤝 Use With Other AI Agents

📘 Copy or reference `SKILL.md` as an operating guide for other AI agent systems.

🧭 The skill is written to be agent-agnostic: it focuses on workflow, verification, and artifact traceability rather than a specific platform.

## ✅ Recommended Use

🔧 Use this skill before an agent modifies an MPH file.

☕ Use this skill before an agent writes or runs COMSOL Java API scripts.

📊 Use this skill before an agent performs parameter sweeps or optimization.

🧯 Use this skill before an agent debugs COMSOL solver convergence or missing variables.

🖼️ Use this skill before an agent exports COMSOL plots, GIFs, CSV files, DOCX reports, or PPTX slides.

🧹 Use this skill before an agent cleans up a COMSOL project folder.

🧾 Use this skill before an agent summarizes results from a multi-stage simulation workflow.

🧱 The skill is intentionally generic and does not contain project-specific simulation data.

## 📝 Notes

📚 This repository is a workflow guardrail, not a replacement for COMSOL documentation or engineering judgment.

🔎 For uncertain COMSOL API behavior, agents should still inspect the model tree and consult official COMSOL documentation.
