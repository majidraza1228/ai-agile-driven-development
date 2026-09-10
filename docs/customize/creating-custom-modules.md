---
title: 'Creating Custom Modules'
description: Build a custom BMad module from the template — what files it needs, how skills are named, and how to keep it valid.
sidebar:
  order: 5
---

Use `src/custom-module-template/` as the starting point for a new BMad module.

## Template layout

```text
src/custom-module-template/
├── module.yaml
├── README.md
├── planning/
│   └── SKILL.md
├── implementation/
│   └── SKILL.md
└── utility/
    └── SKILL.md
```

## `module.yaml` schema

Required fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `code` | string | Short module identifier |
| `name` | string | Display name for the module |
| `description` | string | What the module does and when to use it |

Common optional fields:

| Field | Type | Purpose |
| --- | --- | --- |
| `default_selected` | boolean | Whether the installer should preselect it |
| `directories` | list of strings | Skill directories to include in the module |
| `post-install-notes` | string or map | Installer guidance shown after setup |

## Skill frontmatter schema

Every skill must have `SKILL.md` with this frontmatter:

| Field | Type | Required | Purpose |
| --- | --- | --- | --- |
| `name` | string | yes | Must match the skill directory name |
| `description` | string | yes | Explain what the skill does and when to use it |

The `SKILL.md` body must also contain instructions after the frontmatter.

## Example skill types

- **Planning** — define scope, assumptions, and outputs before building
- **Implementation** — turn approved plans into files and working behavior
- **Utility** — validate, clean up, or support the module workflow

## Validation rules

Keep custom modules aligned with the validator:

- each skill directory must contain `SKILL.md`
- `name` must match the directory name
- `description` must include a `Use when` or `Use if` trigger
- the body must not be empty

## How to extend the template

1. Copy the template folder to a new module directory.
2. Rename the module code and each skill directory.
3. Replace the sample instructions with your domain-specific content.
4. Add or remove skill folders as needed.
5. Run the skill validator against the new module before publishing it.

## Use it from GitHub Copilot

1. Copy `src/custom-module-template/` into your repo or module source.
2. Open the project in GitHub Copilot and point the BMad installer at the folder.
3. Install the module from a local path during development, or from a Git URL after publishing.
4. Invoke the renamed skills from Copilot the same way you would any BMad skill.

For Copilot coding agent or Copilot CLI workflows, keep the module folder in the repository and use the normal BMad install flow so the skills are discoverable in the workspace.
