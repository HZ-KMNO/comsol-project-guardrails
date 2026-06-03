---
name: comsol-project-guardrails
description: Use when any AI agent works on COMSOL Multiphysics MPH files, COMSOL Java API scripts, model cleanup, parameter sweeps, solver debugging, particle tracing, erosion/corrosion simulations, result exports, DOCX/PPTX reports, or COMSOL project handoffs. Provides guardrails to avoid stale results, wrong tags, unsafe cleanup, unclear proxy variables, invalid plots, and report-image mismatches.
---

# COMSOL Project Guardrails

## Core Principle

Treat every COMSOL task as a traceable simulation workflow, not a file-editing task. Identify the authoritative model and data, inspect the model tree, make one controlled change at a time, rerun or redraw the necessary result, and verify the exported artifact before reporting it.

This skill is vendor-neutral. It is intended for any AI agent that can inspect files, run commands, write scripts, use COMSOL batch tools, or edit reports.

## Agent Operating Contract

- State what is known, what is inferred, and what still needs verification.
- Prefer read-only inspection before mutation.
- Write a small audit/probe script before writing a large modifying script.
- Do not rely on memory of a previous run when the model, folder, or report may have changed.
- Keep a chain from input parameters to MPH/study/dataset to exported table/image to report/chart/conclusion.
- Continue debugging until acceptance criteria are met, or report unmet criteria with logs and evidence.
- Preserve source models, source scripts, validated data, final reports, and files referenced by automation.

## Task Intake Guardrails

Before starting a COMSOL automation or simulation task, collect or discover:

- COMSOL version and the COMSOL-bundled Java/runtime path.
- Authoritative MPH file path, or a clean work directory for a new model.
- Local COMSOL documentation locations if available: Application Programming Guide, Reference Manual, Java API index, and `ModelUtil` API page.
- Any relevant MCP/tooling repository or helper server. Treat it as optional until installed and verified.
- Physics objective, geometry assumptions, material assumptions, parameter ranges, study type, and expected outputs.
- Quantitative acceptance criteria such as loss, imbalance, pressure drop, erosion rate, convergence tolerance, stress limit, or figure quality.
- Final deliverables such as saved MPH, CSV/KPI tables, figures/GIFs, DOCX report, PPTX slides, or cleanup requirements.

Do not hard-code sample local paths into reusable scripts or skills. Use user-provided paths, discovered paths, or placeholders such as `<COMSOL_ROOT>` and `<PROJECT_DIR>`.

If the prompt lacks measurable acceptance criteria, ask for them or propose reasonable criteria before running long optimizations.

## Standard Workflow

1. **Find authoritative files.** Locate active MPH files, scripts, exported data, figures, reports, and folders. Do not update an old duplicate because it is easier to open.
2. **Audit before editing.** Enumerate components, physics, features, studies, datasets, plots, exports, selections, parameters, variables, and result tags.
3. **Preserve user work.** If the user manually adjusted plots, views, labels, reports, or folders, patch only requested parts. Avoid broad "repair all" scripts unless explicitly requested.
4. **Change one layer at a time.** Separate parameter edits, geometry/physics edits, solver edits, result-node edits, export edits, and report edits.
5. **Verify from fresh outputs.** A successful script exit code is not proof. Check logs, timestamps, nonempty CSVs, visible images, plausible values, and document references.
6. **Record evidence.** Every KPI, chart point, GIF frame, report figure, or conclusion should trace back to a current simulation case, dataset, or exported table.

## Model Tree Audit Checklist

Before editing or exporting, enumerate:

- Model label, file path, COMSOL version, and intended save target.
- Components, dimensions, geometry sequences, work planes, selections, and coordinate systems.
- Parameters, variables, functions, interpolation tables, and units.
- Materials and assigned domains/boundaries.
- Physics interfaces, features, boundary selections, feature labels, and API tags.
- Mesh sequences, local mesh refinements, boundary layers, and mesh status.
- Studies, study steps, parametric sweeps, time lists, solver sequences, and active/inactive steps.
- Solution datasets, derived datasets, deformed geometry datasets, particle datasets, and time/parameter indices.
- Result groups, plot features, views, exports, tables, animations, and report nodes.

