---
name: comsol-project-guardrails
description: Use when working on COMSOL Multiphysics MPH files, COMSOL Java API scripts, model cleanup, parameter sweeps, particle tracing, corrosion/erosion simulations, result exports, DOCX/PPTX reports, or COMSOL project handoffs. Provides concise guardrails to avoid stale results, wrong tags, unsafe cleanup, unclear proxy variables, invalid plots, and report-image mismatches.
---

# COMSOL Project Guardrails

## Core Principle

Treat every COMSOL task as a traceable simulation workflow, not a file-editing task. First identify the authoritative model/data, then inspect the model tree, make one controlled change at a time, rerun or redraw the necessary result, and verify the exported artifact before reporting it.

## Workflow

1. **Find the authoritative files first.** Locate the active MPH, scripts, exported data, figures, reports, and folders. Do not update an old duplicate because it happens to be easier to open.
2. **Audit before editing.** Enumerate components, physics, features, studies, datasets, plots, exports, selections, parameters, variables, and result tags. Do not assume tags such as `std1`, `pg1`, `er1`, or `comp1`.
3. **Preserve user work.** If the user manually adjusted plots, views, labels, reports, or folders, patch only the requested parts. Avoid broad “repair all” scripts unless explicitly requested.
4. **Change one logical layer at a time.** Separate parameter edits, geometry/physics edits, solver edits, result-node edits, export edits, and report edits. After each layer, run a small verification.
5. **Verify from fresh outputs.** A successful script exit code is not proof. Check logs, modification times, nonempty CSVs, visible images, plausible values, and correct document references.
6. **Keep an audit trail.** Every KPI, chart point, GIF frame, report figure, or conclusion should trace back to a current simulation case, dataset, or exported table.

## COMSOL API And Solver Guardrails

- Use the COMSOL-provided Java/runtime and the project’s known `comsolcompile`/`comsolbatch` pattern. Normal system Java usually cannot load COMSOL APIs correctly.
- Query tags and labels before setting properties. COMSOL labels may be renamed by users while API tags remain machine-generated.
- When an API property is uncertain, write a tiny probe script to list available properties/tags. Do not guess plot, export, feature, or solver property names.
- Confirm study activation, solution datasets, time lists, parameter sweeps, and solver logs. A grayed, inactive, stale, or wrong dataset can silently produce misleading plots.
- For transient flow or particle tracing, set release time, time step, and observation time from the physical travel scale. Do not reuse one trajectory result for different velocities or operating conditions.
- If a result is zero, undefined, nonphysical, or unstable, diagnose the cause: wrong variable, wrong boundary, missing feature, inactive study, stale dataset, inadequate mesh/time step, or model limitation. Do not hide it inside the report.
- If a simplified model cannot directly compute a quantity, label the replacement as an engineering proxy. Define formula, unit, source variables, and interpretation. Never present a proxy as a directly solved physical variable.
- State simplifications honestly, especially 2D geometry, missing solid domains, missing collision statistics, uncoupled physics, or mapped loads.

## Parameters, Units, And Physical Sanity

- Do not change original parameter values casually. If a parameter must change, record why and keep names/descriptions clear.
- Parameter tables need units and plain-language descriptions. Avoid cryptic names without comments.
- Check scales before solving: geometry size, particle size, velocity, pressure, viscosity, conductivity, time step, total time, mesh size, and material properties.
- Compare outputs with expected physical trends. If higher velocity does not increase pressure drop, particle speed, or erosion tendency when it should, suspect setup or dataset errors before writing conclusions.

## Results, Views, And Exports

- Distinguish **dataset** from **view**. Camera, axis range, and zoom only change presentation; they do not prove the plot uses the correct solution, deformed frame, or time step.
- After changing a dataset, expression, view, or legend setting, force the plot to redraw before exporting.
- For each plot, set a concise title, unit, legend, max/min display if needed, dataset, selection, time/parameter case, axis/camera view, background, antialiasing, and export resolution.
- Use macro and micro views when both global context and local mechanism matter. Do not replace missing context by changing captions.
- Transparent PNGs can render badly in Word/PPT or image viewers. If a white academic page is required, verify the image on white background.
- Never reuse copied images, GIFs, or chart points as evidence for another case. Multi-case outputs must come from actual per-case simulations or clearly documented derived data.

## Reports, PPT, And Charts

- Use current exported CSV/tables as the source for charts. Include units in table headers and axes.
- In reports and slides, describe the observed result first, then give the mechanism-based interpretation. Do not overclaim beyond the simulation evidence.
- Remove known-bad zero, failed, placeholder, or obsolete results from final deliverables unless they are explicitly discussed as limitations.
- When regenerating DOCX/PPTX, do not overwrite carefully arranged user layouts unless asked. Patch captions, text, and images in place when possible.
- After inserting figures into DOCX/PPTX, inspect the document text and at least representative slides/pages to ensure image, caption, and discussion match.

## Cleanup And Handoff

- Before deleting or renaming, scan scripts, reports, manifests, and document generators for references. A stale-looking file may still be part of the workflow.
- Delete conservatively and explicitly. Avoid recursive or wildcard deletion unless the user specifically approves it and the project rules allow it.
- After cleanup, update scripts and notes so future agents do not chase removed paths.

## Completion Checklist

- Active MPH/script path confirmed.
- Model tags, studies, datasets, plots, exports, and parameters inspected.
- Intended studies solved or plots redrawn from current datasets.
- Logs checked for solver failures, undefined variables, empty selections, stale datasets, and export errors.
- KPI values are nonempty, unit-labeled, and physically plausible.
- Figures/GIFs/CSVs/DOCX/PPTX exist, have current timestamps, and contain visible/current content.
- Reports avoid stale values, unclear proxies, and unsupported conclusions.
- Final response states what changed, what was verified, and what was intentionally left unchanged.
