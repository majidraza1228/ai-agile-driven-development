---
title: 'Roles and Workflows'
description: How every role in a hedge fund or asset management firm maps to the BMad delivery loop — who runs what, who owns what, and where each approval gate sits.
---

# Roles and Workflows in an Asset Management Firm

## Role Map

| BMad Role | Hedge Fund Equivalent | Runs | Owns |
|---|---|---|---|
| Product Manager | Portfolio Manager / CIO | `bmad-prfaq`, `bmad-prd` | `prd.md` — the investment thesis as product requirements |
| Business Analyst | Quantitative Researcher | `bmad-brainstorming`, `bmad-deep-recon` | Research briefs, model assumptions, domain context |
| **Forward Deployed Engineer** | **FDE** | **Full delivery loop — all skills** | **End-to-end delivery for the investment team** |
| Architect | Tech Lead / Head of Quant Engineering | `bmad-architecture` | Architecture spine — data pipelines, model infra, shared decisions |
| Developer | Quant Developer / AI Engineer | `bmad-build`, `bmad-code-review` | Individual epics: implementation, tests, verified stories |
| UX Designer | Product Designer / Dashboard Lead | `bmad-ux` | `DESIGN.md`, `EXPERIENCE.md` — interface and experience specs |
| Risk Officer | Risk Management | PRD validation, architecture review | Risk sign-off at each named gate |
| Compliance Officer | Legal / Compliance | Readiness gate | Regulatory sign-off before sprint tracking |

## Who Does What, Step by Step

### Phase 1 — Clarify (Investment Thesis → Approvable Concept)

**Who:** Portfolio Manager + FDE (+ Quant Researcher for data-heavy ideas)

**What happens:**
1. FDE sits with the PM to elicit the investment intent — what problem, what signal, what edge
2. FDE runs `bmad-forge-idea` or `bmad-brainstorming` to shape the idea
3. FDE runs `bmad-prfaq` to produce a Working Backwards document
4. **Investment Committee reviews the PRFAQ** — approves, rejects, or asks for changes
5. FDE incorporates feedback and moves to Plan

**Gate:** PRFAQ verdict from Investment Committee → blocks writing the PRD

---

### Phase 2 — Plan (PRD + Architecture + Specs)

**Who:** FDE owns the loop; PM owns the PRD; Architect owns the spine; each epic engineer owns their spec

**What happens:**
1. FDE runs `bmad-prd` with the PRFAQ as input → produces `prd.md`
2. **Risk Officer reviews the PRD** — validates assumptions, flags regulatory exposure
3. FDE runs `bmad-ux` if the tool has a user-facing component → produces `DESIGN.md`
4. FDE coordinates with Architect to run `bmad-architecture` → produces the spine
5. **Architecture review** — Tech lead and risk officer sign off on cross-epic decisions
6. Each engineer (or FDE) runs `bmad-spec` for their epic → one spec per epic
7. FDE runs `bmad-create-epics-and-stories` → stories in tracker
8. **Compliance Officer reviews stories** → readiness gate before sprint tracking

**Gates:** PRD validate (Risk Officer) → Architecture review → Readiness gate (Compliance)

---

### Phase 3 — Build (Story by Story)

**Who:** Quant Developer / AI Engineer implements; FDE reviews and unblocks

**What happens:**
1. Engineer runs `bmad-build` per story — implements, tests, verifies acceptance criteria
2. FDE runs `bmad-code-review` at story boundaries and before epic close
3. Engineer or FDE runs `bmad-qa-generate-e2e-tests` for coverage on critical paths
4. If something is off-course, FDE runs `bmad-correct-course` before touching any document

---

### Phase 4 — Verify (Epic Close + Retrospective)

**Who:** FDE facilitates; PM / Portfolio Manager gives final verdict

**What happens:**
1. FDE runs `bmad-retrospective` — produces verdict, lessons, and next-epic candidates
2. **Desk sign-off** — PM confirms the tool does what the investment thesis required
3. FDE records open items in `sprint-status.yaml`
4. Loop restarts at the next epic or a course-correction

**Gate:** Retrospective verdict (desk sign-off) → blocks starting the next epic

---

## Key Principle: One Document, One Owner

| Document | Owner | Updated By |
|---|---|---|
| `prd.md` | Portfolio Manager / PM | `bmad-prd` in Update mode — never edited by hand |
| Architecture spine | Tech Lead / Head Quant Eng | `bmad-architecture` — never edited to work around the PRD |
| `SPEC.md` (per epic) | Epic engineer / FDE | `bmad-spec` — re-run when PRD changes |
| `sprint-status.yaml` | FDE / whoever tracks the whole | Updated when tracker changes; not auto-synced |
| `DESIGN.md` | Designer / Dashboard Lead | `bmad-ux` — read by specs, not modified by them |

When requirements change mid-flight, the FDE updates the PRD first and re-runs downstream skills. Editing a spec to work around a stale PRD is how systems stop making sense.
