# Software Project Rules

This document is the master rulebook bundled with the `software-project-management-for-claude` skill. It is written for software projects run by a single human operator using Claude Code with agents or subagents. Source anchors refer to [source-anchors.md](./source-anchors.md).

## Table of Contents
- Purpose and How to Use This Document
- Universal Rules
- Project Prerequisites and Readiness Checks
- Lifecycle Selection and Tailoring Rules
- Operator Control Model
- Scope, Requirements, and Acceptance Criteria
- Planning: Backlog, Estimates, Dependencies, Critical Path, Resources, Budget
- Execution, Handoffs, and Stage Transitions
- Monitoring and Control: Status, Metrics, Forecasting, Issue/Risk/Change Control
- Quality Engineering and Test Strategy
- User Research, Usability Testing, and Value Feedback Loops
- Documentation System and Living Documentation
- Release, Operational Readiness, and Closure
- AI-Agent Operating Rules
- Recent Vendor and Benchmark Shifts
- Appendix A - Artifact Checklist
- Appendix B - Control-Mode Mapping
- Appendix C - Question Coverage Map

## Purpose and How to Use This Document
- Use this file as a rulebook for projects steered by one operator and executed partly or mostly through Claude Code agents or subagents.
- Default to the lightest control system that still preserves continuity: scope, small executable tasks, acceptance, dependency sequencing, durable files, tests or evals, change control, and permissions.
- Add dates, budgets, approval paths, vendor calendars, or release-window logic only when those external constraints are real. [S04] [S05] [S08]
- Treat the rules as a control system, not as ceremony. The goal is reliable value delivery under actual constraints. [S01] [S04] [S13]

## Universal Rules

### R01 - Define the value outcome before choosing process
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: problem statement, user or business outcome, success criteria
- Why it matters: process choice only makes sense after the operator knows what outcome the project must produce.
- Failure prevented: optimizing workflow while missing the real goal
- Source anchors: [S01] [S04] [S13]

### R02 - Keep one explicit operator decision record
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: operator decision record, open-decisions list
- Why it matters: solo projects still fail when decisions stay implicit or scattered.
- Failure prevented: thrash, contradictory choices across sessions, hidden assumptions
- Source anchors: [S04] [S15] [S16]

### R03 - Keep one visible system of record for project truth
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: source-of-truth index, linked working artifacts
- Why it matters: project state must survive context resets and interruptions.
- Failure prevented: rediscovery, stale assumptions, fragmented context
- Source anchors: [S15] [S16] [S19]

### R04 - Make each meaningful work item bounded, testable, and resumable
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: decomposed work item, acceptance criteria, explicit stop point, resume-ready note
- Why it matters: if a task cannot be checked or resumed, it is not ready for reliable agentic execution.
- Failure prevented: vague tasks, repeated restarts, unverifiable progress
- Source anchors: [S07] [S09] [S15]

### R04A - Use milestones only as grouping; execute through small tasks
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: milestone or checkpoint map when useful, ordered task queue, task sizing rule
- Why it matters: milestones help orientation but they are too coarse to be safe default execution units for Claude Code.
- Failure prevented: long opaque runs, oversized diffs, weak operator visibility, and poor recovery after interruption
- Source anchors: [S07] [S15] [S16] [S19]

### R04B - Give every execution task a stable identifier
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: ordered task queue with stable task IDs, superseded or split-task history where relevant
- Why it matters: task titles change as understanding improves, but the operator still needs a stable handle for progress, review, and handoff.
- Failure prevented: losing track of what was worked on, ambiguous status updates, and broken continuity after task renames
- Source anchors: [S15] [S16] [S19]

## Project Prerequisites and Readiness Checks

### R05 - Do not start without a success definition and authority to proceed
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: mandate or explicit go signal, success criteria, stop conditions
- Why it matters: even a solo project needs a clear basis for starting and stopping.
- Failure prevented: shadow work, endless setup, vague "just explore" execution
- Source anchors: [S04] [S05]

