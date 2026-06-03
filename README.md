# COMSOL Project Guardrails Skill

[中文版本](README.zh-CN.md)

A lightweight skill for agents working on COMSOL Multiphysics projects.

It provides practical guardrails for handling MPH files, COMSOL Java API scripts, parameter sweeps, particle tracing, corrosion/erosion simulations, result exports, reports, slide decks, and project cleanup.

## What This Skill Helps Prevent

- Reusing stale COMSOL results or old exported figures
- Assuming wrong model tags such as `std1`, `pg1`, `er1`, or `comp1`
- Confusing plot views with solution datasets
- Presenting engineering proxy values as directly solved physical quantities
- Mixing old CSV data, figures, captions, and report conclusions
- Overwriting manually adjusted reports or PPT layouts
- Deleting files before checking whether scripts or reports still reference them

## Repository Contents

```text
comsol-project-guardrails/
├── SKILL.md
└── agents/
    └── openai.yaml
```

`SKILL.md` contains the actual skill instructions.

`agents/openai.yaml` is optional metadata for Codex/OpenAI-style skill interfaces. Claude Code does not need this file.

## Use With Codex

Place this folder under your Codex skills directory, for example:

```text
~/.codex/skills/comsol-project-guardrails/
```

Codex can then use the skill when working on COMSOL automation, exports, reports, or cleanup tasks.

## Use With Claude Code

Claude Code skills are also based on `SKILL.md`. To use this skill with Claude Code, place it under:

```text
~/.claude/skills/comsol-project-guardrails/
```

Only `SKILL.md` is required for Claude Code. The `agents/openai.yaml` file can be ignored.

## Recommended Use

Use this skill before an agent:

- modifies an MPH file
- writes or runs COMSOL Java API scripts
- performs parameter sweeps
- exports COMSOL plots, GIFs, CSV files, DOCX reports, or PPTX slides
- cleans up a COMSOL project folder
- summarizes results from a multi-stage simulation workflow

The skill is intentionally generic and does not contain project-specific simulation data.

## Notes

This repository is a workflow guardrail, not a replacement for COMSOL documentation or engineering judgment. For uncertain COMSOL API behavior, agents should still inspect the model tree and consult official COMSOL documentation.
