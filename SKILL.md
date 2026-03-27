---
name: software-project-management-for-claude
description: Structure software projects run by a single human operator using Claude Code with agents or subagents. Use when Claude Code needs to plan, rescue, or govern solo operator delivery with clear scope, small reviewable tasks, durable files, dependency sequencing, tests or evals, change control, and guardrails, while adding deadline or release controls only when real external constraints exist.
---

# Software Project Management

## Overview

Use this skill to turn vague AI-assisted delivery work into a controlled execution system for one human operator. Default to objective, scope, small executable tasks with stable IDs, acceptance, dependency sequencing, durable files, tests or evals, quality evidence, risk or change logs, and permissions. Add deadline, approval, vendor, budget, or release-window controls only when the project actually has those external constraints.

## Quick Start

1. Inspect the workspace for existing project artifacts before inventing new ones.
2. Classify the work as `solo operator default` or `external-constraint branch`.
3. Create or repair the minimum control system: operator objective, scope, small executable tasks, acceptance, verification ladder, work plan, dependency sequence, risk or change controls, documentation, and guardrails.
4. Produce the lightest artifact set that preserves continuity across sessions and agent runs.

## Workflow

### Build Context First

- Extract the real objective, users, constraints, dependency landscape, acceptance bar, and release expectations. Only treat deadlines, budgets, approvals, vendor schedules, or launch windows as first-class inputs if they are explicit in the project context.
- Look for an existing task brief, execution plan, backlog, design docs, ADRs, test strategy, release plan, runbooks, risk log, CLAUDE.md files, and memory entries.
- If important information is missing, make reasonable assumptions and record them explicitly.
- If the request is to rescue a project, diagnose the control system before proposing fixes: objective clarity, scope quality, dependency visibility, acceptance quality, risk hygiene, context legibility, tool permissions, and release readiness where relevant.

### Choose the Control Mode

- Default to the `solo operator` control mode when one operator is steering Claude Code through the work.
- Add the `external-constraint` branch when a fixed deadline, compliance gate, approval step, vendor dependency, quota cap, or launch window is real.
- Add the `feedback-heavy` branch when user learning, UX iteration, or discovery dominates the work.
- Add the `release-safety` branch when the project ships software that needs cutover, rollback, monitoring, or operating notes.

### Create or Repair the Core Artifact Set

Always maintain these artifacts in some form:
- objective and success criteria
- operator decision record
- source-of-truth index
- scoped work breakdown or backlog
- small task queue with stable task IDs for the next executable units
- acceptance and quality criteria
- verification ladder and evidence path for each nontrivial task
- dependency map or dependency sequence
- durable execution plan or current-state note
- risk, issue, and change controls
- permission and trust-boundary rules
- documentation freshness path

Add these artifacts when needed:
- External constraints: deadline or gate log, minimal critical-path view, vendor or approval dependency list, quota or spend tracker
- Feedback-heavy: research questions, findings log, scope-update loop
- Agent-assisted: CLAUDE.md entry point, agent or task routing, evals, explicit escalation rules, and deterministic hooks or validators for must-always-pass checks
- Quality-heavy: invariants list, review checklist, manual-check procedure, and change budget for risky work
- Release safety: release checklist, rollback plan, monitoring checks, operating notes or runbook

### Size the Execution Units

- Use milestones, themes, or phases only to group work. Do not use them as the next action.
- Default to a task queue where each task is small enough for one focused agent run and one quick operator review.
- Assign a unique stable task ID when a task enters the queue. Keep the ID stable even if the task title or wording changes.
- Make each task narrow in scope: one subsystem, interface, document, or test surface when possible.
- Give every task an explicit stop point, file or module scope, dependency or precondition, and acceptance check.
- If a task is split, keep the original task ID in the history and assign new child IDs to the new tasks. If a task is replaced, mark it as superseded rather than silently renaming it away.
- Refer to active work, progress notes, evidence, and handoffs by task ID as well as by human-readable title.
- If a task would touch many unrelated areas or require a long uninterrupted run, split it before execution.
- After each completed task, update the current-state note, record evidence, and choose the next task.

### Plan and Govern the Work

- Plan at three levels: overall direction, optional checkpoints, and near-term executable tasks. Only add long-range date plans when external commitments require them.
- Map dependencies explicitly, including environments, data, approvals, vendors, quotas, and external systems when they matter.
- Calculate and monitor a critical path only when an external deadline, approval gate, launch window, or scarce bottleneck makes it useful.
- Plan scarce resources only when they constrain throughput: operator attention, CI capacity, API quotas, model budget, environment access, or permissions.
- Treat scope change as a trade-off decision, not as a free addition.
- Govern by evidence and explicit triggers. Do not introduce recurring rituals unless they improve control for this specific project.

