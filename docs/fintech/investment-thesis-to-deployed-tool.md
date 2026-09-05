---
title: Investment Thesis to Deployed Quant Tool
description: How to move a trading or alpha thesis from desk intent to a deployed quant system.
---

# Investment Thesis to Deployed Quant Tool

## When To Use This

- The desk wants a new signal pipeline, model, or trading support tool.
- The work starts as investment intent rather than a software request.
- Risk and compliance need auditability before build starts.

## Workflow

1. FDE captures the thesis, user, market context, and desired edge.
2. FDE writes the PRFAQ if committee approval is needed.
3. Investment Committee reviews the concept.
4. FDE turns the approved concept into a PRD.
5. Risk Officer validates assumptions, data sources, and model risk.
6. FDE writes the architecture spine for data, model, and deployment flow.
7. Engineering writes one spec per epic.
8. Compliance clears the readiness gate.
9. Build, backtest, verify, and deploy.
10. Run the retrospective with the desk and record the verdict.

## Outputs

- PRFAQ
- PRD
- Architecture spine
- Epic specs
- Readiness checklist
- Retrospective verdict

## Notes

Keep the investment thesis as the source of truth. If the thesis changes, update the PRD first and regenerate downstream artifacts.

