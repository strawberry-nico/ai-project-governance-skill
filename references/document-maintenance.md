# Document Maintenance

Use this reference when the project has too many active task files, stale boards, duplicated status docs, or the user says the docs feel heavy.

The goal is active-context weight loss, not prettier documentation.

The progress board is meant to be read frequently. If it becomes too long to scan at the start of a task, it has become a token sink and should be compressed.

## File Lifecycle

- Keep forever: the progress board file, default `tasks/progress-board.md`
- Keep active in `tasks/`: active task files, the current useful blueprint, and the board
- After task status is `done`: move `tasks/{TASK_ID}.md` to `tasks/archive/YYYY-MM/`
- Legacy done tasks: move both `tasks/{TASK_ID}-dispatch.md` and `tasks/{TASK_ID}-report.md` to the same monthly archive folder
- Never archive active, disputed, or under-evidenced work
- Prefer archive over deletion unless files are generated junk, empty shells, or the user explicitly asks for deletion

## Daily Status Source

Treat `tasks/progress-board.md` as the daily status source unless the project defines another board.

The board should show:

- Current phase
- Active tasks
- Blockers
- Passed/failed/in-progress gates
- Allowed next work
- Work that must not be dispatched yet

## Slimming Triggers

Run a slimming pass when any of these happen:

- Task root has more than 20 task files
- Progress board exceeds about 300 lines
- Progress board takes more than a quick scan to identify current phase, active tasks, gates, blockers, and allowed next work
- README exceeds about 500 lines
- Framework/status docs repeat the same phase narrative
- A major phase closes
- The user says the project/docs feel heavy
- Old decisions are being re-litigated
- The user has to correct the same boundary more than once

## Slimming Actions

1. Back up the full progress board to `tasks/archive/YYYY-MM/`
2. Archive completed task files by month
3. Compress the active progress board to current phase, active tasks, gate status, scorecard, execution rules, and handoff only
4. Trim README to project purpose, run instructions, and current fact-source links
5. Remove duplicated status narrative from framework docs
6. Do not create a new explanatory document unless it replaces or shrinks an existing active document

The compressed board should answer these in one pass:

- What phase are we in?
- What is active now?
- What is blocked?
- Which gates have passed or failed?
- What work is allowed next?
- What work must not be dispatched yet?

## Report Evidence

Any slimming task report should include:

- Root task-file count before and after
- Line counts for main active docs before and after
- Files archived
- Files shortened
- Any evidence intentionally preserved in archive

## Context Handoff Trigger

If the discussion becomes repetitive or old decisions keep resurfacing, pause expansion work.

First write the current agreement into project fact sources such as `AGENTS.md`, framework docs, progress board, or module boards. Then suggest opening a fresh thread/window if the current context is overloaded.