### Run a Quality-First Delivery Loop

- Before implementation, define the smallest credible proof that the change is correct: failing repro, automated test, expected output, screenshot check, contract check, or exact manual procedure.
- Use the default sequence `explore -> plan -> implement -> verify -> review -> document`.
- Record evidence, not just conclusions: commands run, outputs, screenshots, metrics, and review notes tied to the task ID.
- Preserve explicit invariants and change budgets for every risky task: file scope, public interfaces that must stay stable, data or migration safety, and rollback or escalation triggers.
- When automated tests are missing, create the fastest credible verification method instead of skipping validation.
- Require a fresh-context review pass for risky, cross-cutting, or high-impact changes. Use a dedicated review step or review agent with a bug, regression, security, and maintainability lens.
- Pilot large automated or repetitive changes on a narrow slice before scaling across the codebase.
- If the same failure repeats twice, stop, strengthen the docs, rules, or validators, and restart with cleaner context instead of stacking corrections.

### Control Quality, Value, and Learning

- Separate user testing for product quality from user research for product value.
- Treat non-functional requirements as release criteria, not deferred polish.
- Keep documentation living: versioned, owned, refreshed, and retired when stale.
- Turn repeated failures into process, tooling, documentation, or policy improvements.

### Extend the System for Agent-Assisted Delivery

- Keep durable task state in files, not only in chat.
- Keep CLAUDE.md entry-point instructions short and navigational.
- Layer instructions close to the code with short `CLAUDE.md` files and linked deeper references rather than one large root manual.
- Use vendor-neutral handoff artifacts so different sessions can continue work safely.
- Use subagents only for bounded parallel work or high-volume output.
- Prefer deterministic hooks or validators for zero-exception checks such as required lint or test commands, path restrictions, and secret scanning.
- Use an independent review step or review-focused subagent when the implementation context is likely to be biased toward its own plan.
- Enforce least privilege, secret-handling rules, trust boundaries, and explicit operator approval for risky actions.
- Revalidate prompts and workflows with evals when behavior or tooling changes.

## Common Deliverables

- operator project plan
- micro-task backlog or execution queue with stable task IDs
- project rescue assessment
- artifact checklist tailored to lifecycle
- dependency and sequencing analysis
- risk, quality, and release-control plan
- agentic execution and guardrail plan
- verification matrix and evidence pack
- review checklist or review prompt for risky work
- external-constraint addendum, only when deadlines, approvals, vendors, or launch windows matter

## Reference Files

- Read [references/project-rulebook.md](./references/project-rulebook.md) for the full rule system and coverage map.
- Read [references/external-constraints.md](./references/external-constraints.md) only when the project has fixed deadlines, approval gates, vendor dependencies, quota caps, launch windows, or production release risk.
- Read [references/ai-agent-practices.md](./references/ai-agent-practices.md) when planning file-backed memory, subagents, evals, quality loops, and guardrails.
- Read [references/source-anchors.md](./references/source-anchors.md) when you need provenance, volatile vendor anchors, or a refresh point for unstable topics.
- Do not load every reference by default. Read the smallest relevant file first.

## Output Standards

- Write in imperative form.
- Prefer concrete artifacts and decision-ready outputs over generic PM advice.
- Make assumptions explicit whenever the workspace does not contain enough project context.
- Distinguish stable control practices from volatile vendor recommendations.
- Prefer task queues over milestone-only plans.
- Default task format: `Task ID`, `Task`, `Scope`, `Depends on`, `Done when`, `Verify with`, `Evidence`, and `Stop after`.
- When reporting progress or selecting next work, reference the task ID first.
- When in doubt, split work into smaller tasks before execution.
- Default quality package: invariants to preserve, exact verification steps, evidence to capture, review focus, and rollback trigger when relevant.
- Prefer one reviewable diff per execution task.
- For large automated changes, require a pilot slice before full rollout.
- Do not introduce date plans, budget tracking, approval workflows, recurring cadences, or stage gates unless the project genuinely depends on them.
- If the user asks for the latest model, benchmark, or vendor workflow guidance, verify it externally before answering because the bundled source anchors are point-in-time snapshots.