### R06 - Surface hidden constraints early
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: constraint log covering NFRs, architecture, environments, permissions, release exposure, data readiness, quotas, compliance, and vendor dependencies where relevant
- Why it matters: most software slips come from forgotten constraints, not from typing speed.
- Failure prevented: late surprises in performance, security, data, release, or integration
- Source anchors: [S04] [S10] [S12]

### R07 - Prepare environments, data, and access as first-class work
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: environment plan, access checklist, test-data plan
- Why it matters: execution stalls when access and setup are treated as background chores.
- Failure prevented: blocked runs, fake progress, invalid testing
- Source anchors: [S04] [S12] [S16]

### R08 - Identify the real bottlenecks before planning around them
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: bottleneck map, capacity or quota note where relevant
- Why it matters: in solo operator projects the constraint is often operator attention, CI, API quotas, model budget, environment access, or a single external dependency.
- Failure prevented: plans that look reasonable but ignore the actual limiter
- Source anchors: [S04] [S13] [S14] [S16]

## Lifecycle Selection and Tailoring Rules

### R09 - Default to the solo-operator control mode
- Applies to: solo operator, agentic
- Required artifacts: objective, work breakdown, small task queue with stable IDs, acceptance criteria, dependency sequence, durable current-state note
- Why it matters: most Claude Code work does not need extra ceremony.
- Failure prevented: bloated process and unnecessary management artifacts
- Source anchors: [S01] [S04] [S15]

### R10 - Add external-constraint controls only when fixed commitments are real
- Applies to: external-constraint, release-safety
- Required artifacts: constraint log, gate list, minimal critical-path or date-risk view, fallback assumptions
- Why it matters: dates, approvals, launch windows, and vendor commitments require tighter control, but only when they truly exist.
- Failure prevented: either under-controlling a real deadline or over-controlling a normal project
- Source anchors: [S05] [S08]

### R11 - Add feedback-heavy loops when learning dominates
- Applies to: feedback-heavy, solo operator
- Required artifacts: prioritized backlog, research questions, review trigger, scope-refresh trigger
- Why it matters: discovery work benefits from deliberate inspection and adaptation.
- Failure prevented: locking detail too early and learning too slowly
- Source anchors: [S01] [S02] [S03] [S11] [S12]

### R12 - Add release-safety controls when real software will be shipped
- Applies to: release-safety, external-constraint
- Required artifacts: release checklist, rollback note, monitoring checks, operator run notes
- Why it matters: delivery is not finished when the code compiles; it is finished when the release can be operated safely.
- Failure prevented: fragile launches and unsupported post-release states
- Source anchors: [S04] [S12] [S16]

## Operator Control Model

### R13 - Keep decisions explicit and local to the operator
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: decision log, unresolved-decisions list, assumption log
- Why it matters: one operator can still lose control if decisions live only in memory or chat.
- Failure prevented: contradictory instructions across agent runs
- Source anchors: [S15] [S16] [S19]

### R14 - Govern through evidence and triggers, not rituals
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: review triggers, evidence pack, change trigger
- Why it matters: recurring rituals are only useful when they improve decisions.
- Failure prevented: status theater and process drag
- Source anchors: [S02] [S05] [S12]

### R15 - Add outside approvals only when they are unavoidable
- Applies to: external-constraint, release-safety
- Required artifacts: approval checklist, required evidence, lead-time assumption
- Why it matters: approvals are a constraint branch, not a default operating model.
- Failure prevented: unnecessary waiting paths or missing real approvals
- Source anchors: [S04] [S05] [S10]

## Scope, Requirements, and Acceptance Criteria

### R16 - Separate outcome scope from solution scope
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: outcome statement, in-scope items, out-of-scope items, assumptions
- Why it matters: the operator must know what result is required before locking in how to get there.
- Failure prevented: premature solution lock-in and hidden scope growth
- Source anchors: [S04] [S09]

