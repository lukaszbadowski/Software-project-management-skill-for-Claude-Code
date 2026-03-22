# AI-Agent Operating Practice Notes

This document synthesizes recent practices for running software delivery with Claude Code when one human operator is steering the work. It is intentionally separate from the rulebook so the skill can keep stable project controls distinct from newer agent-specific operating methods. Source anchors refer to [source-anchors.md](./source-anchors.md).

## Table of Contents
- Purpose and Use
- Core Operating Model
- Files as Durable Memory
- Task Storage Outside the Context Window
- Task Granularity and Stop Points
- Helping Agents Understand a Codebase
- Interoperability Across Sessions
- Routing Work Efficiently
- Including Tests and Evals in Tasks
- Learning Loops
- Managing Context Windows
- How and When to Use Subagents
- Preparing Work for Autonomous Agent Execution
- Process Optimization
- Guardrails
- Recent Shifts
- Unknown Unknowns to Watch
- Working Synthesis

## Purpose and Use
- Treat agentic delivery as an extension of software project management, not a replacement for it.
- The stable question is still: how do we create predictable, high-quality outcomes under constraints?
- In solo operator projects, the default controls are scope, acceptance, dependency sequencing, durable files, evals, and permissions. Dates, budgets, approvals, or launch windows are secondary unless they are explicit external constraints.
- What changes is where the bottleneck moves. In agent-assisted systems, operator attention, environment design, file-backed memory, and validation loops become the primary leverage points. [S13] [S14] [S15] [S16]

## Core Operating Model
- A recent DORA finding is the most important managerial caveat: AI amplifies the surrounding delivery system rather than rescuing a weak one. [S13] [S14]
- Therefore the right operating model is:
  - the operator sets goals, constraints, and acceptance conditions
  - Claude Code agents perform bounded analysis and execution
  - files, tests, and tools hold the durable state
  - evals and guardrails keep behavior inside acceptable bounds

## Files as Durable Memory
- The repository should be treated as the system of record for what the agent can actually know.
- Practical file categories that improve success probability:
  - short entry-point instructions (CLAUDE.md, project-scoped CLAUDE.md files)
  - architecture maps
  - execution plans
  - specs and acceptance criteria
  - runbooks and environment setup
  - generated references where the codebase is too large to rediscover repeatedly
  - decision logs
  - risk and debt trackers
- Short entry points beat giant instruction manuals. Anthropic recommends a concise CLAUDE.md with more detailed topic files behind it. Large memory files reduce adherence. [S19]
- Claude Code also has a persistent file-based memory system in `~/.claude/projects/`. Use it for cross-session user preferences and project context, but keep execution state in repo files for portability. [S19]

## Task Storage Outside the Context Window
- Long-horizon tasks should have an explicit plan file, not only a chat history.
- A good task file contains:
  - task ID
  - problem statement
  - assumptions
  - constraints and non-goals
  - acceptance criteria
  - current progress
  - evidence and commands run
  - decision log
  - surprises or discoveries
  - next actions
- This reduces context-window dependence and makes cross-session continuation possible. [S15] [S19]

## Task Granularity and Stop Points
- Use milestones, themes, or checkpoints to group work, not as the next execution unit.
- Prefer tasks that can usually finish in one focused run and produce one reviewable diff or artifact.
- A good execution task names:
  - task ID
  - one primary outcome
  - exact files or modules in scope
  - dependencies or prerequisites
  - acceptance command or check
  - explicit stop point
- Keep task IDs stable across title edits and scope clarifications.
- If a task splits, keep the original task ID in history and assign new IDs to the child tasks instead of recycling names.
- Split a task before execution if it:
  - spans multiple subsystems
  - requires several independent validations
  - produces a large opaque diff
  - would leave the operator unsure what changed
- After each task, update the task file or current-state note and pick the next task from the queue. [S15] [S16] [S19] [S20]

## Helping Agents Understand a Codebase
- Agent comprehension improves when the codebase is legible:
  - stable directory layout
  - architecture docs
  - explicit domain boundaries
  - generated schema references
  - reproducible commands for build, test, lint, and run
  - searchable design and product notes in-repo
- What the agent cannot discover in-context effectively does not exist.
- This implies a strong bias toward:
  - repository-local knowledge
  - boring and inspectable technology choices
  - mechanical invariants
  - reduced reliance on tribal knowledge
- CLAUDE.md files at different directory levels can provide scoped context for different parts of the codebase. [S16] [S19]

## Interoperability Across Sessions
- Interoperability is primarily an artifact-design problem.
- Different sessions work better when the handoff is:
  - plain-text Markdown
  - explicit about required outputs
  - explicit about assumptions and unresolved questions
  - explicit about commands and evidence
  - free of hidden context
- Shared handoff artifacts should also define trust boundaries:
  - which inputs are authoritative
  - which inputs may be stale or user-supplied
  - where secrets must not be copied
  - what requires operator approval
- Keep the durable state in repo files, not only in Claude Code's conversation memory. Conversation memory is useful for preferences, but execution state belongs in portable files. [S15] [S16] [S19]
- Prefer explicit interfaces:
  - task brief
  - acceptance criteria
  - file paths
  - schema or API contracts
  - test commands
  - escalation rules
- A reliable cross-session handoff template should also include:
  - current task ID
  - current state and what changed
  - commands already run and results
  - unresolved questions
  - exact files to inspect next
  - whether the next session should edit, only review, or only research

## Routing Work Efficiently
- Route by task shape, not by habit.
- Use lighter agent types for:
  - repo search and localization (Explore subagent type)
  - short summaries
  - mechanical transformations
  - narrow documentation edits
  - first-pass triage
