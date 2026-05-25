# Execution Report: {{TASK_ID}}

> File: `tasks/{{TASK_ID}}-report.md`
> Legacy template: use only when the task already uses split `*-dispatch.md` / `*-report.md` files. For new tasks, fill the `## Report` section inside `tasks/{{TASK_ID}}.md`.

## Task Reference
- **Task ID**: 
- **Executed By**: (AI name / model)
- **Dispatch File**: `tasks/{{TASK_ID}}-dispatch.md`

## Attempt Log
(record each significant attempt; stop at abort condition)
| Attempt | Blocker ID / Failure Mode | What Tried | Result | Time/Effort |
|---------|----------------------------|-----------|--------|-------------|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

## Acceptance Criteria Response
(respond to each AC from the Dispatch section or legacy dispatch file)
- [ ] AC1: **STATUS** (completed / partial / blocked / not started)
  - Evidence: (file + line range, or specific behavior)
- [ ] AC2: **STATUS**
  - Evidence: 
- [ ] AC3: **STATUS**
  - Evidence: 

## End-to-End Validation Results
(if applicable per dispatch)
- **Validation method used**: 
- **Result**: passed / failed / not performed
- **Evidence**: (command output, diff, screenshot, simulation log, or user confirmation)
- **Does this evidence justify updating a gate status?** yes / no / pending architect review

## Evaluation Evidence
(connect report evidence back to the dispatch "Evaluation Impact"; do not update scores unless asked, but provide evidence the architect can use)

| Dimension | AI Evidence | Human Review Needed | Suggested Score Effect |
|-----------|-------------|---------------------|------------------------|
| | | yes/no | no change / candidate increase / candidate decrease |

## Gate Status Update
(based on this task's output, which gates may have moved?)

| Gate | Previous Status | Proposed Status | Reasoning | Evidence |
|------|-----------------|-----------------|-----------|----------|
| | | | | |

**Note:** Gate status changes are proposals for the architect AI to review. Do not assume a gate is passed just because this task is done.

## Changes Made
| File | Change Type | Summary |
|------|-------------|---------|
| `path/to/file` | add / modify / delete | one sentence |

## Opportunistic Improvements Used
(if you used allowed adjacent scope, declare it here; otherwise write "none")
- **Improvement**: 
- **Why it was necessary**: 
- **Files touched**: 

## Deviations
(unplanned changes; must be declared here)
- **Deviation**: 
- **Reason**: 

## Blockers
(what prevents further progress)
- **Blocker**: 
- **Same blocker repeated 3 times?** yes / no
- **Needs from architect / user**: 

## Next Suggestions
(optional; executor's view on next logical task)
