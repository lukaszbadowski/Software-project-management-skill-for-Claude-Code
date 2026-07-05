# Software Project Rules

This is the audit and rescue reference bundled with the `software-project-management-for-claude` skill. `SKILL.md` is the operating spec; read this file when diagnosing a drifting project, auditing an existing control system, or deciding whether a control is worth adding. It is written for software projects run by a single human operator using Claude Code with agents or subagents. Source anchors refer to [source-anchors.md](./source-anchors.md).

Conventions:

- Rules apply to all control modes (solo operator, feedback-heavy, external-constraint, release-safety, agentic) unless an `Applies to` line narrows them.
- `Requires` names the artifact that proves the rule is being followed. Default artifacts live as sections in the canonical `pm/` files defined in [file-templates.md](./file-templates.md).
- `Prevents` names the failure the rule exists to stop.

## Table of Contents
- Universal Rules
- Project Prerequisites and Readiness Checks
- Lifecycle Selection and Tailoring Rules
- Operator Control Model
- Scope, Requirements, and Acceptance Criteria
- Planning: Backlog, Estimates, Dependencies, Critical Path, Resources, Budget
- Execution, Handoffs, and Stage Transitions
- Monitoring and Control
- Quality Engineering and Test Strategy
- User Research and Value Feedback Loops
- Documentation System
- Release, Operational Readiness, and Closure
- AI-Agent Operating Rules
- Recent Vendor and Benchmark Shifts
- Appendix A - Artifact-to-File Map
- Appendix B - Control-Mode Mapping

## Universal Rules

### R01 - Define the value outcome before choosing process
- Requires: problem statement, user or business outcome, success criteria
- Prevents: optimizing workflow while missing the real goal
- Sources: [S01] [S04] [S13]

### R02 - Keep one explicit operator decision record
- Requires: operator decision record, open-decisions list
- Prevents: thrash, contradictory choices across sessions, hidden assumptions
- Sources: [S04] [S15] [S16]

### R03 - Keep one visible system of record for project truth
- Requires: the `pm/` files as source-of-truth, linked working artifacts
- Prevents: rediscovery, stale assumptions, fragmented context after resets
- Sources: [S15] [S16] [S19]

### R04 - Make each meaningful work item bounded, testable, and resumable
- Requires: decomposed work item, acceptance criteria, explicit stop point, resume-ready note
- Prevents: vague tasks, repeated restarts, unverifiable progress
- Sources: [S07] [S09] [S15]

### R04A - Use milestones only as grouping; execute through small tasks
- Requires: milestone or checkpoint map when useful, ordered task queue, task sizing rule
- Prevents: long opaque runs, oversized diffs, weak operator visibility, poor recovery after interruption
- Sources: [S07] [S15] [S16] [S19]

### R04B - Give every execution task a stable identifier
- Requires: ordered task queue with stable task IDs, superseded or split-task history
- Prevents: ambiguous status, lost work tracking, broken continuity after renames
- Sources: [S15] [S16] [S19]

### R04C - Gate structure through operator checkpoints
- Requires: CP1-CP4 approval markers with dates in `pm/PLAN.md` and `pm/TASKS.md`
- Prevents: plausible but un-ratified plans, breakdowns the operator never consciously approved, "done" declared without operator acceptance
- Sources: [S03] [S05] [S09]

## Project Prerequisites and Readiness Checks

### R05 - Do not start without a success definition and authority to proceed
- Requires: explicit go signal, success criteria, stop conditions
- Prevents: shadow work, endless setup, vague "just explore" execution
- Sources: [S04] [S05]

### R06 - Surface hidden constraints early
- Requires: constraint log covering NFRs, architecture, environments, permissions, release exposure, data readiness, quotas, compliance, vendor dependencies where relevant
- Prevents: late surprises in performance, security, data, release, or integration
- Sources: [S04] [S10] [S12]

### R07 - Prepare environments, data, and access as first-class work
- Requires: environment plan, access checklist, test-data plan
- Prevents: blocked runs, fake progress, invalid testing
- Sources: [S04] [S12] [S16]

### R08 - Identify the real bottlenecks before planning around them
- Requires: bottleneck map; in solo projects the limiter is often operator attention, CI, API quotas, model budget, or one external dependency
- Prevents: plans that look reasonable but ignore the actual limiter
- Sources: [S04] [S13] [S14] [S16]

