# Reconcile Mode

Use Reconcile Mode when the user wants drift detection, correction, or completion of existing work.

## Triggers

- "纠偏"
- "检查有没有跑偏"
- "补齐没做好的"
- "修原来的 bug"
- "对齐 T000"
- "这个任务是不是没做好"
- "不要派新任务，先修"

## Default Output

Directly repair the existing task scope. Do not create a new dispatch by default.

After repair, summarize:

- what drift was found
- what was fixed
- which existing report/board evidence was updated, if any
- what remains blocked, if anything

If the user asked for "不要派新任务" or "先修", do not create a dispatch unless the fix clearly violates the current task boundary and needs user approval.

## Required Inputs

Read these when present:

- `AGENTS.md` or project-specific operating rules
- `tasks/T000-blueprint.md`
- `tasks/progress-board.md` or the user-defined board
- active `tasks/Txxx.md` task file
- for legacy tasks, active `tasks/Txxx-dispatch.md` and matching `tasks/Txxx-report.md`
- relevant source files, tests, output artifacts, screenshots, or logs
- `references/gates-scorecard.md` when the gap affects gate, score, architecture health, or debt status

If an input file does not exist, skip it and continue. Do not fabricate missing T000, board, report, gate, or scorecard content. If a missing artifact prevents reconciliation, report the missing baseline and ask for the needed file or decision.

## Gap Types

Classify every issue before acting:

| Gap Type | Default Action |
|----------|----------------|
| Existing AC not completed | Finish it inside current scope |
| Existing AC completed poorly | Repair implementation or evidence |
| Implementation deviated from dispatch | Bring implementation back to scope or document the deviation |
| Boundary/gate/scorecard mismatch | Correct board/report evidence or ask if product scope changed |
| Board/report stale or inaccurate | Update the existing artifact |
| Truly new scope | Ask or create dispatch only if explicitly appropriate |

Directly related inconsistencies are in scope for Reconcile. For example, fixing a wrong task ID in the progress board, correcting stale AC status, or updating evidence that directly describes the active task is not an opportunistic adjacent edit.

## New Dispatch Gate

Create a new dispatch only when at least one condition is true:

- the fix is outside the current task boundary
- the fix would touch unrelated modules or files
- the fix conflicts with another active task
- the fix requires user/product clarification
- the work is too large to safely repair inline
- the user explicitly asks for a new task

If none are true, repair the existing work.

## Repair Checklist

- Preserve existing task ID and scope
- Avoid speculative cleanup outside the affected area. Do not cross-file cleanup unless the file is part of the drift evidence or current task boundary.
- Apply the actionability filter before repairing non-obvious gaps
- Add or update tests only where needed to verify the repaired AC
- Update the existing task file's Report or Architect Review section when evidence changed; for legacy tasks, update the existing report
- Update the progress board when task status, AC progress, gate evidence, or score evidence changed
- Do not mark a gate `passed` unless pass criteria are evidenced

## Actionability Filter

Repair now only when the gap passes all checks:

- **In scope**: introduced or meaningfully worsened by current task/change
- **Worth the churn**: fix value exceeds refactor or coordination cost
- **Matches codebase patterns**: does not require alien abstractions
- **Not intentional**: not a documented tradeoff
- **Concrete impact**: consequence can be stated clearly
- **Author would prioritize**: reasonable author would fix before shipping
- **High confidence**: this is real, not speculative

If any check fails, record it as a backlog note or review risk instead of repairing now.

## Existing Format Compatibility

Projects may contain task files that do not match the current `Dispatch / Report / Architect Review` template and are not legacy split files.

For Reconcile:

- Read the existing structure and locate the equivalent dispatch, work, AC, report, and review evidence.
- Update the smallest existing section that carries the stale or inaccurate evidence.
- Do not rewrite the whole task into the new template unless the user asks or current evidence cannot be represented safely in the old shape.

## Minimal Example

User asks: "T012 是不是跑偏了，先纠偏。"

Architect AI:

1. Reads T012 Dispatch/Report, T000, board, and touched files.
2. Finds AC2 evidence is stale and implementation changed a forbidden file.
3. Repairs or reverts only the in-scope drift if safe.
4. Updates T012 Architect Review and board.
5. Summarizes drift found, fix made, and remaining blocker.
