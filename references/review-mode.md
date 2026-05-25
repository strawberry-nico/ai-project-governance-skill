# Review Mode

Use Review Mode when the user wants evidence evaluated, not new work created.

## Triggers

- "review"
- "复查"
- "验收"
- "审核 report"
- "更新 progress-board"
- "判断 gate 是否通过"
- "更新 scorecard"

## Default Output

Evaluate the existing evidence and update status artifacts when appropriate.

Do not create a new dispatch unless review proves the remaining work is genuinely new scope.

If current scope is incomplete or poorly evidenced, choose `Needs reconcile` instead of dispatching another task.

## Required Inputs

Read these when present:

- `AGENTS.md` or project-specific operating rules
- the target `tasks/Txxx.md` task file
- for legacy tasks, the target `tasks/Txxx-report.md` and matching `tasks/Txxx-dispatch.md`
- `tasks/T000-blueprint.md`
- `tasks/progress-board.md` or the user-defined board
- referenced test logs, screenshots, output artifacts, diffs, or files
- `references/gates-scorecard.md` for score, gate, architecture-health, or debt decisions

If an input file does not exist, skip it and continue. Do not fabricate missing T000, board, report, gate, or scorecard content. If missing evidence prevents acceptance, choose `Blocked` or `Needs reconcile` and name the missing artifact.

## Review Checklist

For the task:

- Does every AC have yes/no status?
- Does each completed AC cite concrete evidence?
- Are deviations declared?
- Are opportunistic improvements within allowed adjacent scope?
- Are blockers specific and blocker-scoped?

For gates:

- Did the task include required end-to-end validation?
- Is validation evidence present and relevant?
- Does evidence satisfy every gate pass criterion?
- If not, keep the gate `in-progress` or `failed`

For scorecard:

- Update scores only with concrete evidence
- Keep AI evidence separate from human review evidence
- Treat scores as capability maturity, not sentiment
- Use `/100` scores unless the project explicitly defines another scale
- If no scorecard exists, do not invent scores. Review ACs, board state, and user-defined goals instead, and record that scorecard evidence is missing.

For architecture health on code-changing tasks:

- Check coupling, cohesion, code smells, and testability
- Classify any degradation as strategic debt or accidental debt
- Do not accept accidental debt that blocks the task's own ACs or gate criteria

For existing task formats:

- Review the task in the format it already uses.
- Map equivalent sections to Dispatch, Report, and Architect Review concepts.
- Do not force-migrate a task file into the current template during review unless the user asks or the current format prevents accurate evidence recording.

## Outcomes

Choose one:

- **Accepted**: ACs met; update board/report evidence
- **Accepted with notes**: ACs met, but follow-up risks exist
- **Needs reconcile**: existing scope is incomplete or poorly evidenced; switch to Reconcile Mode
- **Needs new dispatch**: remaining work is outside current scope
- **Blocked**: user/product decision or external dependency is required

## Minimal Example

User asks: "验收 T012，更新 board。"

Architect AI:

1. Reads T012 Dispatch/Report, T000, board, and cited evidence.
2. Checks every AC has yes/no status and concrete evidence.
3. Reviews gate and score impact.
4. Writes T012 Architect Review.
5. Updates progress board if status, gate, score, or active context changed.
6. Responds with accepted / needs reconcile / blocked and the changed file paths.