### R17 - Maintain a controlled decomposition of total work
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: work breakdown or backlog, ordered task queue with stable IDs, dependency markers, current priority
- Why it matters: decomposition is the basis for sequencing, estimation, and handoff safety.
- Failure prevented: missing work, duplicate work, and vague execution
- Source anchors: [S07] [S09]

### R18 - Attach acceptance and quality conditions to every substantial scope item
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: acceptance criteria, NFRs where relevant, definition of done or equivalent
- Why it matters: agents need explicit checks, not implied intent.
- Failure prevented: plausible but wrong outputs and rework after "done"
- Source anchors: [S03] [S04] [S09]

## Planning: Backlog, Estimates, Dependencies, Critical Path, Resources, Budget

### R19 - Plan at three levels: overall direction, optional checkpoints, and near-term executable tasks
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: roadmap or execution map, optional checkpoint map, near-term task queue with stable IDs, refresh trigger
- Why it matters: the operator needs direction without turning checkpoints into oversized execution units.
- Failure prevented: either detail paralysis or vague optimism
- Source anchors: [S05] [S06] [S12]

### R20 - Map dependencies explicitly, including non-code dependencies
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: dependency map, dependency sequence, blocking assumptions
- Why it matters: environments, data, vendor APIs, approvals, and quotas often dominate delivery risk.
- Failure prevented: blocked work and false confidence from local task completion
- Source anchors: [S04] [S05] [S08]

### R21 - Calculate a critical path only when timing or gates actually matter
- Applies to: external-constraint, release-safety
- Required artifacts: sequence model, gating assumptions, review trigger for the critical path
- Why it matters: most solo Claude Code projects do not need date math, but externally timed work does.
- Failure prevented: missing the true sequence drivers on a real deadline
- Source anchors: [S05] [S08]

### R22 - Estimate with explicit assumptions and confidence, not single-number certainty
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: estimate basis, confidence note, refresh trigger
- Why it matters: estimates are only useful when their assumptions are visible.
- Failure prevented: pseudo-precision and surprise drift
- Source anchors: [S04] [S08]

### R23 - Track spend or quota only when money, credits, or limits are real constraints
- Applies to: external-constraint, agentic
- Required artifacts: budget or quota note, burn trigger, fallback path
- Why it matters: spend control matters when it is real, not as default ceremony.
- Failure prevented: runaway usage or needless budgeting overhead
- Source anchors: [S04] [S13] [S16]

### R24 - Refresh commitments when reality changes
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: variance log, replanning trigger, recovery options
- Why it matters: a stale plan creates false confidence.
- Failure prevented: late surprise slippage and unmanaged drift
- Source anchors: [S05] [S12] [S13]

## Execution, Handoffs, and Stage Transitions

### R25 - Start work only when the inputs are ready enough to succeed
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: definition of ready, dependency clearance, input package, task-sized boundary
- Why it matters: starting early without inputs creates churn disguised as progress.
- Failure prevented: blocked execution and repeated clarification loops
- Source anchors: [S03] [S09] [S15]

### R26 - Hand off artifacts, evidence, and unresolved risks together
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: handoff note with task IDs, outputs, evidence, open issues and risks
- Why it matters: a handoff is only complete when the next run can continue without rediscovery.
- Failure prevented: dropped context and broken continuity between sessions
- Source anchors: [S05] [S15] [S16] [S19]

### R27 - Treat transitions as deliverables when tools or release stages change
- Applies to: solo operator, external-constraint, release-safety, agentic
- Required artifacts: transition checklist, changed assumptions, next-step note
- Why it matters: integration and transition work is real work.
- Failure prevented: "almost done" projects that fail during the switch
- Source anchors: [S04] [S12] [S16]

## Monitoring and Control: Status, Metrics, Forecasting, Issue/Risk/Change Control

### R28 - Measure progress through completed evidence, not effort spent
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: evidence log, current-state note, deliverable checks
- Why it matters: visible outputs are a better progress signal than time invested.
- Failure prevented: percent-complete illusions
- Source anchors: [S03] [S05] [S12]

