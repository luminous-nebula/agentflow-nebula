# AgentFlow Nebula — Workflows

Each workflow names the tables (`database/...`) and files it reads or writes, so the
data lookups stay explicit.

## Workflow A — Run Housekeeping
Trigger: "Run Housekeeping" (see `prompt-helper.csv#ph-001`).
1. Scan the workspace for misplaced, misnamed, or orphaned files.
2. Check each against `naming-convention.md` and the expected layout.
3. Propose a move/archive list (source -> destination). Await approval.
4. On approval, move superseded files to `output/archive/` with a `YYYY-MM-DD_` prefix; relocate misplaced files to their correct folder.
5. Never delete. Update any affected `*-ref` columns in the CSV tables.

## Workflow B — Consolidate Reports
Trigger: "Consolidate Reports" (see `prompt-helper.csv#ph-002`).
1. Read recent persona outputs from `output/report/` and from each `task.csv#output-ref`.
2. Synthesize one master markdown summary in `output/report/`.
3. Propose archiving the raw source reports to `output/archive/`. Await approval.

## Workflow C — Task lifecycle
1. Plan: copy a relevant template from `task-plan.csv` into `task.csv` with a new `task-id`, `project-id`, `phase-id`, and `assignee-persona-id`.
2. Status flows through the values in `config/task-status.csv`: `backlog -> planned -> in-progress -> blocked? -> review -> done -> archived`.
3. When a deliverable is produced, set `output-ref` to its path under `project/<project-id>/` or `output/report/`.
4. Only statuses listed in `task-status.csv` are valid.

## Workflow D — Add a persona
1. Choose a `team-id` from `team.csv` and a `role-id` from `role.csv` (add a role first if needed).
2. Create the folder `persona/<team-id>/<persona-id>/` and the file `<persona-id>.md` (use the singularity persona as the structural reference).
3. Append a row to `persona/persona.csv` with `persona-file` pointing to that markdown.

## Workflow E — Add a project
1. Append a row to `project/project.csv` with a kebab-case `project-id` and `project-folder` = `project/<project-id>`.
2. Create `project/<project-id>/` with a `project.md` brief.
3. Add phases to `phase.csv`, then tasks to `task.csv`.
