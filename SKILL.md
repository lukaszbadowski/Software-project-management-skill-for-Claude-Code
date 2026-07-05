---
name: software-project-management-for-claude
description: Structure software projects run by a single human operator using Claude Code with agents or subagents. Use when Claude Code needs to plan, rescue, or govern solo operator delivery with operator-approved story breakdowns, small reviewable tasks with stable IDs, durable pm/ files, cost-aware model routing, tests or evals, traceable acceptance, and guardrails, adding deadline or release controls only when real external constraints exist.
---

# Software Project Management

## Overview

Use this skill to turn vague AI-assisted delivery work into a controlled execution system for one human operator. The operating loop: elicit the frame, get the operator to consciously approve a story breakdown, execute through a small routed task queue in durable files, verify with evidence, and close only when every success criterion is re-verified end-to-end. Add deadline, approval, vendor, budget, or release-window controls only when the project actually has those external constraints.

This skill shares its project file format with the Codex edition (`software-project-management`). The `pm/` files are vendor-neutral; when the operator switches tools mid-project, `pm/` remains the source of truth and only the model-routing table changes.

## Quick Start

1. Inspect the workspace. If `pm/` exists, read `pm/STATE.md`, then `pm/TASKS.md`, and resume from the queue — repair gaps, do not regenerate.
2. If no project system exists, run Checkpoint CP1: ask the elicitation questions and draft the frame in `pm/PLAN.md`.
3. Create the four canonical files from [references/file-templates.md](./references/file-templates.md).
4. Drive the work through the checkpoints: CP2 breakdown, CP3 queue, execution loop, CP4 final acceptance.

## Operator Checkpoint Protocol

The breakdown must be consciously co-created with the operator, not assumed on their behalf. Four approval gates structure this; record each approval with a date in `pm/PLAN.md` or `pm/TASKS.md`.

- **CP1 — Frame.** Elicit and get approval for: objective, success criteria (each with the end-to-end final check the operator would accept as proof), scope in/out, constraints, structural assumptions.
- **CP2 — Breakdown.** Present stories in the operator's language, each with acceptance criteria and traced to the success criteria it serves. Surface open decisions explicitly; resolve them at the checkpoint, do not assume them away. Operator approves before any task queue exists.
- **CP3 — Queue.** Present the ordered task queue with routing tiers. This gate may be quick, but the operator sees the plan before execution starts.
- **CP4 — Final acceptance.** Before reporting the project or milestone done: re-verify every success criterion end-to-end against its CP1 final check, link evidence, present the acceptance report, and get sign-off. Task-level green is not project done.

Standing rules:

- Assumptions may fill small gaps *inside* an approved frame; log them in `pm/DECISIONS.md`. Anything structural — scope, stories, acceptance bar, success criteria — goes back through the relevant checkpoint as a change record with its trade-off stated.
- Default CP1 elicitation questions: What outcome must exist when this is done, and for whom? How will you personally check that it works — what would you test? What is explicitly out of scope for now? Which constraints are fixed (stack, integrations, data, deadline, budget)? What already exists that this must fit? What is riskiest or most unclear? How much do you want to review — every task, every story, or only checkpoints?
- The last answer calibrates operator attention: honor it when deciding what to present versus proceed with.
- In rescue mode, run the checkpoints in repair form: reconstruct the implied frame and breakdown from the workspace, present them for confirmation, then rebuild the queue.

## Canonical Project Files

Keep durable state in `pm/` — four files, defined with full templates in [references/file-templates.md](./references/file-templates.md):

- `pm/PLAN.md` — objective, success criteria, scope, stories, traceability, checkpoint approvals
- `pm/TASKS.md` — ordered task queue with stable IDs, routing tiers, verification, evidence
- `pm/STATE.md` — current state, handoff notes, session log
- `pm/DECISIONS.md` — decisions, working assumptions, risks, issues, change log

Every default artifact this skill requires is a section in these four files; do not create more control files by default. Add `pm/CONSTRAINTS.md`, `pm/RELEASE.md`, or `pm/RESEARCH.md` only when the matching control branch activates. Keep the root `CLAUDE.md` entry short and navigational: point to `pm/STATE.md` first, then `pm/TASKS.md`, with `pm/PLAN.md` as the approved scope.