Save or print a compact audit log for complex tasks so later agents can verify what was actually present.

## COMSOL API And Solver Guardrails

- Use the COMSOL-provided Java/runtime and the project-known `comsolcompile` or `comsolbatch` pattern. Normal system Java usually cannot load COMSOL APIs correctly.
- Prefer official local COMSOL references when available: Application Programming Guide for automation workflow, Reference Manual for properties/features, Java API index for class documentation, and `ModelUtil` for model load/save and server lifecycle.
- Query tags and labels before setting properties. COMSOL labels may be renamed while API tags remain machine-generated.
- When an API property is uncertain, write a tiny probe script to list available properties/tags. Do not guess plot, export, feature, or solver property names.
- Confirm study activation, solution datasets, time lists, parameter sweeps, and solver logs. A grayed, inactive, stale, or wrong dataset can silently produce misleading plots.
- For transient flow or particle tracing, set release time, time step, and observation time from the physical travel scale. Do not reuse one trajectory result for different velocities or operating conditions.
- For small geometric features, narrow gaps, or localized hotspots, use mesh refinement, refined sampling, and local zoom checks before trusting maxima or hotspot locations.
- If a result is zero, undefined, nonphysical, or unstable, diagnose the cause: wrong variable, wrong boundary, missing feature, inactive study, stale dataset, inadequate mesh/time step, or model limitation.
- If a simplified model cannot directly compute a quantity, label the replacement as an engineering proxy. Define formula, unit, source variables, and interpretation. Never present a proxy as a directly solved physical variable.
- State simplifications honestly, especially 2D geometry, missing solid domains, missing collision statistics, uncoupled physics, mapped loads, or omitted chemistry.

## Recommended Script Pattern

For fragile COMSOL work, split automation into small scripts:

1. **Audit script:** load MPH and print model tags, studies, datasets, plots, parameters, and exports. No mutation.
2. **Patch script:** change only one logical layer, such as parameters, solver settings, result labels, or export settings.
3. **Solve/export script:** run the intended study or redraw/export the intended result groups.
4. **Validation script:** check expected files, table row counts, KPI ranges, image dimensions, timestamps, and logs.

This pattern is slower than one huge script but faster than debugging an opaque script that changed everything at once.

## Parameters, Units, And Physical Sanity

- Do not change original parameter values casually. If a parameter must change, record why and keep names/descriptions clear.
- Parameter tables need units and plain-language descriptions.
- Check scales before solving: geometry size, particle size, wavelength, velocity, pressure, viscosity, conductivity, time step, total time, mesh size, and material properties.
- Compare outputs with expected physical trends. If a trend contradicts basic physics, suspect setup or dataset errors before writing conclusions.
- For optimization tasks, keep a case manifest with parameter values, run status, solver outcome, exported file paths, and acceptance metrics.
- For parametric sweeps, confirm that each output is tied to the correct parameter index before sorting, averaging, or plotting.

## Multi-Case And Optimization Guardrails

- Create one output folder or manifest row per case. Include case ID, parameter values, study name, dataset tag, and timestamp.
- Do not represent multiple cases with one reused plot, image, or GIF unless it is explicitly labeled as a schematic.
- For transient or moving-particle cases, adapt the time step and observation time to each case's expected travel time.
- Stop using any metric that is repeatedly zero, undefined, or nonphysical unless the model has been fixed or the metric is explicitly removed from the objective.
- Distinguish actual simulation results from post-processed engineering estimates.

## Results, Views, And Exports

