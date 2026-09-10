---
title: Install BMad for Copilot
description: Set up BMad in a Copilot workspace so the skills are ready to use right away.
---

Use this guide when you want Copilot to have BMad available in a fresh checkout or
worktree. The goal is to make setup repeatable: install the repo, install BMad,
and confirm the skills are visible in the tool you use with Copilot.

## Prerequisites

:::note[What you need]

- **Node.js 20.12 or later**
- **Python 3.10 or later**
- **uv**

:::

## Quick path

1. Open the repository root in a terminal.
2. Run `npx bmad-method install`.
3. Let the installer place the skills for your Copilot-connected tool.
4. Run `bmad-help` or `bmad-build` in Copilot to confirm the setup.

## Install BMad

### 1. Check the runtime

```bash
node --version
python3 --version
uv --version
```

### 2. Install the repository dependencies

```bash
npm ci
```

### 3. Run the BMad installer

```bash
npx bmad-method install
```

The installer detects your tool, writes the BMad skills into the right skills
directory, and creates the shared `_bmad` configuration that Copilot can use
later.

### 4. Confirm the skills are available

Open your Copilot-connected editor or agent session and try:

```text
bmad-help
```

If the skill responds, BMad is ready.

## What gets installed

| Item | Purpose |
| --- | --- |
| Skills | Make BMad commands available in your AI tool |
| `_bmad` | Stores shared configuration and generated artifacts |
| Docs | Explain what to run next and how to use the skills |

## Troubleshooting

:::caution[If the skills do not appear]

Reload the editor window, reopen the workspace, or rerun `npx bmad-method install`
from the same checkout. If `uv` is missing, install it before retrying because
some BMad validation commands depend on it.

:::
