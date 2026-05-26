---
name: ai-project-governance
description: "Use when governing AI project delivery through file-backed dispatch, reconciliation, review, phase gates, scorecards, progress boards, or multi-agent handoffs. Trigger for requests like dispatch tasks, 派发任务, 拆任务, review reports, 复查, 验收, 纠偏, check drift, update progress-board, update gates, update scorecard, or decide whether a project has gone off track. Do not use for ordinary low-risk one-off edits unless the user asks for governance artifacts."
---

# AI Project Governance

Govern AI project work with file-based artifacts, mode routing, acceptance evidence, phase gates, and scorecards.

This skill is not a generic project-management wrapper. Use it to keep multi-step AI work from drifting away from the user's intended outcome.

## Mode Routing

Classify the request into exactly one mode before acting.

| Mode | Use When The User Says | Default Action | Load If Needed |
|------|------------------------|----------------|----------------|
| **Review Mode** | review report, 复查, 验收, update board/gate/score, judge whether ACs passed | Evaluate existing evidence and update status artifacts | `references/review-mode.md` |
| **Reconcile Mode** | 纠偏, check drift, 有没有跑偏, 补齐没做好的, fix original task, align with T000 | Repair existing in-scope drift before creating new tasks | `references/reconcile-mode.md` |
| **Dispatch Mode** | dispatch, 派发任务, 拆任务, write next task, hand this to executor AI | Create or update `tasks/Txxx.md` | `references/dispatch-mode.md` |

If intent is ambiguous, choose the least expansive mode: **Review > Reconcile > Dispatch**. This priority is for ambiguous intent only. If the user explicitly asks to dispatch, use Dispatch Mode, but still run the dispatch readiness/gate check before writing an active task.

Do not create a new dispatch during Review or Reconcile unless the remaining work is outside the current task boundary, conflicts with another active task, requires user/product clarification, or the user explicitly asks for a new task.

After choosing a mode, load that mode's reference file before acting. The main `SKILL.md` is the router; the mode reference is the operating checklist.

## Project Entry Protocol

Before acting inside an existing project, read project-local facts before applying this generic flow. If a listed file does not exist, skip it and continue; missing files are facts to report or compensate for, not blockers by themselves.

1. `AGENTS.md` or project-specific agent contract / SOP
2. `README.md`
3. `docs/framework.md`, `docs/north-star.md`, or equivalent architecture overview
4. `tasks/T000-blueprint.md` if present
5. `tasks/progress-board.md` or the user-defined board
6. `tasks/boards/README.md` and relevant module board, if present
7. Relevant contract, schema, design doc, source files, tests, outputs, or reports

Do not infer current state from chat history when project files exist. Project-specific rules override this skill unless they require unsafe, destructive, or clearly out-of-scope behavior.

## Process Weight

Use the full governance flow when the work affects architecture, module boundaries, APIs, data models, persistence, deployment, user workflow, business semantics, knowledge governance, external systems, multi-agent handoffs, phase gates, or scorecard dimensions.

Use lightweight execution when the work is local, low-risk, directly verifiable, and does not move product behavior, architecture, data, deployment, gate status, or scorecard dimensions.

For lightweight execution, do not create unnecessary task files. Make the change directly, verify it if needed, and summarize the outcome in chat or the relevant existing file.

Use the lightweight path for small board/status hygiene too, when the update only records an already-verified fact and does not change task status, gate status, scorecard evidence, allowed next work, or execution coordination. Examples: fixing a typo in a board row, correcting a broken path, adding a missing date to an already accepted task, or noting a command result the user explicitly asked to record.

If a request looks like governance but only needs a direct factual update, do the small update and say why full governance was not invoked.

## Core Rules

