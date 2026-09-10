# Custom Module Template

This directory shows the minimum structure for a reusable BMad module.

## What is included

- `module.yaml` for module metadata and installer guidance
- planning, implementation, and utility example skills
- a README that explains how to extend the template

## How to extend

1. Copy this folder to a new module name.
2. Rename `code`, the module directory, and each skill directory.
3. Update every skill `name` to match its directory name.
4. Replace the sample instructions with your own module content.
5. Keep each skill description specific and include a `Use when` trigger.

## Skill conventions

- Each skill lives in its own directory.
- Each skill must include `SKILL.md`.
- The `name` frontmatter value must match the directory name.
- The `description` frontmatter value should explain what the skill does and when to use it.

## Example skill types

- `planning/` — for discovery, scoping, and decision-making
- `implementation/` — for build or delivery workflows
- `utility/` — for reusable helper tasks and checks

## Next step

Replace these examples with domain-specific skills, then point the installer at the new module directory.
