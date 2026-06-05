# AgentFlow Nebula — Master Instructions

These are the operating instructions every persona reads before acting. They define
the single source of truth, how to look data up, and the rules of engagement.

## 1. Single source of truth

There is exactly one source of truth for any given fact. Where it lives depends on
the kind of data:

| Kind of data | Lives in | Example |
|---|---|---|
| Structured / tabular | `database/**/*.csv` | who the personas are, tasks, schedules |
| Narrative / identity / process | markdown files | persona identity, this file, workflows |

Tables and files **cross-reference** each other instead of duplicating:

- A CSV row points to a file or folder through a column whose header ends in `File`, `Folder`, or `Ref`.
- This instruction file points back to the tables you must read (below).

Never copy a fact into two places. If a value is tabular, edit the CSV; if it is prose,
edit the markdown and update the CSV reference if the path changed.

## 2. Tables to look up (read these before working)

Defined in full by `database/schema.json`. The ones you will use most:

- `database/config/config.csv` — project name, base path, source-code path, timezone.
- `database/persona/team.csv` — the four functional tiers: `tier-0`, `c-level`, `revenue`, `production`.
- `database/persona/role.csv` — roles and the team each belongs to.
- `database/persona/persona.csv` — the roster. The `Persona File` column tells you where each persona's identity markdown is.
- `database/project/project.csv`, `phase.csv`, `task.csv` — what work exists, in what phase, assigned to whom, and where its output is (`output-ref`).
- `database/config/task-status.csv` — the only allowed task statuses.
- `database/prompt-helper/prompt-helper.csv` — reusable trigger prompts.
- `database/workflow/scheduled-task.csv` — recurring jobs.

To act as a persona: find your row in `persona.csv`, open the `persona-file` it points
to, then consult `role.csv` and `team.csv` for your remit. To work a project: read
`project.csv` -> `phase.csv` -> `task.csv`, filtered to your `persona-id`.

## 3. Workspace layout

```
database/      structured source of truth (CSV)   -> see schema.json
instruction/   process & identity source of truth (markdown)
persona/       one folder per persona, grouped by functional tier
project/       per-project working folders and deliverables
output/        report/ (consolidated), log/, archive/ (dated, superseded files)
docs/          user guide and reference
```

## 4. Rules of engagement

1. **Lookup before action.** Always read the relevant tables (section 2) before making changes.
2. **Referential integrity.** Every `*-id` foreign key must resolve to an existing row. When you add a persona folder, add its `persona.csv` row, and vice versa.
3. **Naming.** Follow `instruction/naming-convention.md` exactly — kebab-case for files/folders/ids; Title Case With Spaces for CSV column headers.
4. **Non-destructive.** Never hard-delete. Move superseded files to `output/archive/` with a `YYYY-MM-DD_` prefix.
5. **Confirm batch changes.** Before moving multiple files or editing many CSV rows, state the intended actions and await approval.
6. **One source of truth.** Do not duplicate a fact across a table and a file.

## 5. Standard workflows

Defined in `instruction/workflow.md`: housekeeping, report consolidation, the task
lifecycle, and adding a persona or project.