## Lifecycle Selection and Tailoring Rules

### R09 - Default to the solo-operator control mode
- Requires: objective, story breakdown, small task queue with stable IDs, acceptance criteria, dependency sequence, durable current-state note
- Prevents: bloated process and unnecessary management artifacts
- Sources: [S01] [S04] [S15]

### R10 - Add external-constraint controls only when fixed commitments are real
- Applies to: external-constraint, release-safety
- Requires: constraint log, gate list, minimal critical-path or date-risk view, fallback assumptions
- Prevents: under-controlling a real deadline or over-controlling a normal project
- Sources: [S05] [S08]

### R11 - Add feedback-heavy loops when learning dominates
- Applies to: feedback-heavy
- Requires: prioritized backlog, research questions, review trigger, scope-refresh trigger
- Prevents: locking detail too early and learning too slowly
- Sources: [S01] [S02] [S03] [S11] [S12]

### R12 - Add release-safety controls when real software will be shipped
- Applies to: release-safety, external-constraint
- Requires: release checklist, rollback note, monitoring checks, operator run notes
- Prevents: fragile launches and unsupported post-release states
- Sources: [S04] [S12] [S16]

## Operator Control Model

### R13 - Keep decisions explicit and local to the operator
- Requires: decision log, unresolved-decisions list, assumption log
- Prevents: contradictory instructions across agent runs, control lost to memory or chat
- Sources: [S15] [S16] [S19]

### R14 - Govern through evidence and triggers, not rituals
- Requires: review triggers, evidence pack, change trigger
- Prevents: status theater and process drag
- Sources: [S02] [S05] [S12]

### R15 - Add outside approvals only when they are unavoidable
- Applies to: external-constraint, release-safety
- Requires: approval checklist, required evidence, lead-time assumption
- Prevents: unnecessary waiting paths or missing real approvals
- Sources: [S04] [S05] [S10]

## Scope, Requirements, and Acceptance Criteria

### R16 - Separate outcome scope from solution scope
- Requires: outcome statement, in-scope items, out-of-scope items, assumptions
- Prevents: premature solution lock-in and hidden scope growth
- Sources: [S04] [S09]

### R17 - Maintain a controlled decomposition of total work
- Requires: story breakdown or backlog, ordered task queue with stable IDs, dependency markers, current priority
- Prevents: missing work, duplicate work, vague execution
- Sources: [S07] [S09]

### R18 - Attach acceptance and quality conditions to every substantial scope item
- Requires: acceptance criteria, NFRs where relevant, definition of done or equivalent
- Prevents: plausible but wrong outputs and rework after "done"; agents need explicit checks, not implied intent
- Sources: [S03] [S04] [S09]

### R18A - Maintain traceability from success criteria to stories, tasks, and evidence
- Requires: traceability map in `pm/PLAN.md` (SC to ST), story references on tasks, evidence per task, CP4 re-verification of every success criterion end-to-end
- Prevents: all tasks green while the product misses the goal; completion inferred from unit-level checks
- Sources: [S04] [S09]

## Planning: Backlog, Estimates, Dependencies, Critical Path, Resources, Budget

### R19 - Plan at three levels: overall direction, optional checkpoints, near-term executable tasks
- Requires: roadmap or execution map, optional checkpoint map, near-term task queue with stable IDs, refresh trigger
- Prevents: detail paralysis or vague optimism
- Sources: [S05] [S06] [S12]

### R20 - Map dependencies explicitly, including non-code dependencies
- Requires: dependency map or sequence, blocking assumptions; environments, data, vendor APIs, approvals, and quotas often dominate delivery risk
- Prevents: blocked work and false confidence from local task completion
- Sources: [S04] [S05] [S08]

### R21 - Calculate a critical path only when timing or gates actually matter
- Applies to: external-constraint, release-safety
- Requires: sequence model, gating assumptions, review trigger for the critical path
- Prevents: missing the true sequence drivers on a real deadline
- Sources: [S05] [S08]

### R22 - Estimate with explicit assumptions and confidence, not single-number certainty
- Requires: estimate basis, confidence note, refresh trigger
- Prevents: pseudo-precision and surprise drift
- Sources: [S04] [S08]