- Distinguish **dataset** from **view**. Camera, axis range, and zoom only change presentation; they do not prove the plot uses the correct solution, deformed frame, or time step.
- After changing a dataset, expression, view, or legend setting, force the plot to redraw before exporting.
- For each plot, set a concise title, unit, legend, max/min display when useful, dataset, selection, time/parameter case, axis/camera view, background, antialiasing, and export resolution.
- Use macro and micro views when both global context and local mechanism matter. Do not replace missing context by changing captions.
- Transparent PNGs can render badly in Word/PPT or image viewers. If a white academic page is required, verify the image on a white background.
- Never reuse copied images, GIFs, or chart points as evidence for another case. Multi-case outputs must come from actual per-case simulations or clearly documented derived data.
- For animations, verify frame source, time range, camera/view lock, scale synchronization, and whether every frame comes from the intended case.
- For local maxima/minima near small features, use local selections, refined sampling, or mesh refinement before trusting a single coarse-grid value.

## Figure Quality Guardrails

- Titles should be short and meaningful. Avoid raw internal names in final figures.
- Units should be visible in legends, axes, color bars, tables, and captions.
- Check legibility at final report/slide size, not only at full-screen size.
- Keep COMSOL result figures, external charts, and schematic diagrams visually distinct and correctly labeled.
- If external tools redraw data charts, preserve the exported numerical data and state that the chart is externally formatted.

## Reports, PPT, And Charts

- Use current exported CSV/tables as chart sources. Include units in table headers and axes.
- In reports and slides, describe the observed result first, then provide mechanism-based interpretation.
- Do not overclaim beyond simulation evidence.
- Remove known-bad zero, failed, placeholder, or obsolete results from final deliverables unless they are explicitly discussed as limitations.
- When regenerating DOCX/PPTX, do not overwrite carefully arranged user layouts unless asked. Patch captions, text, and images in place when possible.
- After inserting figures into DOCX/PPTX, inspect the document text and representative slides/pages to ensure image, caption, and discussion match.
- Prefer concise conclusions tied to verified metrics. Include limitations for geometry simplification, boundary conditions, material assumptions, solver tolerances, and missing physics.
- If a deliverable is for presentation, convert figure descriptions into result analysis. Avoid slide text that only says what a figure is.

## Cleanup And Handoff

- Before deleting or renaming, scan scripts, reports, manifests, and document generators for references. A stale-looking file may still be part of the workflow.
- Delete conservatively and explicitly. Avoid recursive or wildcard deletion unless the user specifically approves it and the project rules allow it.
- After cleanup, update scripts and notes so future agents do not chase removed paths.
- Keep a final handoff note with active model path, key scripts, current outputs, known limitations, and results intentionally removed.

## Common Failure Modes

- The script edits a label, but later code addresses an API tag that is different.
- A result group displays a correct-looking view but uses an old dataset or wrong time step.
- A report includes images from an older run because filenames were reused.
- A transient simulation finishes early or stops changing because the time list, solver step, or dataset was not updated.
- A high-quality figure export fails visually because the view/camera/export node was not tied to the correct plot group.
- A cleanup removes files needed by report generators or rerun scripts.
- An agent satisfies "file exists" but never checks whether the image/table/document content is visible and current.

## Completion Checklist

- Active MPH/script path confirmed.
- Model tags, studies, datasets, plots, exports, and parameters inspected.
- Intended studies solved or plots redrawn from current datasets.
- Logs checked for solver failures, undefined variables, empty selections, stale datasets, and export errors.
- KPI values are nonempty, unit-labeled, and physically plausible.
- Figures/GIFs/CSVs/DOCX/PPTX exist, have current timestamps, and contain visible/current content.
- Reports avoid stale values, unclear proxies, and unsupported conclusions.
- If multiple cases were run, each case has its own verified data source or manifest entry.
- If cleanup was performed, references to removed files were checked.
- Final response states what changed, what was verified, and what was intentionally left unchanged.
