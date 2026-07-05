# Software Project Management for Claude Code

Structure software projects run by a single human operator using Claude Code.

This skill helps turn vague "just build it" work into a controlled delivery system with clear scope, small executable tasks, durable files, acceptance criteria, dependency sequencing, tests or evals, and guardrails. It is designed for people shipping real software with AI help, not for teams looking to recreate heavyweight enterprise PM inside a prompt.

## What You Can Achieve With This Skill

Use this skill to help Claude Code:

- co-create the project breakdown with the operator through explicit approval checkpoints (frame, breakdown, queue, final acceptance) instead of assuming a plan on their behalf
- rescue a drifting project that has become hard to resume or review
- turn a rough idea into a file-backed execution system with a fixed, four-file `pm/` layout
- break approved stories into small reviewable tasks with stable task IDs
- route each task to the cheapest model tier that can do it reliably, keeping capable models for planning, review, and orchestration
- keep the main thread in a director role that delegates bounded work and reviews evidence
- make progress survive context resets, interrupted sessions, and switches between Claude Code and Codex
- trace every success criterion to stories, tasks, and evidence, and close only after end-to-end re-verification
- add tests, evals, risks, and change control without over-managing the project
- handle real-world constraints like deadlines, approvals, vendor dependencies, quotas, and release risk only when they actually exist

Typical outcomes include:

- `pm/PLAN.md`, `pm/TASKS.md`, `pm/STATE.md`, `pm/DECISIONS.md` — the durable control surface of the project
- an operator-approved story breakdown traced to success criteria
- an ordered, model-routed task queue with stable task IDs and clear "done when" checks
- a current-state note that makes handoffs and resumption easy
- a final acceptance report proving each success criterion end-to-end
- release or rollback notes when software is actually going to ship

## Who This Is For

This skill is for:

- solo founders and indie hackers using Claude Code as a serious delivery tool
- engineers steering multiple agent runs or subagents
- operators rescuing messy AI-assisted software projects
- people who want the lightest effective process, but still need reliability

It is especially useful when the bottleneck is no longer coding speed, but coordination, continuity, verification, and operator attention.

## Core Idea

Most AI-assisted software projects do not fail because the model cannot write code. They fail because the work has weak scope, oversized tasks, missing acceptance criteria, hidden dependencies, stale docs, or no durable memory outside chat.

This skill gives Claude Code a practical control model:

1. Inspect the workspace before inventing process.
2. Elicit the real objective, constraints, and success bar from the operator at Checkpoint CP1.
3. Get conscious operator approval of the story breakdown (CP2) and task queue (CP3) before executing.
4. Execute through small bounded tasks in the four `pm/` files, routed to the cheapest reliable model tier.
5. Close only at Checkpoint CP4, when every success criterion is re-verified end-to-end with evidence.
6. Add stronger controls only when the project has a real reason for them.

The default stance is simple:

- keep the main thread on a capable model, focused on direction, synthesis, and sign-off
- delegate autonomy-ready work to the cheapest tier that can do it reliably
- require delegated work to return evidence, not just conclusions
- use the lightest control system that still keeps the project resumable, reviewable, and safe
- keep durable state in vendor-neutral files, not only in conversation history
- prefer task queues over milestone-only plans
- assumptions may fill details inside an approved frame; structure changes go back through a checkpoint
- use dates, budgets, approvals, and release controls only when they are real constraints

## How The Skill Works

This repository follows a progressive disclosure model:

### 1. Metadata triggers the skill

The `name` and `description` in [`SKILL.md`](./SKILL.md) tell Claude Code when this skill should be used.

### 2. `SKILL.md` provides the operating workflow

The main skill file gives Claude Code:

- the control philosophy
- the quick-start workflow
- the core artifact set
- task sizing and sequencing rules
- output standards
- guidance on when to load deeper references

### 3. Reference files add depth only when needed

The bundled references let Claude Code stay lean by default and pull in detail only when the task requires it:

