# AgentFlow Nebula

A general-purpose **agentic-AI workflow and data structure** template. It defines a
roster of AI personas grouped into functional tiers, a CSV-based "database" as the
single source of truth for structured data, and markdown instructions that tell each
persona how to look that data up and do their work.

## Quick start
```bash
./setup.sh        # POSIX            (or)        setup.bat   # Windows
```
Setup writes `database/config/config.csv` and creates `output/{report,log,archive}`.

## Layout
| Path | Purpose |
|---|---|
| `database/` | Structured source of truth (CSV). See `database/schema.json`. |
| `instruction/` | Process & identity source of truth (markdown). Start with `instruction/instruction.md`. |
| `persona/` | One folder per persona, grouped by functional tier (`tier-0`, `c-level`, `revenue`, `production`). |
| `project/` | Per-project working folders and deliverables. |
| `output/` | `report/` (consolidated), `log/`, `archive/` (dated, superseded files). |
| `docs/` | User guide and reference. See `docs/user-guide.md`. |

## Core ideas
- **Single source of truth:** tabular data lives in CSV; narrative lives in markdown. They cross-reference, never duplicate.
- **Functional tiers:** personas belong to `tier-0`, `c-level`, `revenue`, or `production`.
- **Naming:** kebab-case, lowercase, no spaces. See `instruction/naming-convention.md`.

Read `docs/user-guide.md` for the full guide.
