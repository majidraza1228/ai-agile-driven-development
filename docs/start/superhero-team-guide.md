---
title: Superhero Team Guide
description: How a project manager, architecture team, and dev team use the BMAD superhero agent squad in Claude Code — from idea to shipped product.
sidebar:
  order: 4
---

This guide shows a team how to use BMAD's five agent personas end-to-end: from pressure-testing an idea through shipping working code and running a retrospective. Each agent is a named superhero character that Claude plays in your session.

:::tip[Quick Path]
PM runs `/bmad-agent-pm`, Architect runs `/bmad-agent-architect`, Dev runs `/bmad-agent-dev`. Each agent greets you, shows a menu, and guides you from there.
:::

## The Superhero Squad

Each role maps to a superhero persona with a matching icon. When the agent greets you, it leads with the icon so you always know who is speaking.

| Icon | Hero | Role | Skill |
| ---- | ---- | ---- | ----- |
| 🦾 | **Tony Stark** | Product Manager | `bmad-agent-pm` |
| 🦇 | **Batman** | System Architect | `bmad-agent-architect` |
| 🦸 | **Superman** | Senior Developer | `bmad-agent-dev` |
| ⚡ | **Wonder Woman** | UX Designer | `bmad-agent-ux-designer` |
| 🧠 | **Professor X** | Business Analyst | `bmad-agent-analyst` |

Each member works in their own Claude Code session and shares artifacts through files on disk. The PM produces files the Architect reads; the Architect produces files the Dev reads — no manual copy-paste required.

## Phase 1 — Project Manager: Idea to Backlog

Tony Stark drives the project from raw idea through a complete, prioritized backlog ready for development.

### Step 1: Forge the idea

Run `bmad-forge-idea`. Tony Stark pressure-tests the idea using multiple personas — a competitor, a skeptical finance reviewer, a real user — asking hard questions until the idea either hardens or gets killed early. This is the cheapest time to find out the idea does not hold up.

Output: `forged-idea.md` — a short file of locked decisions and rejected options.

### Step 2: Create the PRD

Run `bmad-agent-pm`. Tony Stark greets you and presents a menu. Choose **PRD** (or just say "let's write the PRD") and pick a working mode:

- **Fast path** — Tony Stark drafts the full PRD immediately, tagging guesses with `[ASSUMPTION]`. You review and correct.
- **Coaching path** — Tony Stark walks each section with you, pulling the real requirements out through questions. Takes longer, produces a tighter doc.

Tony Stark reads `forged-idea.md` automatically as input.

Output: `prd.md`

### Step 3: Create epics and stories

From the Tony Stark menu, choose **CE** (Create Epics). Run `bmad-create-epics-and-stories`. Tony Stark reads the PRD and breaks it into epics and user stories with full acceptance criteria — the exact format Superman (Dev) needs to start building.

Output: `epics/*.md` and `stories/*.md`

### Step 4: Generate the sprint tracker

Run `bmad-sprint-planning` or choose **IR** (Implementation Readiness) from the Tony Stark menu. The skill first runs a readiness gate — PASS, CONCERNS, or FAIL — then generates a `sprint-status.yaml` file that tracks every story and epic.

Output: `sprint-status.yaml`

**Track project progress at any time:**

```
bmad-sprint-planning → "show sprint status"
```

Tony Stark can call this anytime to see what is done, what is in progress, and what is blocked.

## Phase 2 — Architecture Review

The architecture review is a live round-table debate, not a document review meeting.

### Run the review as a party

Run `bmad-party-mode`. This puts Tony Stark, Batman, Superman, Wonder Woman, and Professor X in a room together. They argue, challenge each other, and surface issues the PM or Architect working alone would miss. Say what you want to decide — the stack, a key boundary, a data ownership question — and let the party clash over it.

This IS the architecture review meeting.

### Lock the architecture spine

After the party, run `bmad-agent-architect`. Batman greets you and presents a menu. Choose **CA** (Create Architecture). Batman works in one of two modes:

- **Coaching path** (default) — Batman asks open-ended questions, surfaces alternatives, and pushes back when a decision is thin. The load-bearing calls — paradigm, boundaries, shared state rules — are shown with the alternatives Batman weighed, so the team can choose rather than discover the choice later.
- **Fast path** — Batman drafts the full spine immediately with `[ASSUMPTION]` tags for review.

