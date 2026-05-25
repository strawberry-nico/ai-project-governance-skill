# Dispatch Mode

Use Dispatch Mode only when the user asks to create, split, or hand off work.

Dispatch Mode does not require a full Review/Reconcile pass first when the user intent is explicit. It does require a dispatch readiness check: read current project facts, gates, board evidence, and active reports enough to avoid dispatching blocked or stale work.

## Triggers

- "派发任务"
- "dispatch"
- "拆任务"
- "写下一个任务"
- "交给执行 AI"
- "根据 T000 / progress-board 生成 Txxx"

## Default Output

Write one task file:

`tasks/{TASK_ID}.md`

Then respond only with the path:

`Next task: tasks/{TASK_ID}.md`

If there are multiple tasks in the dispatch round, also state the minimum coordination the user needs: owner, parallel/sequential status, dependencies, and execution order. Keep details in files.

## Required Inputs

Read these when present:

- `AGENTS.md` or project-specific operating rules
- `tasks/T000-blueprint.md`
- `tasks/progress-board.md` or the user-defined board
- relevant module board or ownership file
- active reports that affect dependencies or gates
- `assets/task-dispatch-template.md` for full governance tasks
- `assets/lightweight-task-template.md` for low-risk governed tasks that still need a file

If an input file does not exist, skip it and continue. Do not fabricate its contents. Record missing T000, missing board, or missing scorecard as governance gaps when they affect dispatch safety.

## Dispatch Checklist

Before writing a dispatch:

- Confirm this is Dispatch Mode, not Review or Reconcile
- Identify the current phase and gate states
- Classify the task as `convergence` or `expansion`
- For expansion, verify all blocked-by gates are `passed`
- For expansion, verify target dimensions are at least `60/100` or the project-defined threshold
- If no scorecard exists, do not invent dimension scores. Use ACs, board state, user goals, and gate evidence as temporary readiness criteria, and note that scorecard evidence is missing.
- For convergence, state which gate/dimension it repairs, tightens, validates, or unblocks
- Keep the task focused on 1-3 scorecard dimensions
- Keep primary files to 3 or fewer unless the task genuinely requires more
- Name required files, allowed adjacent files, and forbidden files
- State external-impact boundary: no external write, dry-run only, or explicitly authorized real write
- State owner, parallel/sequential safety, dependencies, and execution order
- Include end-to-end validation when touching output, generator, data model, or cross-module contracts

Load `references/gates-scorecard.md` when gate or score status is unclear.

## File Format

New tasks use one file, `tasks/{TASK_ID}.md`, with three sections:

- `## Dispatch` — architect handoff
- `## Report` — executor evidence, filled after execution
- `## Architect Review` — architect acceptance notes, filled during review/reconcile

Section ownership is strict: architect AI owns Dispatch and Architect Review; executor AI owns only Report. If an executor changes Dispatch without explicit permission, treat it as a deviation during review.

Legacy split files (`tasks/{TASK_ID}-dispatch.md` and `tasks/{TASK_ID}-report.md`) may be read and maintained for older projects, but do not create them for new tasks unless the user explicitly requests the legacy format.

Some projects have non-standard mixed task formats that are neither the current single-file template nor legacy split files. Read and maintain those files in their existing shape. Do not force-migrate old task files just to satisfy this skill. New task files should use the current single-file format unless the project explicitly standardizes another format.

Use the full template by default when the task touches architecture, user workflow, data, external systems, multiple modules, phase gates, or scorecard movement.

Use the lightweight template only when the task is local, low-risk, directly verifiable, and still benefits from a file-backed handoff.

## When Not To Dispatch

Do not create a new dispatch when:

- the user asked to review a report
- the user asked to check drift or fix existing work
- the gap is inside the current dispatch's accepted scope
- the board/report is stale and can be updated directly
- the issue is a small local repair that can be completed now

Use Reconcile Mode instead.

## Minimal Example

User asks: "根据 T000 派发下一个任务。"

Architect AI:

1. Reads project rules, T000, progress board, and active reports.
2. Confirms the next task is not blocked by gates.
3. Writes `tasks/T012.md`.
4. Responds: `Next task: tasks/T012.md`.