### R29 - Keep separate logs for risks, issues, and changes
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: risk register, issue log, change log
- Why it matters: risks, active problems, and scope changes need different responses.
- Failure prevented: confused control and weak mitigation
- Source anchors: [S10]

### R30 - Estimate risks with triggers and responses, not only labels
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: risk register with likelihood, impact, trigger, mitigation, contingency
- Why it matters: a risk list is only useful when it tells the operator what to watch and what to do.
- Failure prevented: vague risk tracking with no action path
- Source anchors: [S10]

### R31 - Inspect and adapt on fixed triggers, not by accident
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: review trigger, retrospective or learning trigger, action list
- Why it matters: problems worsen when learning only happens after failure.
- Failure prevented: repeated mistakes and late drift detection
- Source anchors: [S02] [S03] [S12] [S14]

### R32 - Treat scope changes as trade-off decisions, not free additions
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: change record, impact note, updated forecast or sequence
- Why it matters: every addition consumes time, attention, budget, or quality margin.
- Failure prevented: silent scope creep
- Source anchors: [S05] [S06]

## Quality Engineering and Test Strategy

### R33 - Design quality in before building, then verify continuously
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: quality criteria, review strategy, test strategy
- Why it matters: quality cannot be added after the system is already wrong.
- Failure prevented: late defect discovery and preventable rework
- Source anchors: [S03] [S04]

### R34 - Use layered testing that matches software risk
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: test layers, environment matrix, test-data plan
- Why it matters: different risks need different evidence.
- Failure prevented: gaps caused by overreliance on one test type
- Source anchors: [S04] [S11]

### R34A - Define the verification ladder and evidence pack before implementation
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: verification ladder, exact commands or checks, evidence capture plan
- Why it matters: if the agent cannot prove the change works, it will guess.
- Failure prevented: false-positive completion, weak handoffs, and "works for me" claims without evidence
- Source anchors: [S22]

### R35 - Treat non-functional requirements as acceptance or release criteria
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: NFR list, thresholds, validation method
- Why it matters: performance, security, accessibility, privacy, and operability often decide whether the software is actually shippable.
- Failure prevented: technically complete but operationally unacceptable releases
- Source anchors: [S04] [S10] [S12]

### R36 - Treat architecture and technical debt as managed scope
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: architecture decision records, debt log, trade-off notes
- Why it matters: structural shortcuts change future speed, cost, and reliability.
- Failure prevented: hidden long-term degradation
- Source anchors: [S04] [S10] [S16]

## User Research, Usability Testing, and Value Feedback Loops

### R37 - Run user testing to improve product quality
- Applies to: feedback-heavy, release-safety, solo operator
- Required artifacts: usability test plan, participant criteria, findings log
- Why it matters: users expose quality problems that internal tests do not.
- Failure prevented: shipping software that passes tests but fails real tasks
- Source anchors: [S11]

### R38 - Run user research to improve delivered value
- Applies to: feedback-heavy, solo operator
- Required artifacts: discovery research plan, research questions, decision log tied to findings
- Why it matters: building the right product is different from building the product right.
- Failure prevented: feature output with weak user value
- Source anchors: [S01] [S02] [S11] [S13]

### R39 - Feed research and review findings back into scope and process
- Applies to: feedback-heavy, solo operator, release-safety, agentic
- Required artifacts: backlog or scope updates, changed assumptions, improvement actions
- Why it matters: feedback matters only when it changes what happens next.
- Failure prevented: inert retrospectives and ignored research
- Source anchors: [S02] [S03] [S11] [S14]

## Documentation System and Living Documentation

### R40 - Maintain a minimal entry-point map with deeper linked references
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: top-level index, linked topical docs, freshness markers
- Why it matters: the operator and the agents need navigation before detail.
- Failure prevented: giant unreadable manuals and repeated repo rediscovery
- Source anchors: [S15] [S16] [S19]

