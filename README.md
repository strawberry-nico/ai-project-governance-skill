# AI Project Governance

`ai-project-governance` is a Codex skill for keeping AI-led projects aligned across multiple tasks, reports, reviews, and agents.

It is not a normal todo-list format. It is a file-backed governance protocol for answering:

- What is the project trying to become?
- Which work is allowed now?
- Which work is blocked until foundations are stable?
- Did the executor actually satisfy the acceptance criteria?
- Is the progress board describing reality or just intent?

## When To Use

Use this skill when work involves:

- Dispatching tasks to executor AIs
- Reviewing reports or acceptance evidence
- Checking whether a project has drifted
- Repairing unfinished or poorly executed task scope
- Updating progress boards, gates, or scorecards
- Managing multi-phase work where later tasks depend on earlier stability

For a small local edit, use the lightweight path: edit, verify, summarize. Do not create governance artifacts unless they add control.

## Three Modes

| Mode | User Intent | Default Behavior |
|------|-------------|------------------|
| Review | 复查 / 验收 / update board/gate/score | Evaluate existing evidence and update status |
| Reconcile | 纠偏 / 有没有跑偏 / 补齐没做好 | Repair existing in-scope drift before new tasks |
| Dispatch | 派发任务 / 拆任务 / hand to executor AI | Write or update `tasks/Txxx.md` |

If unclear, prefer the least expansive mode: **Review > Reconcile > Dispatch**.

## Core Artifacts

| Artifact | Purpose |
|----------|---------|
| `tasks/T000-blueprint.md` | Project boundaries, scorecard, phase gates, task breakdown |
| `tasks/Txxx.md` | One executable task with Dispatch, Report, and Architect Review sections |
| `tasks/progress-board.md` | Current phase, active tasks, gates, scores, blockers, allowed next work |

## Main Rule

Do not dispatch expansion work just because it is interesting or requested in the moment.

First check the blueprint, progress board, gates, scorecard, and current evidence. If foundations are weak, dispatch convergence work or reconcile the existing task instead.

## Files In This Skill

| File | Purpose |
|------|---------|
| `SKILL.md` | Agent entrypoint and routing rules |
| `references/dispatch-mode.md` | Task dispatch workflow |
| `references/reconcile-mode.md` | Drift detection and repair workflow |
| `references/review-mode.md` | Report, gate, score, and board review workflow |
| `references/gates-scorecard.md` | Detailed gate, scorecard, architecture-health, and debt rules |
| `references/document-maintenance.md` | Archive and active-context slimming rules |
| `assets/project-blueprint-template.md` | T000 blueprint template |
| `assets/task-dispatch-template.md` | Full governed task template |
| `assets/lightweight-task-template.md` | Small governed task template |
| `assets/progress-board-template.md` | Progress board template |

## Migration From `ai-task-bridge`

Existing split `*-dispatch.md` and `*-report.md` files remain readable.

For new work:

1. Add or update `tasks/T000-blueprint.md` with phase gates.
2. Add gate status and scorecard sections to the progress board.
3. Use single-file `tasks/Txxx.md` for new executable tasks.
4. Do not redo old completed tasks unless their evidence is needed for a current gate.
