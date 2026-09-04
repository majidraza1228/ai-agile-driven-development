---
title: 'Delivery Examples'
description: Real delivery scenarios in an asset management firm — how the BMad loop runs for a quant signal pipeline, a risk dashboard, and a compliance reporting system.
---

# Delivery Examples

## Example 1 — Quant Signal Pipeline (Alpha-Generating Tool)

**Desk problem:** The PM runs a momentum strategy across 500 equities. Signal generation is manual, runs overnight in Excel, and has no audit trail. The PM wants it automated, backtestable, and able to incorporate new factor inputs without an engineering sprint.

**Who does what:**

| Step | Who | Skill |
|---|---|---|
| Shape the idea, write PRFAQ | FDE + PM | `bmad-prfaq` |
| Investment Committee review | IC | — (approval gate) |
| Write PRD with factor model requirements | FDE | `bmad-prd` |
| Risk officer validates data sourcing and model risk | Risk Officer | `bmad-prd` validate mode |
| Design data pipeline architecture (tick data → signal → order) | FDE + Architect | `bmad-architecture` |
| Architecture review | Tech Lead + Risk | — (approval gate) |
| Spec Epic 1: ingestion + normalization | Quant Dev | `bmad-spec` |
| Spec Epic 2: factor computation + backtest harness | Quant Dev | `bmad-spec` |
| Compliance sign-off on model documentation | Compliance | — (readiness gate) |
| Build Epic 1, Build Epic 2 | Quant Dev | `bmad-build` |
| Retrospective — desk runs live signals, signs off | FDE + PM | `bmad-retrospective` |

**Key FDE decisions:**
- Scoped Epic 1 and Epic 2 so the ingestion layer could be reused by other strategies — went into the architecture spine
- Pulled in the risk officer in week 1, not at the end — saved three weeks of rework on data provenance
- Cut the "dynamic factor weight UI" from MVP scope — desk validated it was not needed for signal quality

---

## Example 2 — Risk Dashboard (Operational Tool)

**Desk problem:** The risk team reviews portfolio exposure daily in a spreadsheet that takes 45 minutes to refresh. They want a live dashboard with VaR, Greeks, sector exposure, and concentration limits — with alert thresholds they can adjust themselves.

**Who does what:**

| Step | Who | Skill |
|---|---|---|
| Forge idea (fast — clear scope) | FDE | `bmad-forge-idea` |
| PRD: requirements from risk team | FDE + Risk Officer | `bmad-prd` |
| UX: wireframe of dashboard panels and alert config | Designer | `bmad-ux` |
| Architecture: real-time feed → aggregation → UI | FDE + Architect | `bmad-architecture` |
| Spec: data layer epic | Quant Dev | `bmad-spec` |
| Spec: UI + alert config epic | AI Engineer | `bmad-spec` |
| Build both epics in parallel (spine makes it safe) | Quant Dev + AI Engineer | `bmad-build` |
| Integration check between epics | FDE | `bmad-code-review` |
| Retrospective — risk team uses it live for one week | FDE + Risk Officer | `bmad-retrospective` |

**Key FDE decisions:**
- Entered the loop at `bmad-forge-idea`, not `bmad-prfaq` — the scope was already clear enough to skip IC approval
- Two epics in parallel because the architecture spine made the data contract explicit before either engineer started
- Retrospective gate required one week of live use, not just a demo — desk confirmed latency and refresh rate before sign-off

---

## Example 3 — Compliance Reporting System (Regulatory Mandate)

**Desk problem:** A new regulatory requirement mandates daily position reporting in a specific format, with a 72-hour audit trail on every change. The firm has 90 days to comply.

**Who does what:**

| Step | Who | Skill |
|---|---|---|
| PRD: mandate as input, validate mode first | FDE + Compliance | `bmad-prd` (validate → create) |
| Architecture: immutable audit log, report generation | FDE + Architect | `bmad-architecture` |
| Architecture review — compliance sign-off on audit design | Compliance + Tech Lead | — (approval gate) |
| Spec: audit log epic | Quant Dev | `bmad-spec` |
| Spec: report generation epic | AI Engineer | `bmad-spec` |
| Spec: submission pipeline epic | Quant Dev | `bmad-spec` |
| Build sequentially (audit log first — blocks the rest) | Quant Dev, AI Engineer | `bmad-build` |
| Retrospective: compliance officer runs full submission | FDE + Compliance | `bmad-retrospective` |

**Key FDE decisions:**
- Used `bmad-prd` in validate mode first — got a findings report showing three ASSUMPTION tags that needed Compliance answers before any architecture was designed
- Architecture spine made audit log immutability a mandatory constraint on all three epics — could not be opted out of per-epic
- Skipped UX skill — no user-facing interface, only a submission pipeline and a log viewer for auditors
- Sequenced epics strictly (audit log → report generation → submission) rather than parallel, because Epic 2 depended on Epic 1's schema being locked

---

## Patterns Across All Three

- **FDE decides where to enter the loop** — not every change needs a PRFAQ
- **Risk and compliance are pulled in early** — not as a gate to clear at the end
- **The architecture spine makes parallel work safe** — two engineers can build without a daily sync
- **Retrospective requires real use** — demos do not close epics in a financial context
