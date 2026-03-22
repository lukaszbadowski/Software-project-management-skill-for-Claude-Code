# External Constraints Notes

This file is a narrow addendum for projects run by a single human operator that still face real outside constraints. Read it only when the work has a fixed date, approval gate, vendor dependency, quota cap, launch window, or production release risk. Source anchors refer to [source-anchors.md](./source-anchors.md).

## Table of Contents
- Purpose and Use
- Fixed Dates and Launch Windows
- Approval and Compliance Gates
- Vendor and API Dependencies
- Spend and Quota Caps
- Production Release Safety
- Minimal Artifact Set

## Purpose and Use
- Do not import full project ceremony into a solo operator project just because one external constraint exists.
- Add only the controls needed to manage the actual constraint: sequence, evidence, fallback, and decision points. [S04] [S05] [S08]

## Fixed Dates and Launch Windows
- Convert a real date into sequence logic, not vague urgency.
- Identify the small set of tasks that truly determine date risk.
- Track assumptions that could change the date: approvals, environment access, vendor responses, data arrival, or release readiness.
- Recompute the sequence whenever those assumptions move. [S05] [S08] [S12]

## Approval and Compliance Gates
- List each required approval or evidence package explicitly.
- Record who or what grants the approval, what proof is needed, typical lead time, and what happens if the first attempt fails.
- Treat compliance and security evidence as deliverables, not side paperwork. [S04] [S05] [S10]

## Vendor and API Dependencies
- Record every external dependency with expected response time, quota or contract limits, failure modes, and fallback options.
- Test integration assumptions early when a vendor or API can block the schedule.
- Keep a local substitute or degraded-mode plan when feasible. [S04] [S08]

## Spend and Quota Caps
- Budget only when money, credits, or request quotas are real constraints.
- Track burn against the limit and define the trigger for switching to a lighter agent type, lower-frequency run, or narrower scope. [S04] [S13] [S16]

## Production Release Safety
- When software will be deployed, add cutover, rollback, monitoring, and operator run notes before calling the project done.
- Define what to watch after release, what signals require rollback, and which manual steps must remain under explicit operator control. [S04] [S12] [S16]

## Minimal Artifact Set
- constraint log
- dependency sequence with the blocking items highlighted
- approval or evidence checklist when applicable
- quota or spend tracker when applicable
- release checklist and rollback note when applicable
- changed assumptions log
