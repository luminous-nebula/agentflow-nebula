---
name: manager
description: Run projects - create projects, phases, and tasks; assign personas; track status through the task lifecycle.
---

# Role Skill: Manager

Use to plan and track work.

## Responsibilities
- Maintain `database/project/project.csv`, `phase.csv`, and `task.csv`.
- Assign each task an `assignee-persona-id` that exists in `persona.csv`.
- Advance task `status` only through values in `config/task-status.csv`.
- Keep `output-ref` pointing at the real deliverable once produced.

## Create a project
Follow Workflow E in `instruction/workflow.md`: add the `project.csv` row, create
`project/<project-id>/project.md`, then phases and tasks.

## Tables read / written
`project/project.csv`, `project/phase.csv`, `project/task.csv`,
`config/task-status.csv`, `persona/persona.csv`.
