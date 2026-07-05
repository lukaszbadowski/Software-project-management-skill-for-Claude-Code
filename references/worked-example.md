# Worked Example: From Idea to Verified Delivery

A compressed end-to-end example of the skill applied to a small real project. It shows the operator checkpoints, the `pm/` files, tiered routing, and final acceptance. Formats follow [file-templates.md](./file-templates.md). This file is identical across the Claude Code and Codex editions of the skill.

The operator's opening request: *"Build me a reading-list web app. I want to save links with notes and find them later. Just build it."*

## Checkpoint CP1 — Frame

The skill does not start building. It asks the elicitation questions and gets:

- Outcome: operator saves links with notes, tags them, and finds them later by tag or text search. Single user, local only.
- Personal test: "I add 5 links, close the browser, reopen, search 'rust', and my Rust articles show up."
- Out of scope: accounts, sharing, mobile app, browser extension.
- Constraints: Python backend preferred; SQLite; no cloud services.
- Existing material: none, fresh repo.
- Riskiest part: operator unsure whether search should match notes too — flagged as an open decision, not assumed.
- Review appetite: approve checkpoints and story completions; individual tasks may proceed unreviewed.

Resulting `pm/PLAN.md` frame (excerpt):

```markdown
## Objective
A local single-user web app where the operator saves links with notes and tags,
and reliably finds them later by tag or text search.

## Success Criteria
| ID | Criterion | Final check | Status |
| --- | --- | --- | --- |
| SC-1 | Links with note and tags can be saved and persist across restarts | Add 5 links, restart server and browser, all 5 present | pending |
| SC-2 | Search by tag or text finds the right links | Search "rust" returns exactly the Rust-tagged/titled items | pending |
| SC-3 | App runs locally with one command | `make run` starts app on localhost | pending |

### Out of scope
- Accounts, sharing, mobile, browser extension.

**CP1 — frame: approved by operator on 2026-07-05**
```

## Checkpoint CP2 — Breakdown

Stories in the operator's language, each traced to success criteria:

```markdown
### ST-1: Save a link with note and tags
- Serves: SC-1
- Acceptance:
  - [ ] Submitting the form stores link, note, tags in SQLite
  - [ ] Data survives server restart
- Status: approved

### ST-2: Browse and search saved links
- Serves: SC-2
- Acceptance:
  - [ ] List view shows newest first
  - [ ] Search matches title, tags, and notes (D-1)
- Status: approved

### ST-3: One-command local run
- Serves: SC-3
- Acceptance:
  - [ ] `make run` serves the app; README states the URL
- Status: approved

## Traceability
| Success criterion | Covered by stories |
| --- | --- |
| SC-1 | ST-1 |
| SC-2 | ST-2 |
| SC-3 | ST-3 |
```

The open decision was resolved at the checkpoint, not silently: `D-1 (2026-07-05): search matches notes too. Why: operator writes context in notes. By: operator.`

## Checkpoint CP3 — Queue

The heavy tier plans the queue; execution is routed down to cheaper tiers:

```markdown
### T-001: Scaffold app, SQLite schema, and make run target
- Story: ST-3
- Route: standard
- Scope: app/, Makefile, README.md
- Depends on: -
- Done when: `make run` serves an empty list page on localhost
- Verify with: `make run` + curl localhost:8000 returns 200
- Stop after: scaffold only, no features
- Status: todo

### T-002: Save-link form and persistence
- Story: ST-1
- Route: standard
- Scope: app/routes.py, app/models.py, app/templates/
- Depends on: T-001
- Done when: posted link+note+tags row visible in DB and list view
- Verify with: pytest tests/test_save.py; manual add + restart + reload
- Stop after: saving only, no search
- Status: todo

### T-003: Search across title, tags, notes
- Story: ST-2
- Route: standard
- Depends on: T-002
- Verify with: pytest tests/test_search.py (incl. "rust" fixture case)
- Status: todo

### T-004: Write README usage section
- Story: ST-3
- Route: light
- Depends on: T-001
- Verify with: commands in README copy-paste-run clean
- Status: todo

### T-005: Fresh-context review of persistence and search
- Story: ST-1, ST-2
- Route: heavy
- Depends on: T-002, T-003
- Done when: review findings recorded and resolved or logged as issues
- Status: todo

**CP3 — queue: approved by operator on 2026-07-05**
```

Routing rationale: scaffolding and CRUD are `standard`; the README edit is mechanical, so `light`; the independent review is `heavy` because reviewer tier must be at least writer tier and it guards two stories.

## Execution

Each completed task fills its Evidence field and updates `pm/STATE.md` in the same run:

```markdown
### T-002: Save-link form and persistence  [Done]
- Evidence: pytest tests/test_save.py -> 4 passed; manual check 2026-07-05:
  added 5 links, restarted server, all 5 listed. Screenshot: docs/evidence/t002.png
```

```markdown
## Where the project stands
- Last completed: T-003 — search across title/tags/notes with tests
- Next up: T-004, then T-005 review
- Checkpoint status: CP1 approved, CP2 approved, CP3 approved, CP4 pending
```

During T-003 the model twice generated a wrong SQLite FTS query. Per the two-failure rule, the run stopped, recorded the working query pattern in the repo docs, and restarted the task with clean context instead of stacking corrections.

## Checkpoint CP4 — Final Acceptance

Tasks being done is not the finish line. Each success criterion is re-verified end-to-end against its **final check** from CP1, and evidence is linked:

```markdown
## Success Criteria
| ID | Criterion | Final check | Status |
| --- | --- | --- | --- |
| SC-1 | Links persist across restarts | 5 links added, server+browser restart, all present | verified — docs/evidence/sc1.png |
| SC-2 | Search finds the right links | "rust" returns the 2 Rust items, nothing else | verified — docs/evidence/sc2.png |
| SC-3 | One-command run | `make run` on clean clone serves app | verified — session log 2026-07-06 |

**CP4 — acceptance: approved by operator on 2026-07-06**
```

Only after the operator approves CP4 is the project reported as done. Residual items (R-1: no backup story for the SQLite file) move to `pm/DECISIONS.md` as recorded risks, not silent omissions.