1. **Files are the source of truth** — task details, reports, reviews, boards, and gates live in files, not pasted chat blocks.
2. **Acceptance criteria define done** — effort, confidence, and partial progress are not substitutes for AC evidence.
3. **One executable task per file** — new tasks use `tasks/Txxx.md` with `Dispatch`, `Report`, and `Architect Review` sections.
4. **T000 before broad dispatch** — new projects or major features need `tasks/T000-blueprint.md` with boundaries, dimensions, gates, and a task breakdown before normal task dispatch.
5. **Review/Reconcile before redispatch** — stale reports, incomplete ACs, and in-scope drift are repaired in the existing task before new work is created.
6. **Gate before expansion** — expansion tasks are blocked until prerequisite gates pass and target dimensions meet the project threshold, default `60/100`.
7. **Convergence is allowed** — convergence tasks may fix, tighten, validate, connect, or unblock failed/locked/in-progress gates.
8. **Small dimensional impact** — each dispatch should primarily improve 1-3 scorecard dimensions.
9. **Bound file scope** — every dispatch must name primary files, allowed adjacent files, forbidden files, and external-impact boundaries.
10. **Declare coordination** — every dispatch round must state owner, parallel/sequential safety, dependencies, and execution order.
11. **Abort on blocker loops** — executor stops after 3 consecutive attempts against the same blocker/failure mode and writes the report.
12. **External writes need authorization** — pushes, publishing, account settings, production sync, and third-party CRUD require explicit user or project-file approval.
13. **Autonomy stays inside boundaries** — permission automation and fewer prompts are useful only inside explicit task scope, allowed files, ACs, verification, abort conditions, and external-impact gates.
14. **Architecture health matters** — code-changing tasks must review coupling, cohesion, code smells, and testability before being accepted.
15. **Separate evidence from opinion** — AI evidence covers implementation, tests, logs, diffs, screenshots, and artifacts; human evidence covers usefulness, taste, trust, market fit, and workflow fit.
16. **No opportunistic adjacent edits by default** — adjacent cleanup must be explicitly allowed and reported.
17. **Do not revive legacy paths silently** — archived tasks, obsolete fields, deleted shells, and old scripts stay inactive unless compatibility requires them.
18. **Respect existing task formats** — read and maintain non-standard project task formats when they already exist; do not force-migrate old tasks unless the user asks or the migration is necessary for current evidence.
19. **Do not invent missing scorecards** — if no T000/scorecard exists, do not make up dimension scores. Use ACs, board state, and user goals as temporary review criteria, and record that scorecard/gate evidence is missing.
20. **Archive deliberately** — completed task cleanup and board slimming are governed by `references/document-maintenance.md`; never archive active or disputed evidence.
21. **Use `N/A`, not fiction** — when a template field does not apply or evidence is missing, write `N/A`, `not applicable`, or `missing evidence`; do not fill governance tables with invented dimensions, gates, scores, risks, or validation results.

Detailed gate, scorecard, architecture health, and debt rules live in `references/gates-scorecard.md`.

## Artifact Conventions

| Artifact | Naming Convention | Writer | Notes |
|----------|-------------------|--------|-------|
| Project blueprint | `tasks/T000-blueprint.md` | Architect AI | Meta-task; executable tasks start at `T001` |
| Task file | `tasks/{TASK_ID}.md` | Architect / Executor / Architect | New standard format |
| Legacy dispatch | `tasks/{TASK_ID}-dispatch.md` | Architect AI | Read and maintain only for old projects |
| Legacy report | `tasks/{TASK_ID}-report.md` | Executor AI | Do not create for new tasks unless requested |
| Progress board | `tasks/progress-board.md` or user-defined file | Architect AI / User | Daily project status source |

Task IDs use `T` + 3-digit zero-padded number: `T001`, `T002`, etc. `T000` is reserved for the blueprint.

New task files use these sections:

1. `## Dispatch` — architect-owned handoff
2. `## Report` — executor-owned evidence
3. `## Architect Review` — architect-owned acceptance decision

During execution, changing `## Dispatch` is a deviation unless the architect/user explicitly asked for a dispatch correction.

## Standard Workflow

### Step 0: Blueprint for New Projects

When the user starts from a vague project or major feature:

1. Read `assets/project-blueprint-template.md`
2. Write `tasks/T000-blueprint.md`
3. Include architecture boundaries, scorecard dimensions, phase gates, task breakdown, and validation method
4. Ask for explicit user confirmation before dispatching executable tasks

The blueprint is accepted only when the user confirms the project boundaries, dimensions, gates, and task breakdown.

### Step 1: Dispatch Mode

Use only when the user asks to create/split/hand off work, or when Review/Reconcile proves remaining work is new scope.