Batman reads the PRD and any `forged-idea.md` automatically.

Output: `ARCHITECTURE-SPINE.md` — a binding contract of the invariants every developer must follow. It fixes only the decisions that would cause incompatible implementations if left open.

:::note[What goes in the spine]
The spine records decisions, not rationale. The reasoning lives in the memlog (`.memlog.md`) that Batman maintains during the session. One test decides what belongs in the spine: if two developers built the same thing independently, could they make incompatible choices? If yes and the call is non-obvious, it goes in.
:::

## Phase 3 — Developer: Build and Ship

Superman executes the backlog story by story with test-first discipline.

### Pick up a story

Run `bmad-agent-dev`. Superman greets you and shows a menu. He reads `sprint-status.yaml` to find the next story ready for implementation.

### Build

Choose **BD** (Build) or run `bmad-build` directly. Superman follows red-green-refactor — writes a failing test first, makes it pass, then refactors. He works from the acceptance criteria in the story file and the constraints in `ARCHITECTURE-SPINE.md`. He does not add features beyond what the story asks for.

### Review the code

Choose **CR** (Code Review) or run `bmad-code-review`. Batman reviews the build against the story's acceptance criteria and the architecture spine — not just for style, but for correctness and invariant compliance.

### Walk a human through the change

Run `bmad-walkthrough`. This guides a product manager or tech lead through what was built: what it is for, what to look at closely, and how to test it. Use this before marking a story done if a human sign-off is required.

### Generate tests

Choose **QA** or run `bmad-qa-generate-e2e-tests`. Superman generates an end-to-end test suite from the story's acceptance criteria.

## Phase 4 — Retrospective

Run `bmad-retrospective` at the end of every epic. It reads the epic spec, all story files, commit history, and `sprint-status.yaml`, then produces a retrospective with:

- Sourced findings — every claim has a file, line, or commit reference. No invented root causes.
- Action items for the next epic.
- An acceptance decision: accept or reject the epic based on the evidence.

## Complete Flow at a Glance

```
Tony Stark (PM)
  bmad-forge-idea          → forged-idea.md
  bmad-agent-pm → PRD      → prd.md
  bmad-create-epics-and-stories → epics + stories
  bmad-sprint-planning     → sprint-status.yaml

Architecture Review
  bmad-party-mode          → all heroes debate the design
  bmad-agent-architect     → ARCHITECTURE-SPINE.md

Superman (Dev) — one story at a time
  bmad-agent-dev           → picks story from sprint-status.yaml
  bmad-build               → working code + tests
  bmad-code-review         → reviewed
  bmad-walkthrough         → human sign-off

Track (Tony Stark, anytime)
  bmad-sprint-planning → "show sprint status"

End of epic
  bmad-retrospective       → retro report + acceptance decision
```

## Artifact Map

| Artifact | Created by | Read by |
| -------- | ---------- | ------- |
| `forged-idea.md` | Tony Stark (forge) | Tony Stark (PRD) |
| `prd.md` | Tony Stark | Batman, Superman |
| `ARCHITECTURE-SPINE.md` | Batman | Superman |
| `epics/*.md`, `stories/*.md` | Tony Stark | Superman, sprint tracker |
| `sprint-status.yaml` | Sprint planner | Tony Stark, Superman |
| `retrospective.md` | BMAD auto | Whole team |

## How to Invoke Each Hero

Type the skill name in Claude Code. Each hero greets you by name, shows a numbered menu, and waits for your choice. You can skip the menu by naming your intent directly:

```
"hey Tony Stark, let's write the PRD"
"hey Batman, let's architect this"
"hey Superman, let's implement the next story"
"hey Wonder Woman, let's design the UX"
"hey Professor X, let's research the market"
```

The hero stays active in character for the whole session. Call `bmad-help` at any time if you are unsure what to do next.

:::caution[BMAD updates]
The hero names are set in each agent's source files. If you run `npx bmad-method install` to update BMAD, check that the names were not reset to the original defaults (John, Winston, Amelia, Sally, Mary).
:::