### R23 - Track spend or quota only when money, credits, or limits are real constraints
- Applies to: external-constraint, agentic
- Requires: budget or quota note, burn trigger, fallback path
- Prevents: runaway usage or needless budgeting overhead
- Sources: [S04] [S13] [S16]

### R24 - Refresh commitments when reality changes
- Requires: variance log, replanning trigger, recovery options
- Prevents: false confidence from a stale plan, late surprise slippage
- Sources: [S05] [S12] [S13]

## Execution, Handoffs, and Stage Transitions

### R25 - Start work only when the inputs are ready enough to succeed
- Requires: definition of ready, dependency clearance, input package, task-sized boundary
- Prevents: churn disguised as progress, repeated clarification loops
- Sources: [S03] [S09] [S15]

### R26 - Hand off artifacts, evidence, and unresolved risks together
- Requires: handoff note with task IDs, outputs, evidence, open issues and risks
- Prevents: dropped context; a handoff is complete only when the next run continues without rediscovery
- Sources: [S05] [S15] [S16] [S19]

### R27 - Treat transitions as deliverables when tools or release stages change
- Requires: transition checklist, changed assumptions, next-step note
- Prevents: "almost done" projects that fail during the switch
- Sources: [S04] [S12] [S16]

## Monitoring and Control

### R28 - Measure progress through completed evidence, not effort spent
- Requires: evidence log, current-state note, deliverable checks
- Prevents: percent-complete illusions
- Sources: [S03] [S05] [S12]

### R29 - Keep separate logs for risks, issues, and changes
- Requires: risk, issue, and change sections in `pm/DECISIONS.md`
- Prevents: confused control; threats, active problems, and scope changes need different responses
- Sources: [S10]

### R30 - Estimate risks with triggers and responses, not only labels
- Requires: risk entries with impact, trigger, and response
- Prevents: vague risk tracking with no action path
- Sources: [S10]

### R31 - Inspect and adapt on fixed triggers, not by accident
- Requires: review trigger, retrospective or learning trigger, action list
- Prevents: repeated mistakes and late drift detection
- Sources: [S02] [S03] [S12] [S14]

### R32 - Treat scope changes as trade-off decisions, not free additions
- Requires: change record, impact note, updated forecast or sequence, checkpoint re-approval when structural
- Prevents: silent scope creep
- Sources: [S05] [S06]

## Quality Engineering and Test Strategy

### R33 - Design quality in before building, then verify continuously
- Requires: quality criteria, review strategy, test strategy
- Prevents: late defect discovery; quality cannot be added after the system is already wrong
- Sources: [S03] [S04]

### R34 - Use layered testing that matches software risk
- Requires: test layers, environment matrix, test-data plan
- Prevents: gaps caused by overreliance on one test type
- Sources: [S04] [S11]

### R34A - Define the verification ladder and evidence pack before implementation
- Requires: verification ladder, exact commands or checks, evidence capture plan
- Prevents: false-positive completion and "works for me" claims; an agent that cannot prove a change works will guess
- Sources: [S22]

### R35 - Treat non-functional requirements as acceptance or release criteria
- Requires: NFR list, thresholds, validation method
- Prevents: technically complete but operationally unacceptable releases
- Sources: [S04] [S10] [S12]

### R36 - Treat architecture and technical debt as managed scope
- Requires: architecture decision records, debt log, trade-off notes
- Prevents: hidden long-term degradation from structural shortcuts
- Sources: [S04] [S10] [S16]

## User Research and Value Feedback Loops

### R37 - Run user testing to improve product quality
- Applies to: feedback-heavy, release-safety
- Requires: usability test plan, participant criteria, findings log
- Prevents: shipping software that passes tests but fails real tasks
- Sources: [S11]

### R38 - Run user research to improve delivered value
- Applies to: feedback-heavy
- Requires: discovery research plan, research questions, decision log tied to findings
- Prevents: feature output with weak user value; building the right product differs from building the product right
- Sources: [S01] [S02] [S11] [S13]

### R39 - Feed research and review findings back into scope and process
- Requires: backlog or scope updates, changed assumptions, improvement actions
- Prevents: inert retrospectives and ignored research
- Sources: [S02] [S03] [S11] [S14]

## Documentation System