### R41 - Review, refresh, and retire documentation continuously
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: freshness trigger, stale-doc retirement path, update notes
- Why it matters: stale docs are active project risk.
- Failure prevented: incorrect decisions based on obsolete instructions
- Source anchors: [S12] [S16] [S19]

## Release, Operational Readiness, and Closure

### R42 - Plan cutover, rollback, and operating notes as project work when shipping
- Applies to: release-safety, external-constraint
- Required artifacts: release plan, rollback plan, monitoring checks, operating notes
- Why it matters: release safety is part of delivery, not postscript work.
- Failure prevented: failed launches and unsupported live systems
- Source anchors: [S04] [S12] [S16]

### R43 - Close work by recording residual risks, debt, and next obligations
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: residual risk log, debt list, lessons learned, next-step note
- Why it matters: closure turns one project's cost into future capability.
- Failure prevented: repeated mistakes and abandoned loose ends
- Source anchors: [S02] [S05] [S14]

## AI-Agent Operating Rules

### R44 - Store durable task state in files, not only in chat
- Applies to: agentic, solo operator, feedback-heavy, external-constraint, release-safety
- Required artifacts: execution plan, ordered task queue with stable IDs, progress log, decision log, evidence log
- Why it matters: chat context is transient; files survive sessions.
- Failure prevented: context-window dependence and task amnesia
- Source anchors: [S15] [S16] [S19]

### R45 - Keep agent entry-point instructions short, stable, and navigational
- Applies to: agentic, solo operator
- Required artifacts: short CLAUDE.md root instructions, linked deeper references
- Why it matters: concise entry points preserve context budget and improve adherence.
- Failure prevented: bloated instruction files that crowd out the task
- Source anchors: [S16] [S19]

### R46 - Make the codebase legible before expecting autonomy
- Applies to: agentic, solo operator
- Required artifacts: architecture map, runnable commands, boundary rules, searchable references
- Why it matters: agents can only act reliably on what they can discover and verify.
- Failure prevented: hallucinated structure and repeated rediscovery
- Source anchors: [S15] [S16]

### R47 - Make every autonomous task acceptance-driven and short enough to inspect
- Applies to: agentic, solo operator
- Required artifacts: task ID, acceptance criteria, exact commands, success condition, explicit stop condition, escalation rule
- Why it matters: agents need clear checks and size boundaries before they act.
- Failure prevented: plausible-looking but unverifiable work and long opaque runs
- Source anchors: [S15]

### R47A - Use a fresh-context review pass for risky or cross-cutting changes
- Applies to: agentic, solo operator
- Required artifacts: review checklist or prompt, review findings, resolution note
- Why it matters: the context that wrote the change is biased toward its own plan; a second pass catches blind spots.
- Failure prevented: missed edge cases, security issues, regression holes, and maintainability surprises
- Source anchors: [S20] [S22]

### R48 - Route work to the smallest agent type that can do it reliably
- Applies to: agentic, solo operator
- Required artifacts: routing rule, stronger-agent trigger, cost note when relevant
- Why it matters: token efficiency is a workflow design problem, not a finance afterthought.
- Failure prevented: waste and unnecessary latency
- Source anchors: [S17] [S18]

### R49 - Prefer subagents for autonomy-ready bounded work that protects main context
- Applies to: agentic, solo operator
- Required artifacts: scoped subtask brief, expected output, verification command, expected evidence, tool limits
- Why it matters: the main thread should preserve context for requirements, decomposition, synthesis, and sign-off while delegated agents handle noisy bounded execution.
- Failure prevented: context pollution, duplicated analysis, and main-thread drift into low-signal execution detail
- Source anchors: [S20] [S22]

### R50 - Enforce least privilege and explicit operator approval paths
- Applies to: agentic, solo operator
- Required artifacts: permission mode, hook rules, destructive-action policy, escalation rules
- Why it matters: autonomous tooling without permission boundaries is unsafe.
- Failure prevented: accidental destructive behavior and overbroad access
- Source anchors: [S21]

