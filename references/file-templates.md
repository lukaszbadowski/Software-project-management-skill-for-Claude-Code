# Canonical Project Files and Templates

This file defines the durable project artifacts the skill creates and maintains. It is intentionally vendor-neutral and byte-identical across the Claude Code and Codex editions of this skill, so an operator can switch tools mid-project: the `pm/` directory is the source of truth, not any tool-local memory.

## Canonical Layout

Create these four files in the project workspace under `pm/`. Do not invent additional control files by default; every default artifact in the skill maps to a section in one of these four files.

```text
pm/
├── PLAN.md       # objective, success criteria, scope, stories, traceability, checkpoint approvals
├── TASKS.md      # ordered task queue with stable IDs, routing tier, verification, evidence
├── STATE.md      # current state, handoff notes, session log
└── DECISIONS.md  # operator decisions, assumptions, risks, issues, change log
```

Add extra files only when a control branch activates:

```text
pm/CONSTRAINTS.md   # only for real external constraints: deadlines, gates, vendors, quotas
pm/RELEASE.md       # only when shipping: release checklist, rollback, monitoring, run notes
pm/RESEARCH.md      # only for feedback-heavy work: research questions, findings log
```

The agent entry-point file (`CLAUDE.md` or `AGENTS.md`) should contain one short pointer: read `pm/STATE.md` first, then `pm/TASKS.md`, and follow `pm/PLAN.md` as the approved scope.

## ID and Status Conventions

- `SC-#` success criteria, `ST-#` stories, `T-###` tasks, `D-#` decisions, `A-#` assumptions, `R-#` risks, `I-#` issues, `C-#` change records.
- IDs are stable: never renumber, never reuse. If a task is split, the children get new IDs and name the parent (`Split from: T-004`); the parent becomes `superseded`. If a task is replaced, mark it `superseded`, never delete it.
- Task statuses: `todo | in-progress | blocked | done | superseded`.
- Routing tiers: `light | standard | heavy`. Tiers are vendor-neutral; each skill edition maps them to current models in its SKILL.md. Never write model names into `pm/` files — write tiers, so the queue stays valid when switching tools.
- Checkpoint markers: `CP1` frame, `CP2` breakdown, `CP3` queue, `CP4` final acceptance. Record each approval as `approved by operator on YYYY-MM-DD`; until then write `pending`.

## Template: pm/PLAN.md

```markdown
# Project Plan — <project name>

## Objective
<One paragraph: what outcome must exist when this is done, and for whom.>

## Success Criteria
| ID | Criterion | Final check (how the operator will see it works) | Status |
| --- | --- | --- | --- |
| SC-1 | <observable outcome> | <end-to-end check> | pending |

## Scope
### In scope
- <item>
### Out of scope
- <item>

## Constraints
- <fixed stack, integrations, data, deadline only if real>

## Structural Assumptions
- A-1: <assumption the plan depends on; confirm at next checkpoint>

**CP1 — frame: pending | approved by operator on YYYY-MM-DD**

## Stories
### ST-1: <title in the operator's language>
- Outcome: <user-visible result>
- Serves: SC-1
- Acceptance:
  - [ ] <check the operator would accept as proof>
- Status: pending | approved | in-progress | done

## Traceability
| Success criterion | Covered by stories |
| --- | --- |
| SC-1 | ST-1, ST-2 |

**CP2 — breakdown: pending | approved by operator on YYYY-MM-DD**

## Final Acceptance
**CP4 — acceptance: pending | approved by operator on YYYY-MM-DD**
<At CP4, re-verify every SC end-to-end and link evidence in the Success Criteria table.>
```

## Template: pm/TASKS.md

```markdown
# Task Queue — <project name>

Statuses: todo | in-progress | blocked | done | superseded. Routing tiers: light | standard | heavy (model mapping lives in the active skill, not here).

**CP3 — queue: pending | approved by operator on YYYY-MM-DD**

## Queue (ordered)

### T-001: <imperative title>
- Story: ST-1
- Route: standard
- Scope: <exact files or modules allowed to change>
- Depends on: <task IDs or ->
- Done when: <single observable acceptance check>
- Verify with: <exact commands or manual procedure>
- Evidence: <filled after completion: command output, screenshot path, test name>
- Stop after: <explicit stop point>
- Status: todo

## Done
<Move completed tasks here with their Evidence field filled.>

## Superseded and split history
<Keep superseded tasks with a pointer to their replacements.>
```

## Template: pm/STATE.md

```markdown
# Current State — <project name>

Updated: YYYY-MM-DD <update after every completed task>

## Where the project stands
- Last completed: T-00X — <one line on what changed>
- In progress: T-00Y | none
- Next up: T-00Z
- Checkpoint status: CP1 <state>, CP2 <state>, CP3 <state>, CP4 <state>

## Handoff notes
- Commands already run and results: <...>
- Files to inspect first: <...>
- Unresolved questions: <...>
- Next session should: edit | review only | research only

## Blockers
- <blocker and what unblocks it, or none>

## Session log
- YYYY-MM-DD: <one line per session: what moved>
```

## Template: pm/DECISIONS.md

```markdown
# Decisions, Assumptions, Risks, Changes — <project name>

## Decisions
- D-1 (YYYY-MM-DD): <decision>. Why: <reason>. By: operator | proposed by agent, approved by operator

## Open decisions
- <question the operator still needs to answer>

## Working assumptions
- A-#: <detail-level assumption made inside the approved frame; structural assumptions belong in PLAN.md>

## Risks
- R-1: <risk>. Impact: <what it would break>. Trigger: <what to watch>. Response: <what to do>

## Issues
- I-1 (YYYY-MM-DD): <active problem>. Status: open | resolved (<how>)

## Change log
- C-1 (YYYY-MM-DD): <scope or plan change>. Trade-off: <what it costs>. Re-approved: CP2 on YYYY-MM-DD
```

## Usage Rules

- Read before writing: if `pm/` already exists, resume from `STATE.md` and repair gaps instead of regenerating files.
- Update `STATE.md` and the task's `Evidence` field after every completed task, in the same run that completed it.
- Keep entries short. These files are control surfaces, not documentation; deep design docs, ADRs, and runbooks live in the repo's normal docs and get linked from here.
- When switching between Claude Code and Codex mid-project, no conversion is needed: both skill editions read and write this same layout. Only re-check the `Route:` tiers against the new tool's model mapping.