### R40 - Maintain a minimal entry-point map with deeper linked references
- Requires: short top-level index, linked topical docs, freshness markers
- Prevents: giant unreadable manuals and repeated repo rediscovery
- Sources: [S15] [S16] [S19]

### R41 - Review, refresh, and retire documentation continuously
- Requires: freshness trigger, stale-doc retirement path, update notes
- Prevents: incorrect decisions based on obsolete instructions; stale docs are active project risk
- Sources: [S12] [S16] [S19]

## Release, Operational Readiness, and Closure

### R42 - Plan cutover, rollback, and operating notes as project work when shipping
- Applies to: release-safety, external-constraint
- Requires: release plan, rollback plan, monitoring checks, operating notes
- Prevents: failed launches and unsupported live systems
- Sources: [S04] [S12] [S16]

### R43 - Close work by recording residual risks, debt, and next obligations
- Requires: residual risk log, debt list, lessons learned, next-step note
- Prevents: repeated mistakes and abandoned loose ends
- Sources: [S02] [S05] [S14]

## AI-Agent Operating Rules

### R44 - Store durable task state in files, not only in chat
- Requires: the `pm/` files: plan, task queue with stable IDs, state note, decision log
- Prevents: context-window dependence and task amnesia; chat context is transient, files survive sessions
- Sources: [S15] [S16] [S19]

### R45 - Keep agent entry-point instructions short, stable, and navigational
- Requires: short CLAUDE.md root instructions, linked deeper references
- Prevents: bloated instruction files that crowd out the task and reduce adherence
- Sources: [S16] [S19]

### R46 - Make the codebase legible before expecting autonomy
- Requires: architecture map, runnable commands, boundary rules, searchable references
- Prevents: hallucinated structure and repeated rediscovery; what the agent cannot discover effectively does not exist
- Sources: [S15] [S16]

### R47 - Make every autonomous task acceptance-driven and short enough to inspect
- Requires: task ID, acceptance criteria, exact commands, success condition, explicit stop condition, escalation rule
- Prevents: plausible-looking but unverifiable work and long opaque runs
- Sources: [S15]

### R47A - Use a fresh-context review pass for risky or cross-cutting changes
- Requires: review checklist or prompt, review findings, resolution note
- Prevents: missed edge cases, security issues, and regressions; the context that wrote a change is biased toward its own plan
- Sources: [S20] [S22]

### R48 - Route work to the smallest model tier that can do it reliably
- Requires: `Route:` tier per task (light, standard, heavy), tier-to-model mapping in the active skill, escalation rule after two failures or low confidence, reviewer tier at least writer tier
- Prevents: paying heavy-model prices for mechanical work, and light models silently owning risky decisions
- Sources: [S17] [S18]

### R49 - Prefer subagents for autonomy-ready bounded work that protects main context
- Requires: scoped subtask brief, expected output, verification command, expected evidence, tool limits
- Prevents: context pollution and main-thread drift into low-signal execution detail
- Sources: [S20] [S22]

### R50 - Enforce least privilege and explicit operator approval paths
- Requires: permission mode, hook rules, destructive-action policy, escalation rules
- Prevents: accidental destructive behavior and overbroad access
- Sources: [S21]

### R51 - Convert repeated failures into documentation, tooling, or policy improvements
- Requires: failure log, updated docs or tools, validation of the improvement
- Prevents: paying the same coordination tax every run
- Sources: [S13] [S14] [S16]

### R52 - Treat evals as required infrastructure for prompt and workflow changes
- Requires: eval set, regression checks, change note
- Prevents: silent degradation masked by anecdotal wins
- Sources: [S13] [S14]

### R53 - Prefer mechanical invariants over taste-by-conversation
- Requires: structural checks, lint rules, boundary tests, repo conventions
- Prevents: style drift, boundary erosion, inconsistent outputs
- Sources: [S16]

### R53A - Encode zero-exception quality checks in deterministic guardrails when possible
- Requires: hook or validator configuration, blocking rules, scope note
- Prevents: skipped validation and policy drift under pressure; advice drifts, deterministic enforcement does not
- Sources: [S21] [S22] [S23]

### R54 - Use vendor-neutral handoff artifacts for cross-session interoperability
- Requires: task brief, current task ID, current-state summary, exact file list, commands run, expected next action
- Prevents: hidden-context handoffs and session-specific dead ends
- Sources: [S15] [S16] [S19]