### R51 - Convert repeated failures into documentation, tooling, or policy improvements
- Applies to: agentic, solo operator
- Required artifacts: failure log, updated docs or tools, validation of the improvement
- Why it matters: repeated operator intervention means the system has not learned yet.
- Failure prevented: paying the same coordination tax every run
- Source anchors: [S13] [S14] [S16]

### R52 - Treat evals as required infrastructure for prompt and workflow changes
- Applies to: agentic, solo operator
- Required artifacts: eval set, regression checks, change note
- Why it matters: agent systems drift whenever prompts, tools, or policies change.
- Failure prevented: silent degradation masked by anecdotal wins
- Source anchors: [S13] [S14]

### R53 - Prefer mechanical invariants over taste-by-conversation
- Applies to: agentic, solo operator
- Required artifacts: structural checks, lint rules, boundary tests, repo conventions
- Why it matters: high-throughput agent systems stay coherent when the rules are encoded, not re-explained.
- Failure prevented: style drift, boundary erosion, inconsistent outputs
- Source anchors: [S16]

### R53A - Encode zero-exception quality checks in deterministic guardrails when possible
- Applies to: agentic, solo operator
- Required artifacts: hook or validator configuration, blocking rules, scope note
- Why it matters: advice drifts; deterministic enforcement keeps quality checks happening across sessions and contributors.
- Failure prevented: skipped validation steps, forbidden edits, and policy drift under time pressure
- Source anchors: [S21] [S22] [S23]

### R54 - Use vendor-neutral handoff artifacts for cross-session interoperability
- Applies to: agentic, solo operator
- Required artifacts: task brief, current task ID, current-state summary, exact file list, commands run, expected next action
- Why it matters: continuation across sessions only works when state is explicit and portable.
- Failure prevented: hidden-context handoffs and session-specific dead ends
- Source anchors: [S15] [S16] [S19]

### R55 - Define trust boundaries for agent inputs, secrets, and side effects
- Applies to: agentic, solo operator
- Required artifacts: trust-boundary policy, secret-handling rules, external-input policy, signoff rules for privileged actions
- Why it matters: fetched content, generated code, and third-party text are not safe privileged instructions.
- Failure prevented: prompt-injection-driven actions, secret exposure, unsafe automation
- Source anchors: [S16] [S21]

## Recent Vendor and Benchmark Shifts

### R56 - Assume benchmark claims are provisional until reproduced on your own tasks
- Applies to: agentic, solo operator
- Required artifacts: local eval suite, benchmark interpretation note
- Why it matters: public coding benchmarks can be contaminated or misaligned with real work.
- Failure prevented: overtrusting leaderboard wins that do not transfer
- Source anchors: [S13] [S14]

### R57 - Assume models, costs, and capabilities will drift; revalidate routing and prompts when conditions change
- Applies to: agentic, solo operator
- Required artifacts: revalidation trigger, routing refresh, prompt or eval refresh
- Why it matters: model capabilities, snapshots, and reasoning tradeoffs change over time.
- Failure prevented: stale optimization choices and degraded reliability
- Source anchors: [S17] [S18]

### R58 - Treat operator attention as a scarce resource and design around it
- Applies to: solo operator, feedback-heavy, external-constraint, release-safety, agentic
- Required artifacts: attention bottleneck note, automation strategy, review trigger
- Why it matters: in solo operator projects the real critical path is often what the operator must still inspect or approve manually.
- Failure prevented: hidden review bottlenecks
- Source anchors: [S13] [S14] [S16]

### R58A - Pilot large automated changes on a narrow slice before scaling out
- Applies to: agentic, solo operator
- Required artifacts: pilot slice, scale-out trigger, stop trigger, refinement note
- Why it matters: large unattended changes multiply prompt mistakes, environment gaps, and policy omissions.
- Failure prevented: repo-wide low-quality churn and hard-to-undo mass edits
- Source anchors: [S22]

## Appendix A - Artifact Checklist

