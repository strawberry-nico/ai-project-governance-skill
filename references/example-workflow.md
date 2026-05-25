# Example Workflow

Use these examples to check whether the skill is routing correctly. They are intentionally short; project files remain the source of truth.

## Example 1: Review Finds Missing Evidence

User says:

`验收 T012，更新 progress-board。`

Mode:

`Review Mode`

AI reads, if present:

- `AGENTS.md`
- `tasks/T012.md`
- `tasks/T000-blueprint.md`
- `tasks/progress-board.md`
- cited test logs, screenshots, diffs, or output artifacts
- `references/review-mode.md`

AI behavior:

- Reviews the task in its existing format, even if it is not the current three-section template.
- Checks each AC for yes/no status and concrete evidence.
- Does not invent scorecard scores if no T000/scorecard exists.
- Writes or updates the closest equivalent of `Architect Review`.
- Updates the board only when task status, gate evidence, score evidence, or active context changed.

Possible outcome:

`Needs reconcile: AC2 is marked complete, but no cited verification output exists. Updated tasks/T012.md and tasks/progress-board.md with review status.`

No new dispatch is created because the issue is inside T012 scope.

## Example 2: Reconcile Fixes Direct Drift

User says:

`T012 是不是跑偏了？先纠偏，不要派新任务。`

Mode:

`Reconcile Mode`

AI reads, if present:

- `AGENTS.md`
- `tasks/T012.md`
- `tasks/progress-board.md`
- relevant source files, tests, reports, or artifacts
- `references/reconcile-mode.md`

AI behavior:

- Classifies gaps before acting: incomplete AC, poor AC, dispatch deviation, stale board/report, boundary mismatch, or new scope.
- Repairs only direct in-scope drift.
- May fix directly related inconsistencies, such as a wrong task ID or stale AC status in the progress board. This is not opportunistic adjacent cleanup.
- Does not cross-file cleanup or format-migrate the task unless needed for current evidence.
- If the fix is new scope, stops and asks instead of dispatching because the user said not to.

Possible outcome:

`Reconciled T012: corrected stale AC2 evidence and fixed the matching T012 board row. No new task created.`

## Example 3: Dispatch With Readiness Check

User says:

`根据当前进度派发下一个任务。`

Mode:

`Dispatch Mode`

AI reads, if present:

- `AGENTS.md`
- `tasks/T000-blueprint.md`
- `tasks/progress-board.md`
- active reports that affect dependencies or gates
- `references/dispatch-mode.md`
- `assets/task-dispatch-template.md` or `assets/lightweight-task-template.md`

AI behavior:

- Does not run a full Review/Reconcile pass just because dispatch was requested.
- Does run a dispatch readiness check: current phase, gate state, blocked-by gates, active task dependencies, owner, parallel/sequential safety, and external-impact boundary.
- If no scorecard exists, does not invent dimension scores. It uses ACs, board state, user goals, and gate evidence as temporary readiness criteria, and records that scorecard evidence is missing.
- If expansion is blocked, moves the idea to backlog or dispatches a convergence task that unblocks the gate.
- Writes a new `tasks/Txxx.md` only when the active dispatch is allowed.

Possible outcome:

`Next task: tasks/T013.md`

If blocked:

`No active dispatch created: requested expansion is blocked by F1. Recommended convergence task: validate schema contract evidence for F1.`

## Example 4: Empty Or Under-Documented Project

User says:

`这个项目现在怎么样？`

Mode:

Usually `Review Mode` if the user wants status; otherwise answer from available files.

AI reads available project facts and skips missing files.

AI behavior:

- Does not fabricate project state.
- Reports missing baseline files such as `T000`, board, task files, reports, or scorecard.
- If the user wants governance started, suggests creating `tasks/T000-blueprint.md` before dispatching executable tasks.

Possible outcome:

`I cannot review project health yet: no T000, progress board, or task report exists. Next useful governance step is a T000 blueprint, not T001 execution.`