### R55 - Define trust boundaries for agent inputs, secrets, and side effects
- Requires: trust-boundary policy, secret-handling rules, external-input policy, signoff rules for privileged actions
- Prevents: prompt-injection-driven actions, secret exposure, unsafe automation
- Sources: [S16] [S21]

## Recent Vendor and Benchmark Shifts

### R56 - Assume benchmark claims are provisional until reproduced on your own tasks
- Requires: local eval suite, benchmark interpretation note
- Prevents: overtrusting leaderboard wins that do not transfer
- Sources: [S13] [S14]

### R57 - Assume models, costs, and capabilities will drift; revalidate routing and prompts when conditions change
- Requires: revalidation trigger, routing refresh, prompt or eval refresh
- Prevents: stale optimization choices and degraded reliability
- Sources: [S17] [S18]

### R58 - Treat operator attention as a scarce resource and design around it
- Requires: attention bottleneck note, automation strategy, review trigger
- Prevents: hidden review bottlenecks; the real critical path is often what the operator must inspect manually
- Sources: [S13] [S14] [S16]

### R58A - Pilot large automated changes on a narrow slice before scaling out
- Requires: pilot slice, scale-out trigger, stop trigger, refinement note
- Prevents: repo-wide low-quality churn and hard-to-undo mass edits
- Sources: [S22]

## Appendix A - Artifact-to-File Map

| Artifact | Lives in | Purpose |
| --- | --- | --- |
| Objective and success criteria | `pm/PLAN.md` | Defines what valuable completion means |
| Scope and exclusions | `pm/PLAN.md` | Prevents silent scope creep |
| Story breakdown with acceptance | `pm/PLAN.md` | Operator-approved units of value |
| Traceability map | `pm/PLAN.md` | Ties success criteria to stories, tasks, evidence |
| Checkpoint approvals | `pm/PLAN.md`, `pm/TASKS.md` | Records conscious operator sign-off |
| Task queue with stable IDs and routing | `pm/TASKS.md` | Next small executable units, traceable through renames |
| Dependency markers | `pm/TASKS.md` | Makes blockers visible |
| Verification and evidence per task | `pm/TASKS.md` | Verifies quality, survives handoffs |
| Current-state and handoff note | `pm/STATE.md` | Preserves continuity across sessions and tools |
| Operator decision record | `pm/DECISIONS.md` | Preserves choices and unresolved decisions |
| Risk register, issue log, change log | `pm/DECISIONS.md` | Tracks threats, problems, and scope changes |
| External-constraint log | `pm/CONSTRAINTS.md` (branch) | Gates, vendors, quotas, dates when real |
| Release checklist and rollback note | `pm/RELEASE.md` (branch) | Safe deployment when shipping |
| Research questions and findings | `pm/RESEARCH.md` (branch) | Learning loop when discovery dominates |
| Architecture and design records | repo docs, linked | Preserves technical intent |
| Environment and data setup docs | repo docs, linked | Enables reproducible execution |
| Eval suite | repo, linked | Regresses agent behavior on workflow changes |
| Guardrail and permission rules | tool config, hooks | Prevents unsafe actions |

## Appendix B - Control-Mode Mapping

| Mode | When to use it | What to add |
| --- | --- | --- |
| Solo operator default | One operator runs the project through Claude Code with no hard outside gate | The four `pm/` files, checkpoints CP1-CP4, routed task queue, tests or evals, guardrails |
| Feedback-heavy | User learning or UX uncertainty dominates | `pm/RESEARCH.md`: research questions, findings log, scope-refresh loop |
| External-constraint | Fixed date, approval gate, vendor dependency, quota cap, or launch window exists | `pm/CONSTRAINTS.md`: constraint log, minimal critical path, gate evidence, fallback assumptions |
| Release-safety | Real software will be deployed or handed to users | `pm/RELEASE.md`: release checklist, rollback plan, monitoring checks, operating notes |
| Agentic | Claude Code agents or subagents perform substantial execution | CLAUDE.md entry-point rules, task-state files, model routing, evals, trust boundaries |

The former Appendix C (question coverage map from the original research pack) moved to the research workspace; it documented research completeness, not runtime behavior.