| Artifact | Purpose |
| --- | --- |
| Objective and success criteria | Defines what valuable completion means |
| Operator decision record | Preserves choices and unresolved decisions |
| Source-of-truth index | Keeps project state discoverable |
| Scope and exclusions | Prevents silent scope creep |
| Work breakdown or backlog | Decomposes total work |
| Task queue or execution queue with stable IDs | Defines the next small executable units and keeps them traceable through renames |
| Dependency map or sequence | Makes blockers visible |
| Current-state note or execution plan | Preserves continuity across sessions |
| Risk register | Tracks threats and mitigations |
| Issue log | Tracks active problems |
| Change log | Governs scope and plan changes |
| Acceptance criteria / DoD | Defines completion quality |
| Test strategy and evidence | Verifies quality |
| Architecture and design records | Preserves technical intent |
| Environment and data setup docs | Enables reproducible execution |
| User testing or research notes | Improves quality or value when relevant |
| Release checklist and rollback note | Enables safe deployment when shipping |
| Eval suite | Regresses agent behavior when prompts or workflows change |
| Guardrail and permission rules | Prevents unsafe actions |

## Appendix B - Control-Mode Mapping

| Mode | When to use it | What to add |
| --- | --- | --- |
| Solo operator default | One operator runs the project through Claude Code with no hard outside gate | Scope, decomposition, small task queue with stable IDs, dependencies, acceptance, durable files, tests or evals, guardrails |
| Feedback-heavy | User learning or UX uncertainty dominates | Research questions, findings log, scope-refresh loop |
| External-constraint | Fixed date, approval gate, vendor dependency, quota cap, or launch window exists | Constraint log, minimal critical path, explicit gate evidence, fallback assumptions |
| Release-safety | Real software will be deployed or handed to users | Release checklist, rollback plan, monitoring checks, operating notes |
| Agentic | Claude Code agents or subagents perform substantial execution | CLAUDE.md entry-point rules, task-state files, agent routing, evals, trust boundaries |

## Appendix C - Question Coverage Map

| Original question | Primary rule coverage |
| --- | --- |
| Prerequisites for a software project | R05-R08 |
| Stages of a software project | R12, R25-R27, R42-R43 |
| How to plan the work | R04A, R17, R19-R24 |
| How to map dependencies | R20 |
| How to hand off work and artifacts | R26-R27, R54 |
| How to map a critical path | R21 |
| How to plan resources | R08, R23, R58 |
| How to budget time and cost | R21-R24 |
| How to scope work | R16-R18 |
| How to prepare the documentation | R03, R40-R41 |
| What documentation the project needs | Appendix A, R40-R41 |
| How to control progress | R28-R32 |
| How to estimate risks | R06, R29-R30 |
| How to mitigate risks | R29-R32 |
| How to control quality | R33-R36, R34A, R47A |
| How to address scope changes | R32 |
| What processes ensure project success | R01-R15, R28-R32, R47-R47A |
| How to include learning loops for process improvement | R31, R39, R43, R51 |
| How to include feedback loops to refine scope | R31-R32, R38-R39 |
| How to include user testing to improve quality | R37 |
| How to include user testing to improve value | R38 |
| How and when to include agile practices | R11, R31, R39 |
| How to run living project documentation | R40-R41 |
| How to use files to improve success probability | R03, R40, R44-R46 |
| How to store tasks outside context windows | R44-R45 |
| How to ensure interoperability across sessions | R26, R44, R54-R55 |
| How to route work efficiently | R48, R57 |
| How to include tests in tasks | R18, R33-R35, R34A, R47, R52 |
| How to include learning loops in agent work | R51-R52, R57-R58 |
| How to help agents understand codebases | R45-R46, R53 |
| How to manage context windows | R03, R40, R44-R46, R49 |
| How and when to use subagents | R49 |
| How to prepare work for autonomous agents | R44-R50 |
| How to optimize processes | R31, R51-R53A, R58-R58A |
| How to set guardrails | R50, R53-R55, R53A |
| What else was missed | R06, R12, R35-R36, R42-R43, R56-R58 |
| Latest AI coding-space good practices | R48-R58A |
