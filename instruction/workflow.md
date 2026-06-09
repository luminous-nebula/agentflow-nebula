# AgentFlow Nebula — Workflows

Each workflow names the tables (`database/...`) and files it reads or writes, so the
data lookups stay explicit.

## Workflow A — Run Housekeeping
Trigger: "Run Housekeeping".
1. Scan the workspace for misplaced, misnamed, or orphaned files.
2. Check each against `naming-convention.md` and the expected layout.
3. Propose a move/archive list (source -> destination). Await approval.
4. On approval, move superseded files to `output/archive/` with a `YYYY-MM-DD_` prefix; relocate misplaced files to their correct folder.
5. Never delete. Update any affected `*-ref` columns in the CSV tables.

## Workflow B — Consolidate Reports
Trigger: "Consolidate Reports".
1. Read recent persona outputs from `output/report/` and from each `task.csv#output-ref`.
2. Synthesize one master markdown summary in `output/report/`.
3. Propose archiving the raw source reports to `output/archive/`. Await approval.

## Report file naming
Every markdown report written to `output/report/` uses this filename format:

```
<YYYY>-<MM>-<DD> <HH><MI> <persona-id> report.md
```

- `<YYYY>-<MM>-<DD>` — ISO date; `<HH><MI>` — 24-hour time with no separator (e.g. `1430`).
- `<persona-id>` — the author persona's `Persona ID` from `persona.csv` (e.g. `carina-nebula`).
- Example: `2026-06-06 1430 carina-nebula report.md`.

This is a report-specific convention — it uses spaces and a time component and is an
intentional exception to the kebab-case file rule in `naming-convention.md`. When a newer
report supersedes an earlier one, archive the old file to `output/archive/` (Workflow A).

## Workflow C — Task lifecycle
1. Plan: add a row to `task.csv` with a new `Task ID` (`PH<NN>-PD<NN>-T<NNNN>`), plus its `Project ID`, `Phase ID`, a `Description`, its estimated `Hours`, and the `Auto` flag (see "Auto flag" below).
2. Status flows through the values in `config/task-status.csv`: `backlog -> planned -> in-progress -> blocked? -> review -> done -> archived`.
3. Only statuses listed in `task-status.csv` are valid.

### Auto flag
The `Auto` column in `task.csv` marks whether a task can be executed by an AI persona.
`TRUE` = an AI persona may pick up and run the task autonomously; `FALSE` = the task
requires the human founder (manual/offline work). Personas only self-assign and execute
tasks where `Auto` is `TRUE`.

## Workflow D — Add a persona
1. Choose a `team-id` from `team.csv` and a `role-id` from `role.csv` (add a role first if needed).
2. Create the folder `persona/<team-id>/<persona-id>/` and the file `<persona-id>.md` (use the singularity persona as the structural reference).
3. Append a row to `persona/persona.csv` with `persona-file` pointing to that markdown.

## Workflow E — Add a project
1. Append a row to `project/project.csv` with a `Project ID` (`PD<NN>`) and `Project Folder` = `project/<project-id>`.
2. Create `project/<project-id>/` with a `project.md` brief.
3. Add phases to `phase.csv`, then tasks to `task.csv`.

## Workflow F — Dispatch & Execution
1. **Plan & Assign:** The Dispatcher (Mensa) reads `task.csv` to determine today's goals. Mensa assigns these tasks by writing to `database/project/dispatch.csv`.
2. **Execute:** Production personas (Daedalus, Doradus, Quasar, Quadrans, Pictor) read `dispatch.csv` on their scheduled cycles. If assigned a task, they execute it. If not, they sleep.
3. **Report:** Upon completion or at the end of a cycle, personas submit their execution reports to `output/report/`.
4. **Consolidate & Update:** Mensa reads the execution reports, consolidates them, and updates the central `task.csv` state. Production personas never write directly to `task.csv`.

## Workflow G — Work Cycle
Trigger: "Work Cycle <n>" (e.g., Work Cycle 3)
1. Read `database/project/dispatch.csv` to find tasks assigned to your Persona ID.
2. If no tasks are assigned, terminate the cycle successfully (sleep).
3. If tasks are assigned, execute them autonomously using your role skills and the context in the `project/` folders.
4. Write execution reports to `output/report/` using the strict naming convention.

## Workflow H — Aggregate Status
Trigger: "Aggregate Status"
1. Read the central state from `database/project/task.csv` and `dispatch.csv`.
2. Identify blocked tasks, overdue deliverables, or unassigned backlog items.
3. Generate a status digest in `output/report/` to inform the executive team.

## Workflow I — Weekly Retrospective
Trigger: "Weekly Retrospective"
1. Review the week's completed tasks in `task.csv` and the execution reports in `output/report/`.
2. Identify bottlenecks, velocity metrics, and workflow failures across the production team.
3. Write a retrospective summary to `output/report/`.

## Workflow J — Executive Review
Trigger: "Executive Review"
1. Read recent status aggregates, production reports, and cash flow assumptions (`database/cashflow/`).
2. Perform red-team stress-tests and identify strategic risks or architectural flaws.
3. Output an executive brief to `output/report/`.

## Workflow K — Weekly Strategic Review
Trigger: "Weekly Strategic Review"
1. Read Carina's executive reviews and Orion's market research from `output/report/`.
2. Evaluate current trajectory against `instruction/strategic-baseline.md`.
3. Make binding strategic decisions and output a strategic directive to `output/report/`.

## Workflow L — Competitor Baseline Scan
Trigger: "Competitor Baseline Scan"
1. Search the web and recent literature for updates on key competitors.
2. Synthesize intelligence briefs highlighting competitor movements and market shifts.
3. Output the brief to `output/report/`.