Claude Code's built-in task list and plan mode are session-scoped conveniences: mirror anything durable into `pm/TASKS.md` and `pm/STATE.md`, which remain the system of record across sessions and tools.

## Model Routing for Cost Control

Route every task to the cheapest tier that can do it reliably. Tasks carry a vendor-neutral `Route:` tier in `pm/TASKS.md`; this edition maps tiers to Claude models:

| Tier | Claude model | Use for |
| --- | --- | --- |
| heavy | opus | planning, decomposition, architecture, cross-cutting refactors, ambiguous debugging, review and sign-off of risky work, final acceptance |
| standard | sonnet | bounded implementation, tests, moderate-complexity changes |
| light | haiku | repo search and localization, summaries, mechanical edits, doc updates, formatting, log triage |

Routing rules:

- Keep the main thread on a capable model as director: it frames briefs, routes work, judges evidence, and signs off. Delegate execution via the Agent tool with an explicit `model` parameter matching the task's tier.
- Assign the tier when the task enters the queue at CP3; the heavy tier plans, the cheaper tiers execute.
- Escalate one tier after two failed attempts or a low-confidence result on the same task; record the escalation in the task entry.
- The reviewer tier must be at least the writer tier, and risky or cross-cutting diffs get a fresh-context heavy review. A light-tier agent never self-approves.
- Model names drift. Revalidate this mapping against current model docs when models or prices change; the tiers in `pm/` files stay valid regardless.

## Workflow

### Build Context First

- Extract the real objective, users, constraints, dependency landscape, acceptance bar, and release expectations. Treat deadlines, budgets, approvals, vendor schedules, or launch windows as first-class inputs only when they are explicit in the project context.
- Look for existing artifacts before inventing new ones: `pm/` files, task briefs, backlogs, design docs, ADRs, test strategy, runbooks, risk logs, CLAUDE.md files, and memory entries.
- If important structural information is missing, ask at the checkpoint; make and log assumptions only for details inside an approved frame.
- For a rescue, diagnose the control system before proposing fixes: objective clarity, scope quality, dependency visibility, acceptance quality, risk hygiene, context legibility, tool permissions, and release readiness where relevant.

### Choose the Control Mode

- Default to `solo operator` control: one operator steering Claude Code through the work.
- Add the `external-constraint` branch when a fixed deadline, compliance gate, approval step, vendor dependency, quota cap, or launch window is real.
- Add the `feedback-heavy` branch when user learning, UX iteration, or discovery dominates.
- Add the `release-safety` branch when the project ships software needing cutover, rollback, monitoring, or operating notes.

### Size the Execution Units

- Stories group user-visible value and carry acceptance criteria; milestones only group work. Neither is the next action — execution runs through the task queue.
- Make each task small enough for one focused agent run and one quick operator review: one subsystem, interface, document, or test surface; one reviewable diff.
- Give every task a stable ID, story reference, routing tier, file or module scope, dependency or precondition, done-when check, exact verification, and explicit stop point.
- Split before execution if a task would touch many unrelated areas or need a long uninterrupted run. Splits and replacements keep history: children get new IDs naming the parent; replaced tasks are marked superseded, never silently renamed.
- After each completed task, fill its Evidence field, update `pm/STATE.md`, and pick the next task — in the same run.

### Maintain Traceability

- Every success criterion maps to at least one story; every story maps to at least one task. Keep the map current in `pm/PLAN.md` as stories and tasks change.
- A story is done only when all its tasks are done and its acceptance criteria are verified with evidence.
- The project is done only when CP4 passes: each success criterion re-verified end-to-end, not inferred from unit-level green.

### Plan and Govern the Work

- Plan at three levels: overall direction, optional checkpoints, near-term executable tasks. Add long-range date plans only when external commitments require them.
- Map dependencies explicitly, including environments, data, approvals, vendors, quotas, and external systems when they matter. Compute a critical path only when an external deadline, gate, launch window, or scarce bottleneck makes it useful.
- Plan scarce resources only when they constrain throughput: operator attention, CI capacity, API quotas, model budget, environment access, permissions.
- Treat scope change as a trade-off decision recorded in the change log, not a free addition.
- Govern by evidence and explicit triggers; add recurring rituals only when they demonstrably improve control for this project.

