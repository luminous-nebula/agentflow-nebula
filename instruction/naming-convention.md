# AgentFlow Nebula — Naming Convention

One convention, applied everywhere. The goal is portability (scripts, git,
cross-platform) and predictability.

## Core rule
**kebab-case, lowercase, no spaces** for every folder, file, and identifier.
Use `-` to separate words. Use `_` only as documented below.

| Item | Pattern | Example |
|---|---|---|
| Folder | `kebab-case` | `c-level`, `prompt-helper` |
| Persona id & folder | `<name>-nebula` | `carina-nebula` |
| Persona file | `<persona-id>.md` | `carina-nebula.md` |
| Project id & folder | `kebab-case` | `luminous-forge` |
| Table (CSV) | `kebab-case.csv` | `task-status.csv` |
| Column header | `kebab-case` | `assignee-persona-id` |
| Id value | `kebab-case` | `tier-0`, `ph-001` |
| Role / SKILL folder | `kebab-case` | `executive-consultant` |

## Dated and versioned files
Deliverables and archived files use an ISO date prefix with an underscore separating
the date block from the kebab-case name:

```
YYYY-MM-DD_<kebab-name>[-v<n>].<ext>
2026-06-01_cash-flow-model-v6.xlsx
```

- Date prefix sorts chronologically and is machine-parseable.
- `_` separates the date from the descriptive name; the name itself stays kebab-case.
- Optional `-v<n>` suffix for explicit versions.

## Archiving
Superseded files move to `output/archive/` keeping (or gaining) the `YYYY-MM-DD_`
prefix of the date they were archived. Never delete.

## Ids
All `*-id` values are kebab-case and unique within their table. Short sequential ids
use a prefix: `ph-001` (prompt-helper), `tp-001` (task-plan), `st-001` (scheduled-task),
`t-001` (task), `pj-...`/`<slug>` (project).
