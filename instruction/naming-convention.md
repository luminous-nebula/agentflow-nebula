# AgentFlow Nebula — Naming Convention

One convention, applied everywhere. The goal is portability (scripts, git,
cross-platform) and predictability.

## Core rule
**kebab-case, lowercase, no spaces** for every folder, file, and identifier.
Use `-` to separate words. Use `_` only as documented below.

**Exception — CSV column headers** use **Title Case With Spaces**: every word
starts with a capital letter and words are separated by single spaces
(e.g. `Assignee Persona Id`). This applies to the header row of CSV tables only;
the *values* in `* Id` columns remain kebab-case.

| Item | Pattern | Example |
|---|---|---|
| Folder | `kebab-case` | `c-level`, `prompt-helper` |
| Persona id & folder | `<name>-nebula` | `carina-nebula` |
| Persona file | `<persona-id>.md` | `carina-nebula.md` |
| Project id & folder | `kebab-case` | `luminous-forge` |
| Table (CSV) file | `kebab-case.csv` | `task-status.csv` |
| **CSV column header** | **Title Case With Spaces** | **`Assignee Persona Id`** |
| Id value (inside a cell) | `kebab-case` | `tier-0`, `ph-001` |
| Role / SKILL folder | `kebab-case` | `executive-consultant` |

## CSV column headers (Title Case With Spaces)
The header row names each column with capitalized words separated by spaces.
The meaning is unchanged from the kebab-case ids; only the header text differs:

| Concept | Column header |
|---|---|
| persona-id | `Persona Id` |
| assignee-persona-id | `Assignee Persona Id` |
| team-id | `Team Id` |
| sort-order | `Sort Order` |
| output-ref | `Output Ref` |
| persona-file | `Persona File` |

Cell values still follow their own rules: id cells stay kebab-case
(`tier-0`, `t-001`), dates are ISO (`2026-06-05`), free text is prose.
File-reference columns are those whose header ends in `File`, `Folder`, or `Ref`.

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
All `* Id` cell values are kebab-case and unique within their table. Short sequential
ids use a prefix: `ph-001` (prompt-helper), `tp-001` (task-plan), `st-001`
(scheduled-task), `t-001` (task), `<slug>` (project).