### Run a Quality-First Delivery Loop

- Before implementation, define the smallest credible proof that the change is correct: failing repro, automated test, expected output, screenshot check, contract check, or exact manual procedure. When automated tests are missing, create the fastest credible check instead of skipping validation.
- Use the default sequence `explore -> plan -> implement -> verify -> review -> document`.
- Record evidence, not just conclusions: commands run, outputs, screenshots, metrics, review notes — tied to the task ID.
- Preserve invariants and change budgets for risky tasks: file scope, public interfaces that must stay stable, data or migration safety, rollback or escalation triggers.
- Require a fresh-context review (dedicated step or review subagent, heavy tier) for risky, cross-cutting, or high-impact changes, with a bug, regression, security, and maintainability lens.
- Pilot large automated or repetitive changes on a narrow slice before scaling across the codebase.
- If the same failure repeats twice, stop, strengthen the docs, rules, or validators, and restart with clean context instead of stacking corrections.
- Separate user testing for product quality from user research for product value; treat non-functional requirements as release criteria, not deferred polish; turn repeated failures into process, tooling, or documentation improvements.

### Delegate Safely

- Keep the main thread in the director role: goals, decomposition, synthesis, sign-off. Prefer subagents for autonomy-ready bounded work — especially high-volume, parallel, read-heavy, or verification-heavy tasks — returning concise summaries with evidence rather than raw logs.
- Give every delegated task a written brief: task ID, objective, scope, constraints, verification commands, expected evidence, stop point, escalation trigger, and the model matching its routing tier.
- Keep tiny, tightly coupled, or heavily interactive tasks in the main thread when delegation overhead outweighs context savings.
- Prefer deterministic hooks or validators for zero-exception checks: required lint or test commands, path restrictions, secret scanning.
- Enforce least privilege, secret-handling rules, trust boundaries, and explicit operator approval for risky actions. Revalidate prompts and workflows with evals when behavior or tooling changes.

## Common Deliverables

- the four `pm/` files, created or repaired
- operator-approved story breakdown with traceability map
- ordered, routed task queue with stable task IDs
- project rescue assessment
- verification matrix and evidence pack
- CP4 acceptance report mapping success criteria to evidence
- review checklist or review prompt for risky work
- external-constraint addendum, only when deadlines, approvals, vendors, or launch windows matter

## Reference Files

- Read [references/file-templates.md](./references/file-templates.md) when creating or repairing the `pm/` files. This defines the cross-tool file contract.
- Read [references/worked-example.md](./references/worked-example.md) for one compressed end-to-end example of checkpoints, routing, and acceptance.
- Read [references/project-rulebook.md](./references/project-rulebook.md) when auditing or rescuing a project, or deciding whether a control is worth adding. SKILL.md remains the operating spec.
- Read [references/external-constraints.md](./references/external-constraints.md) only when the project has fixed deadlines, approval gates, vendor dependencies, quota caps, launch windows, or production release risk.
- Read [references/ai-agent-practices.md](./references/ai-agent-practices.md) when planning file-backed memory, subagents, routing, evals, quality loops, and guardrails in depth.
- Read [references/source-anchors.md](./references/source-anchors.md) when you need provenance or a refresh point for volatile vendor topics.
- Do not load every reference by default. Read the smallest relevant file first.

## Output Standards

- Write in imperative form; prefer concrete artifacts and decision-ready outputs over generic PM advice.
- Report checkpoint status first when summarizing project state; reference task IDs first when reporting work.
- Default task format: `Task ID`, `Task`, `Story`, `Route`, `Scope`, `Depends on`, `Done when`, `Verify with`, `Evidence`, `Stop after`, `Status`.
- When in doubt, split work into smaller tasks before execution; prefer one reviewable diff per task.
- Default quality package: invariants to preserve, exact verification steps, evidence to capture, review focus, rollback trigger when relevant.
- Keep model names out of `pm/` files; write routing tiers instead.
- Do not introduce date plans, budget tracking, approval workflows, recurring cadences, or stage gates unless the project genuinely depends on them.
- If the user asks for the latest model, benchmark, or vendor workflow guidance, verify it externally; the bundled source anchors are point-in-time snapshots.
