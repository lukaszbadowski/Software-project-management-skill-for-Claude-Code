# Source Log

Access date for all entries: `2026-03-22`

This log records the primary sources used to build the `software-project-management-for-claude` skill. Source IDs are referenced from the bundled note files and the master rulebook.

## Table of Contents
- Solo Operator and Constraint Guidance
- AI-Agent Operating Practice
- Source Prioritization Rule

## Solo Operator and Constraint Guidance

### S01 - Agile Manifesto
- Type: Official framework source
- URL: <https://agilemanifesto.org/>
- Why trusted: Primary source from the original Agile Manifesto authors.
- Questions answered: Agile principles, mindset, value system, why iterative delivery and change-friendly practices matter.
- Notes on paywall or uncertainty: Public and stable. High-level values, not a full operating model.

### S02 - Principles Behind the Agile Manifesto
- Type: Official framework source
- URL: <https://agilemanifesto.org/principles.html>
- Why trusted: Primary source for the twelve agile principles.
- Questions answered: Feedback loops, changing scope, continuous delivery, sustainable pace, continuous improvement.
- Notes on paywall or uncertainty: Public and stable. Principles require interpretation for specific delivery systems.

### S03 - Scrum Guide 2020
- Type: Official framework guide
- URL: <https://scrumguides.org/docs/scrumguide/v2020/2020-Scrum-Guide-US.pdf>
- Why trusted: Official definition of Scrum by Ken Schwaber and Jeff Sutherland.
- Questions answered: Empiricism, backlog management, inspection, adaptation, and practical feedback-loop structure.
- Notes on paywall or uncertainty: Public PDF. Team-role content is not imported directly into the solo-operator skill.

### S04 - PMI PMBOK Guide
- Type: Official standard overview
- URL: <https://www.pmi.org/standards/pmbok>
- Why trusted: PMI's current flagship standard overview.
- Questions answered: Value delivery, tailoring, scope, schedule, finance, procurement, risk, and release-related constraints.
- Notes on paywall or uncertainty: Overview is public; the full guide is member-gated or purchasable. Use as a canonical anchor, not a sole source of procedural detail.

### S05 - PMI Process Groups: A Practice Guide
- Type: Official practice guide overview
- URL: <https://www.pmi.org/standards/process-groups>
- Why trusted: Current PMI process-based guide for predictive delivery.
- Questions answered: Initiating, planning, executing, monitoring and controlling, closing; minimal predictive controls for real external commitments.
- Notes on paywall or uncertainty: Public overview, full guide gated.

### S06 - PMI Agile Practice Guide
- Type: Official practice guide overview
- URL: <https://www.pmi.org/standards/agile>
- Why trusted: PMI guide developed with Agile Alliance.
- Questions answered: Life-cycle selection, tailoring agile approaches, empirical measures, and hybrid framing.
- Notes on paywall or uncertainty: Public overview, full guide gated.

### S07 - PMI Work Breakdown Structures - Third Edition
- Type: Official standard overview
- URL: <https://www.pmi.org/standards/work-breakdown-structures-third-edition>
- Why trusted: PMI's standard on decomposition and scope structuring.
- Questions answered: Scoping, decomposition, schedule/resource/risk linkage, cross-lifecycle applicability.
- Notes on paywall or uncertainty: Public overview, full guide gated.

### S08 - PMI Practice Standard for Scheduling - Third Edition
- Type: Official practice guide overview
- URL: <https://www.pmi.org/standards/scheduling-third-edition>
- Why trusted: PMI's scheduling practice standard.
- Questions answered: Schedule models, critical path, rolling-wave planning, Monte Carlo, adaptive scheduling.
- Notes on paywall or uncertainty: Public overview, full guide gated.

### S09 - PMI Requirements Management: A Practice Guide
- Type: Official practice guide overview
- URL: <https://www.pmi.org/standards/requirements-management>
- Why trusted: PMI's dedicated requirements guide.
- Questions answered: Requirements development, requirements management, acceptance framing, benefits and outcomes linkage.
- Notes on paywall or uncertainty: Public overview, full guide gated.

### S10 - PMI Risk Management in Portfolios, Programs, and Projects
- Type: Official practice guide overview
- URL: <https://www.pmi.org/standards/risk-management-in-portfolios>
- Why trusted: Current PMI practice guide focused on risk management principles and lifecycle.
- Questions answered: Risk identification, analysis, mitigation, opportunity capture, ongoing risk management.
- Notes on paywall or uncertainty: Public overview, full guide gated.

### S11 - GOV.UK Service Manual: User Research
- Type: Official government delivery guidance
- URL: <https://www.gov.uk/service-manual/user-research>
- Why trusted: Mature public-sector delivery guidance based on repeated service-delivery practice.
- Questions answered: Planning user research, research cadence by phase, usability testing, continuous discovery, sharing findings.
- Notes on paywall or uncertainty: Public. Written for digital services but broadly applicable to software delivery.

