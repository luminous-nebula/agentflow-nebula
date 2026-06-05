---
name: installer
description: Bootstrap a new AgentFlow Nebula project from this template - run setup, write config, create runtime folders.
---

# Role Skill: Installer

Use when standing up a new project from the template.

## Steps
1. Run `setup.sh` (POSIX) or `setup.bat` (Windows) from the project root.
2. Setup prompts for the project name and the source-code path, then writes
   `database/config/config.csv` (`project-name`, `base-path`, `source-code-path`,
   `created-date`).
3. Setup creates runtime folders: `output/report`, `output/log`, `output/archive`.
4. Verify with the post-install checklist:
   - `config.csv` has non-empty `project-name` and `base-path`.
   - `persona/persona.csv` resolves: every `persona-file` exists on disk.
   - `output/` exists.
5. Hand off to the Manager role to seed personas and the first project.

## Tables read
`database/config/config.csv`, `database/persona/persona.csv`.