1. Read `references/dispatch-mode.md`, project facts, T000 if present, board if present, and active reports
2. Run the gate check
3. Use `assets/task-dispatch-template.md` for full governance tasks
4. Use `assets/lightweight-task-template.md` only for low-risk governed tasks that still need a file
5. Write `tasks/{NEXT_ID}.md`
6. In chat, return only the path and any coordination note the user needs

### Step 2: Execute and Report

The executor AI:

1. Reads the task file
2. Executes within allowed scope
3. Fills `## Report` in the same task file
4. Reports blockers after 3 attempts on the same blocker
5. In chat, returns only the path

If the executor returns only free-form chat without updating the report file, reject it and ask for the file update.

### Step 3: Review Mode

Use when the user asks to review, accept, update board, update gate, or update score.

1. Read `references/review-mode.md`, the task Dispatch and Report, plus board and T000 if present
2. Evaluate AC evidence, file-boundary compliance, external-impact compliance, validation evidence, gate status, scorecard impact, and architecture health
3. Fill `## Architect Review`
4. Update the progress board if task status, gate evidence, score evidence, or active context changed
5. Switch to Reconcile Mode if current scope is incomplete or poorly evidenced

### Step 4: Reconcile Mode

Use when the user asks whether work drifted, whether a task was done poorly, or to fix existing scope.

1. Read `references/reconcile-mode.md`, T000 if present, board if present, active task/report, source files, tests, and artifacts
2. Classify gaps as incomplete AC, poor AC, dispatch deviation, boundary/gate/score mismatch, stale evidence, or new scope
3. Repair in-scope gaps directly when the fix is concrete, worthwhile, pattern-matching, high-confidence, and within boundary
4. Update Report, Architect Review, and board evidence as needed
5. Create a new dispatch only for true new scope or unresolved product decisions

## Gate Check Before Dispatch

Before writing `tasks/Txxx.md`, answer:

```text
□ Is this actually Dispatch Mode?
□ Have project-specific rules, T000, board, and relevant module boundaries been read?
□ What phase is the project in?
□ Which gates are passed / in-progress / locked / failed?
□ Which module owns the task, and what interfaces does it touch?
□ Is this convergence or expansion?
□ If expansion, are all prerequisite gates passed?
□ If expansion, are target dimension scores at or above threshold? If no scorecard exists, do not invent scores; treat this as missing governance evidence and use AC/board readiness only for temporary judgment.
□ If convergence, which gate/dimension does it repair or unblock?
□ Does it touch output, generator, data model, or cross-module contract? If yes, is end-to-end validation in ACs?
□ Does it require external writes? If yes, is explicit authorization present?
□ Does it improve 1-3 dimensions instead of claiming to fix everything?
```

If any required check fails, do not dispatch the task as active. Reframe it as convergence, move it to backlog, or ask the user for clarification.

## Anti-Patterns

- Pasting full dispatch/report content into chat instead of writing files
- Creating split `*-dispatch.md` / `*-report.md` files for new tasks by default
- Dispatching expansion work on unstable foundations
- Confusing task AC completion with gate pass
- Updating scores as praise, mood, or confidence
- Creating megatasks with broad scope, vague ACs, or many unrelated files
- Claiming everything improves every scorecard dimension
- Hiding deviations, dry-runs, or external-write status
- Doing architecture review only at the end of a project
- Fixing every nearby issue during Reconcile without checking scope and value
- Combining implementation changes and governance-record cleanup when the project expects separate commits
- Creating new documents that increase active reading burden without replacing or shrinking old ones

## References and Assets

Load these only when needed:

| File | Use For |
|------|---------|
| `references/dispatch-mode.md` | Writing task dispatches and blueprints |
| `references/reconcile-mode.md` | Drift checks and in-scope repair |
| `references/review-mode.md` | AC, report, gate, score, and board review |
| `references/gates-scorecard.md` | Gate lifecycle, score rules, architecture health, debt handling |
| `references/document-maintenance.md` | Archiving, progress-board slimming, old-doc cleanup |
| `references/example-workflow.md` | End-to-end example |
| `assets/project-blueprint-template.md` | `tasks/T000-blueprint.md` |
| `assets/task-dispatch-template.md` | Full governed `tasks/Txxx.md` |
| `assets/lightweight-task-template.md` | Small governed `tasks/Txxx.md` |
| `assets/execution-report-template.md` | Legacy split reports only |
| `assets/progress-board-template.md` | `tasks/progress-board.md` |
