---
title: 'AI-Driven Agile for Asset Management & Hedge Funds'
description: How the BMad Method maps to the delivery needs of asset management firms and hedge funds — from investment thesis to deployed system.
---

# AI-Driven Agile for Asset Management & Hedge Funds

## Why Standard Agile Falls Short in Finance

Most agile frameworks were designed for product companies. In a hedge fund or asset management firm, the constraints are different:

- **The "customer" is the portfolio manager or trader**, not an external user. Their time is expensive and their tolerance for process friction is low.
- **Decisions carry financial and regulatory weight.** A bad architecture choice in a quant model is not a tech-debt problem — it is a risk event.
- **Speed and rigor must coexist.** The desk needs fast iteration. Risk and compliance need audit trails and reproducibility.
- **Requirements are not written down.** Investment intent lives in a PM's head, in a Bloomberg terminal, and in a trading strategy — not in a Jira ticket.

BMad Method solves this by making decisions explicit at the right moments, sizing the process to the work, and giving every role a clear lane.

## The Delivery Loop in a Hedge Fund Context

```
Investment Idea / Desk Problem
        ↓
  [FDE + PM] Shape & PRFAQ
        ↓
  Investment Committee ← approval gate
        ↓
  PRD (investment thesis as product requirements)
        ↓
  [Risk Officer] PRD Validate ← approval gate
        ↓
  UX + Architecture (data pipelines, model infra, UI)
        ↓
  [Architecture Review] ← approval gate
        ↓
  Spec per epic (one spec per quant model / tool / dashboard)
        ↓
  [Readiness Gate] ← compliance check
        ↓
  Build → Backtest / Validate → Deploy
        ↓
  [Retrospective] FDE + desk sign-off ← approval gate
        ↓
  Next epic or course correction
```

## What BMad Preserves for Finance

| Concern | How BMad Addresses It |
|---|---|
| Audit trail | Every decision lives in a versioned document with a named owner. |
| Regulatory sign-off | Five explicit approval gates with written artifacts — ready for audit. |
| Reproducibility | Architecture spine records every cross-epic decision. No undocumented tribal knowledge. |
| Speed | Small, clear changes go straight to Build. Planning depth scales to risk, not habit. |
| Parallel teams | One PRD, one architecture spine, one spec per epic. Multiple engineers cannot diverge. |
| Changing requirements | Update the PRD, propagate to specs. The change path is the same as the original. |

## Where to Start

- **New investment tool from scratch** → Start at `bmad-forge-idea` or `bmad-prfaq`, then follow the delivery loop above.
- **Existing system, new capability** → Start at `bmad-deep-recon` (understand what's there), then `bmad-spec` for the new epic.
- **Desk problem with no clear shape** → Start with the FDE agent (`bmad-agent-fde`). Alex will elicit the intent and decide where in the loop to enter.
- **Compliance or risk mandate** → Start at `bmad-prd` with the mandate as input. Validate mode gives a findings report without changing anything.
