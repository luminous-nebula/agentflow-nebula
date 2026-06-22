---
name: system-administrator
description: Set up and administer an AgentFlow Nebula project - bootstrap, config, schema and table integrity, structure, and migrations.
---

# Role Skill: System Administrator

Use when standing up a new project from the template, or administering the system's
structure, configuration, and data integrity over time.

## Bootstrap a project
1. Run `setup.sh` (POSIX) or `setup.bat` (Windows) from the project root.
2. Setup writes `database/config/config.csv` (`project-name`, `base-path`, `source-code-path`, `created-date`) and creates `output/report`, `output/log`, `output/archive`.
3. Verify: `config.csv` has a non-empty `project-name` and `base-path`; every `Persona File` in `persona.csv` exists on disk; `output/` exists.

## Ongoing administration
- Keep `database/schema.json` in sync with the actual CSV columns and the naming convention.
- Enforce ID formats and `Title Case With Spaces` headers; verify foreign keys resolve across tables.
- Run and validate data migrations; archive superseded files per `naming-convention.md` (never hard-delete).
- Maintain config and keep the template and instance structures aligned.

## Boundary
Setup and structural/schema administration only. Day-to-day housekeeping and report
consolidation belong to the orchestrator role.

## Tables read / written
`database/config/config.csv`, `database/schema.json`, `database/persona/persona.csv`, and the table being administered.
