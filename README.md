# AgentFlow Nebula

> A general-purpose template for running a team of AI personas over a shared,
> file-based workspace.

AgentFlow Nebula gives a set of AI personas one organized place to work. Structured
data lives in CSV tables (the "database"); identity and process live in markdown.
A Tier-0 persona, **Singularity Nebula**, keeps the workspace clean.

This README is the orientation and quick start. For the full manual — every table,
workflow, and persona checklist — see **[`docs/user-guide.md`](docs/user-guide.md)**.

## Quick start

```bash
./setup.sh        # POSIX
setup.bat         # Windows
```

Setup asks for the project name and source-code path, writes
`database/config/config.csv`, and creates `output/{report,log,archive}`.

## Repository layout

| Path | Purpose |
|---|---|
| `database/` | Structured source of truth (CSV). Described by `database/schema.json`. |
| `instruction/` | Process & identity source of truth (markdown). Start at `instruction/instruction.md`. |
| `persona/` | One folder per persona, grouped by functional tier. |
| `project/` | Per-project working folders and deliverables. |
| `output/` | `report/` (consolidated), `log/`, `archive/` (dated, superseded files). |
| `docs/` | The user guide. |

## Core concepts

- **Single source of truth.** Tabular data lives in CSV; narrative lives in markdown.
  They cross-reference (via `*-file` / `*-folder` / `*-ref` columns), never duplicate.
- **Functional tiers.** Every persona belongs to one tier: `tier-0`, `c-level`,
  `revenue`, or `production`.
- **One naming rule.** kebab-case, lowercase, no spaces — for files, folders, ids,
  and columns. Dated files use `YYYY-MM-DD_<name>[-v<n>].<ext>`.
  See `instruction/naming-convention.md`.
- **Non-destructive.** Nothing is deleted; superseded files move to `output/archive/`.

## Where to go next

| You want to… | Read |
|---|---|
| Understand the whole system | `docs/user-guide.md` |
| Operate as / with personas | `instruction/instruction.md` |
| Know the data model | `database/schema.json` |
| Follow a workflow | `instruction/workflow.md` |
| Get the naming rules | `instruction/naming-convention.md` |

---
AgentFlow Nebula · v2.0.0
