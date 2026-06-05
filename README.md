# 🛡️ COMSOL Project Guardrails Skill

<p align="center">
  <img src="assets/logo.png" alt="COMSOL Project Guardrails logo" width="220">
</p>

🌐 [Chinese version](README.zh-CN.md)

💡 A vendor-neutral skill for AI agents working on COMSOL Multiphysics projects.

💡 It provides practical guardrails for MPH files, COMSOL Java API scripts, parameter sweeps, solver debugging, particle tracing, erosion/corrosion simulations, result exports, reports, slide decks, and project cleanup.

## 🎯 What This Skill Helps Prevent

- ✅ Reusing stale COMSOL results or old exported figures
- ✅ Assuming wrong model tags such as `std1`, `pg1`, `er1`, or `comp1`
- ✅ Confusing plot views with solution datasets
- ✅ Presenting engineering proxy values as directly solved physical quantities
- ✅ Mixing old CSV data, figures, captions, and report conclusions
- ✅ Reusing one case image or animation for multiple simulation cases
- ✅ Overwriting manually adjusted reports or PPT layouts
- ✅ Deleting files before checking whether scripts or reports still reference them

## 🗂️ Repository Contents

```text
comsol-project-guardrails/
|-- SKILL.md
|-- README.md
|-- README.zh-CN.md
|-- agents/
|   `-- openai.yaml
`-- assets/
    `-- logo.png
```

💡 `SKILL.md` contains the actual skill instructions.

💡 `agents/openai.yaml` is optional metadata for Codex/OpenAI-style skill interfaces. Other agents can ignore it.

## 🚀 Use With Codex

💡 Place this folder under your Codex skills directory:

```text
~/.codex/skills/comsol-project-guardrails/
```

💡 Codex can then use the skill when working on COMSOL automation, exports, reports, or cleanup tasks.

## 🚀 Use With Claude Code

💡 Claude Code skills are also based on `SKILL.md`. To use this skill with Claude Code, place it under:

```text
~/.claude/skills/comsol-project-guardrails/
```

💡 Only `SKILL.md` is required for Claude Code. The `agents/openai.yaml` file can be ignored.

## 🚀 Use With Other AI Agents

💡 For other AI agent systems, copy or reference `SKILL.md` as an operating guide. The skill is written to be agent-agnostic: it focuses on workflow, verification, and artifact traceability rather than a specific platform.

## 🚀 Recommended Use

💡 Use this skill before an agent:

- ✅ modifies an MPH file
- ✅ writes or runs COMSOL Java API scripts
- ✅ performs parameter sweeps or optimization
- ✅ debugs COMSOL solver convergence or missing variables
- ✅ exports COMSOL plots, GIFs, CSV files, DOCX reports, or PPTX slides
- ✅ cleans up a COMSOL project folder
- ✅ summarizes results from a multi-stage simulation workflow

💡 The skill is intentionally generic and does not contain project-specific simulation data.

## 📝 Notes

💡 This repository is a workflow guardrail, not a replacement for COMSOL documentation or engineering judgment. For uncertain COMSOL API behavior, agents should still inspect the model tree and consult official COMSOL documentation.
