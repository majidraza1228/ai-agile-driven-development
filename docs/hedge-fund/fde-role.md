---
title: 'The Forward Deployed Engineer (FDE)'
description: What the FDE role is, why it exists in a hedge fund, and how it fits into the AI-driven agile delivery loop.
---

# The Forward Deployed Engineer (FDE)

## What the FDE Is

The Forward Deployed Engineer is not a developer who takes tickets. The FDE is embedded directly with the investment team — sitting alongside portfolio managers, quant researchers, and traders — and owns the entire delivery loop for that team.

The FDE's job is to close the gap between **investment intent** and **working software**, without either side having to translate for the other.

## Why This Role Exists in Finance

Investment teams have high-value problems and low tolerance for process. They cannot spend three weeks writing requirements before seeing a prototype. They cannot wait for a project manager to translate their trading intuition into a Jira epic. And they cannot afford a system that breaks in production because the developer never understood the alpha logic.

The FDE solves this by being the person who:
- Sits with the desk and understands the investment thesis before any code is written
- Shapes that thesis into a scoped, buildable deliverable using BMad workflows
- Builds it — or coordinates the engineers who do — and stays accountable to the desk throughout
- Handles the compliance and risk gates without the investment team having to learn the process
- Iterates until the tool works for the people actually using it

## What the FDE Owns

| Artifact | FDE's Role |
|---|---|
| PRFAQ / Investment concept | Co-creates with PM / Portfolio Manager |
| PRD | Ensures it reflects real desk intent, not assumed requirements |
| Architecture spine | Reviews for data integrity, latency, and audit trail requirements |
| Epic specs | Writes or reviews — must be implementable without guessing |
| Build sessions | Leads or pairs — stays in the code |
| Risk and compliance gates | Prepares artifacts, schedules reviews, resolves findings |
| Retrospective | Facilitates desk sign-off — the FDE does not declare success alone |

## How the FDE Uses BMad

The FDE uses the full BMad delivery loop but enters it at the right point for the work:

- **Vague desk problem** → Start with `bmad-forge-idea` or a conversation to shape intent
- **Clear investment thesis** → Go straight to `bmad-prd`
- **Approved PRD, ready to build** → `bmad-spec` then `bmad-build`
- **Something broke in production** → `bmad-correct-course` before touching any document

The FDE also uses `bmad-deep-recon` to understand the regulatory landscape, existing market tools, or quant literature before committing to an approach.

## What Makes an Effective FDE

- **Financial literacy** — understands factor models, execution risk, P&L attribution, and why latency matters
- **Technical depth** — can write production code, design a data pipeline, and spot an architecture flaw
- **Judgment under ambiguity** — makes scoping decisions without a committee, and owns them
- **Delivery discipline** — uses BMad structure to keep the loop moving, not as a reason to slow down

## The FDE in the Approval Chain

The FDE does not bypass governance — they navigate it on behalf of the desk. At each named gate:

| Gate | FDE's Action |
|---|---|
| PRFAQ verdict | Presents concept to investment committee; incorporates feedback into PRD |
| PRD validate | Runs risk officer review; resolves ASSUMPTION tags before architecture |
| Architecture review | Defends cross-epic decisions; ensures spine is complete before spec |
| Readiness gate | Confirms compliance sign-off; unblocks stories for sprint tracking |
| Retrospective verdict | Gets desk sign-off before declaring epic complete |

The FDE keeps these gates moving. Stalled reviews are an FDE problem to solve, not a reason to skip.
