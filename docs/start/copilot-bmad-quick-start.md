---
title: BMad Quick Start for Copilot
description: Start using BMad in Copilot after setup with the shortest useful path.
---

BMad gives Copilot a repeatable workflow: ask for guidance, choose the right
skill, then keep the result in the repo where the next step can use it.

## Fast path

1. Install BMad with `npx bmad-method install`.
2. Open the repo in Copilot.
3. Run `bmad-help` when you want the next step.
4. Run `bmad-build` when you already know the change you want.

## Common first commands

| Command | Use it when |
| --- | --- |
| `bmad-help` | You want the next best BMad action |
| `bmad-project-context` | You need Copilot to understand an existing codebase |
| `bmad-build` | You want to turn a clear request into code |
| `bmad-prd` | You need to shape a larger idea before implementation |

## A simple Copilot loop

1. Ask `bmad-help` for the next step.
2. Use the suggested skill.
3. Let BMad write artifacts into `_bmad` or `docs/`.
4. Return to Copilot with the saved context.

## When to start with planning

Start with planning if the work needs a product decision, architecture choice,
or UX direction. Skip straight to build when the change is already clear and
small.