- Use the main Claude Code session for:
  - ambiguous debugging
  - architecture changes
  - cross-cutting refactors
  - long-horizon execution
  - unresolved tradeoffs
- Claude Code supports model selection per agent (sonnet, opus, haiku) via the Agent tool. Route subagents to the lightest model that can handle the task. [S17] [S18]
- Revalidate routing whenever task mix or cost constraints change. [S17] [S18]

## Including Tests and Evals in Tasks
- Every nontrivial task should define how correctness will be checked before the agent starts.
- Minimum task-ready test package:
  - acceptance criteria
  - exact commands to run
  - expected success condition
  - expected failure modes or regressions to avoid
- Evals are especially relevant when:
  - prompts change
  - tools change
  - hook configurations change
  - CLAUDE.md rules change
- Evals are the behavioral regression suite for the agent workflow itself. [S13] [S14]

## Learning Loops
- There are three learning loops in an agentic system:
  - task loop: fix the specific issue
  - process loop: update prompts, docs, rules, or tools
  - system loop: revise the environment so the next run is easier and safer
- Failures should be framed as missing capability or missing legibility in the environment rather than "the model should just try harder".
- DORA's AI capability framing reinforces the same point: improvement comes from strengthening the system around the tool. [S13] [S14]

## Managing Context Windows
- Keep the startup context small and stable.
- Push detailed, rarely needed information into deeper files.
- Use progressive disclosure:
  - concise CLAUDE.md entry-point file
  - linked topical references
  - generated references or searchable files
  - task-local plans
- Claude Code automatically compresses prior messages as context limits approach. This helps but does not remove the need for external durable state. The reliable pattern is still "files first, prompt second". [S15] [S16] [S19]

## How and When to Use Subagents
- Use subagents when:
  - a task produces a lot of output
  - work can happen in parallel
  - a subtask is well-scoped and bounded
  - the main thread should preserve context for synthesis
- Claude Code's Agent tool supports specialized subagent types:
  - `Explore`: fast codebase exploration, file search, keyword search
  - `Plan`: architecture and implementation planning
  - `general-purpose`: multi-step research and execution
- Subagents can run in isolated worktrees for parallel work that touches files.
- Subagents can run in foreground (when results are needed before proceeding) or background (for independent parallel work). [S20]
- Practical uses:
  - repository exploration
  - documentation gathering
  - log analysis
  - independent review passes
  - specialized task slices with separate scope
- Do not use subagents for vague "go think about everything" delegation. Give one job, clear outputs, and minimal required tools.

## Preparing Work for Autonomous Agent Execution
- A task is autonomy-ready when it includes:
  - task ID
  - goal and user or business outcome
  - constraints and non-goals
  - files or modules in scope
  - acceptance tests
  - environment commands
  - explicit stop condition
  - escalation conditions
  - guardrails for risky actions
- If any of those are missing, the agent will substitute guesses. That may be acceptable for low-risk tasks but becomes dangerous for large or cross-cutting work. [S15] [S16]

## Process Optimization
- High-leverage improvements include:
  - worktrees for parallel agent runs (via Agent tool's `isolation: "worktree"`)
  - agent-readable observability
  - structural linting and architecture tests
  - recurring documentation freshness checks
  - mechanical enforcement of naming, boundaries, and safety rules
  - targeted review checkpoints where throughput matters
  - Claude Code hooks for automated pre/post-action checks
- The general pattern is to encode taste and policy into tools and files so the operator does not have to restate them every run. [S16] [S21]

## Guardrails
- Good guardrails combine:
  - Claude Code's permission modes (allowedTools, blockedTools)
  - hooks with allow/deny rules for specific tool calls
  - path-scoped rules via directory-level CLAUDE.md files
  - destructive-command restrictions (git push, rm, etc.)
  - secret-handling rules
  - trust-boundary rules for untrusted inputs and external content
  - tests and structural checks
  - mandatory escalation for ambiguous high-risk actions
- Claude Code's hooks system makes the enforcement model concrete with pre- and post-tool-use events and configurable allow/deny flows. [S21]
- Guardrails should prevent silent damage without freezing useful work. They work best when paired with good task specs and strong validation.
- Guardrails should also define trust boundaries for:
  - secrets and credentials
  - production systems
  - external content that may contain prompt injection or malicious instructions
  - generated artifacts that require operator signoff before execution or release
- In practice this means the agent should not treat fetched text, issue content, or generated code as automatically trustworthy input for privileged actions. [S16] [S21]

## Recent Shifts
- AI-assisted delivery has become more obviously multi-agent and long-horizon. [S16] [S20]
- Prompt and workflow changes now require formal regression discipline; "it seemed fine last week" is not enough. [S13] [S14]
- Practical AI delivery guidance is shifting from "prompt tricks" toward environment design, evaluation, and delivery-system capability. [S13] [S14] [S16]

## Unknown Unknowns to Watch
- Hidden business context that never makes it into the repo
- Stale docs that agents treat as truth
- Environment-specific failures that benchmarks do not capture
- Test suites that reject correct solutions or miss important regressions
- Cost runaway from overusing heavyweight models or agents
- Tool over-permissioning
- Attention bottlenecks where operator review becomes the true critical path
- Local success that does not generalize because the environment was unusually favorable

## Working Synthesis
- Stable PM controls still matter: scope, operator decisions, quality, risk, change control, and learning loops.
- Agentic delivery adds a new layer: design files, tools, prompts, policies, and evaluation harnesses so the system can act reliably even when the chat context is small or changing.
- The most important implementation principle is: make the work legible, testable, and controllable outside the model's transient context. [S13] [S14] [S15] [S16] [S19] [S20] [S21]