### S12 - GOV.UK Service Manual: Agile Delivery
- Type: Official government delivery guidance
- URL: <https://www.gov.uk/service-manual/agile-delivery>
- Why trusted: Mature public-sector agile delivery guidance with governance, progress reporting, and phased delivery detail.
- Questions answered: Agile planning, progress reporting, roadmap use, phased delivery, and practical adaptation.
- Notes on paywall or uncertainty: Public. Strong on service delivery and progress control, lighter on engineering detail.

### S13 - DORA State of AI-assisted Software Development 2025
- Type: Official research report overview
- URL: <https://dora.dev/research/2025/dora-report/>
- Why trusted: Research program run by Google Cloud's DORA team.
- Questions answered: How AI affects delivery systems, organizational amplifiers, why tooling alone is insufficient, latest good practices in AI-assisted delivery.
- Notes on paywall or uncertainty: Report download is public. Findings are research-backed but still require local validation.

### S14 - DORA AI Capabilities Model 2025
- Type: Official research companion guide
- URL: <https://dora.dev/ai/capabilities-model/report/>
- Why trusted: Companion guide to DORA's 2025 report with implementation-oriented capability framing.
- Questions answered: Continuous improvement capabilities, monitoring progress, and delivery-system prerequisites for AI-assisted delivery.
- Notes on paywall or uncertainty: Public overview and report download.

## AI-Agent Operating Practice

### S15 - Anthropic Claude Code Best Practices
- Type: Official product docs
- URL: <https://docs.anthropic.com/en/docs/claude-code/best-practices>
- Why trusted: Official Anthropic guidance on effective Claude Code usage patterns.
- Questions answered: How to structure work for Claude Code, task sizing, file-backed state, prompt design, effective workflows.
- Notes on paywall or uncertainty: Public docs. Practices evolve as the product matures.

### S16 - Anthropic Claude Code CLAUDE.md and Project Setup
- Type: Official product docs
- URL: <https://docs.anthropic.com/en/docs/claude-code/claude-md>
- Why trusted: Official guidance on project configuration, memory, and rule loading.
- Questions answered: Persistent file-backed memory, keeping index files short, path-scoped rules, managing durable context, CLAUDE.md structure and conventions.
- Notes on paywall or uncertainty: Public docs. The file-backed-memory pattern is product-specific but the principle generalizes.

### S17 - Anthropic Claude Model Cards
- Type: Official model reference
- URL: <https://docs.anthropic.com/en/docs/about-claude/models>
- Why trusted: Current official model reference for Claude model family.
- Questions answered: Model capabilities, task-model fit, cost/latency tradeoffs, model selection for different task types (Opus for complex reasoning, Sonnet for balanced performance, Haiku for speed).
- Notes on paywall or uncertainty: Public. Specific model rankings change over time.

### S18 - Anthropic Prompt Caching
- Type: Official API docs
- URL: <https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching>
- Why trusted: Official Anthropic guidance on cache behavior and prompt structure for cost and latency control.
- Questions answered: Token saving, prompt structure, stable-prefix design, cost-aware model usage.
- Notes on paywall or uncertainty: Public docs. Applies to API behavior.

### S19 - Anthropic Claude Code Memory Docs
- Type: Official product docs
- URL: <https://docs.anthropic.com/en/docs/claude-code/memory>
- Why trusted: Official guidance on project memory and rule loading.
- Questions answered: Persistent file-backed memory, keeping index files short, path-scoped rules, managing durable context.
- Notes on paywall or uncertainty: Public docs for Claude Code specifically, but the file-backed-memory pattern generalizes.

### S20 - Anthropic Claude Code Sub-agents Docs
- Type: Official product docs
- URL: <https://docs.anthropic.com/en/docs/claude-code/sub-agents>
- Why trusted: Official docs on scoped delegation and context isolation.
- Questions answered: When to use subagents, isolating high-volume output, fresh context, tool scoping, agent types (Explore, Plan, general-purpose), foreground vs background execution, worktree isolation.
- Notes on paywall or uncertainty: Public docs. Feature names are product-specific, but the operating pattern generalizes.

### S21 - Anthropic Claude Code Hooks Docs
- Type: Official product docs
- URL: <https://docs.anthropic.com/en/docs/claude-code/hooks>
- Why trusted: Official docs on guardrails and permission mediation.
- Questions answered: Permission interception, policy hooks, allow/deny flows, tool restrictions, runtime guardrails, pre- and post-tool-use events.
- Notes on paywall or uncertainty: Public docs. Implementation is product-specific; the least-privilege principle is general.

## Source Prioritization Rule
- Official framework owners and official vendor docs were used first.
- Primary research and benchmark owners were used second.
- Secondary sources were used only to find primary material, not as the basis for claims in the research pack.