- [`references/file-templates.md`](./references/file-templates.md): the canonical `pm/` layout and templates — the cross-tool file contract
- [`references/worked-example.md`](./references/worked-example.md): one compressed end-to-end example of checkpoints, routing, and acceptance
- [`references/project-rulebook.md`](./references/project-rulebook.md): the audit and rescue rule system
- [`references/external-constraints.md`](./references/external-constraints.md): deadlines, approvals, quotas, vendor dependencies, release safety
- [`references/ai-agent-practices.md`](./references/ai-agent-practices.md): file-backed memory, handoffs, routing, evals, subagents, guardrails
- [`references/source-anchors.md`](./references/source-anchors.md): provenance and source tracking for the rule set

This gives you a full operating system for software delivery without forcing Claude Code to load the whole thing for every request.

### 4. The `pm/` files are the cross-tool contract

The project artifacts this skill maintains are deliberately vendor-neutral. A sibling edition of this skill exists for Codex (`software-project-management`); both editions read and write the same `pm/` layout, ID scheme, and routing tiers, so an operator can switch tools mid-project without conversion. Only the tier-to-model mapping differs per edition, and tasks record tiers, never model names.

## What Makes This Skill Different

Many project-management prompts either:

- stay too vague to survive real execution, or
- import too much ceremony for solo operator work

This skill is built around a different balance:

- strong enough for real delivery
- small enough for everyday use
- explicit enough for cross-session handoffs
- flexible enough to stay out of the way when the project is simple

It treats software project management as a control system for AI-assisted execution, not as a pile of rituals.

## What This Skill Will Not Do

This skill is deliberately opinionated about its boundaries.

- It will not act as your software architect. It can help structure architecture work, decisions, and trade-offs, but it does not replace technical design judgment.
- It will not act as a security enforcer or compliance authority. It can surface risks, checks, and approval points, but it does not certify a system as secure, compliant, or production-safe by itself.
- It will not invent product strategy, business goals, or success criteria out of thin air. The operator still owns the objective and the trade-offs.
- It will not replace tests, evals, code review, or human verification. It pushes toward explicit checks, but it does not guarantee correctness.
- It will not add heavyweight ceremony by default. It does not force stage gates, budget tracking, approval workflows, or deadline mechanics unless those constraints are actually real.

## Repository Layout

```text
software-project-management-for-claude/
├── SKILL.md
├── README.md
└── references/
    ├── ai-agent-practices.md
    ├── external-constraints.md
    ├── file-templates.md
    ├── project-rulebook.md
    ├── source-anchors.md
    └── worked-example.md
```

## Installation

Copy or clone this repository into a location accessible to your Claude Code setup. The skill can be used by referencing it from a CLAUDE.md file or by installing it as a Claude Code skill.

To make the skill available project-wide, reference it from your project's CLAUDE.md:

```markdown
When managing this project, follow the rules in /path/to/software-project-management-for-claude/SKILL.md
```

Or install it as a skill in your Claude Code skills directory:

```text
~/.claude/skills/software-project-management-for-claude
```

Once installed, Claude Code can use the skill when the request matches the skill description.

## Example Prompts

- `Use software-project-management to rescue this drifting MVP project and rebuild the task queue.`
- `Use software-project-management to run the CP1 elicitation and set up the pm/ files for this idea.`
- `Use software-project-management to break this feature roadmap into stories and routed tasks with acceptance checks.`
- `Use software-project-management to run final acceptance and verify every success criterion end-to-end.`
- `Use software-project-management to prepare a safe release plan with rollback notes and monitoring checks.`
- `Use software-project-management to set up multi-agent delivery rules, model routing, evals, and guardrails for this codebase.`

## Design Principles

- Default to solo-operator control, not team ceremony.
- The operator consciously approves the frame, the breakdown, the queue, and the final acceptance.
- Prefer reviewable tasks over heroic long runs.
- Keep the parent thread as a director on a capable model; route execution to the cheapest reliable tier.
- Keep project truth in vendor-neutral files that both skill editions can read and write.
- Trace success criteria to stories, tasks, and evidence; done means re-verified end-to-end.
- Separate stable delivery practices from volatile vendor advice.
- Add complexity only when an actual constraint justifies it.

## Sources And Trust Model

The skill combines stable software-delivery guidance with recent AI-agent operating practice. The source log intentionally separates long-lived control rules from more volatile model and vendor patterns, so the skill can stay useful even as tooling changes.

That means the skill is opinionated, but not trendy for its own sake. It tries to preserve what actually helps a solo operator keep control while using Claude Code.
