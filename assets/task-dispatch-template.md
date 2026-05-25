# Task: {{TASK_ID}}

> File: `tasks/{{TASK_ID}}.md`

## Dispatch

> Owner: Architect AI. Executor AI must not edit this section during execution unless the architect/user explicitly asks for a dispatch correction.

### Basics
- **Task Name**: 
- **Project**: 
- **Priority**: P0 / P1 / P2
- **Workstream / Layer**: main-chain / knowledge / output / tests / other
- **Depends On**: (task IDs, or "none")
- **Parallel Safety**: parallel-safe / sequential / architect-owned
- **Owner**: architect/self / executor AI / external agent / user
- **Execution Order**: first / second batch / after Txxx / parallel with Txxx / low-priority backlog
- **Why This Task Is Separate**: (one sentence; explain non-overlap or dependency)

### Gate Check

Before this task was dispatched, the architect AI verified:

- [ ] **Task type**: `convergence` (fix / tighten / validate / connect) OR `expansion` (new feature / module / capability)
- [ ] **Blocked by gates**: (gate IDs, or "none")
- [ ] **Gate status at dispatch**: all blocked-by gates are `passed` if expansion; if convergence, this task explicitly repairs/unblocks gates that are `locked`, `failed`, or `in-progress`
- [ ] **Dimension score check**: if this is expansion, target dimension score ≥ 60 / 100 (or project-defined threshold)
- [ ] **End-to-end validation required?** yes / no — if yes, validation method is described in ACs

**If any gate check item failed, this task must be reframed or moved to backlog.**

### Context Summary
(max 200 words; reference files by path, do not paste code)

### Evaluation Impact
(connect this task to the T000 scorecard; if no T000 exists, write the project dimension this task is meant to improve. Use 1-3 primary dimensions only.)

| Dimension | Expected Capability Change | Evidence To Review | Score Update Candidate? |
|-----------|----------------------------|--------------------|-------------------------|
| | | | yes/no |

**Non-goals for this task:** (name relevant scorecard dimensions this task deliberately does not try to improve)

### Primary Files
(required files; executor must focus here)
- `path/to/file.ext`

### Allowed Adjacent Files
(same-domain supporting files that may be updated if needed to satisfy the task cleanly)
- `path/to/adjacent-file.ext`

### Allowed Opportunistic Improvements
(explicitly allowed same-domain cleanup or supporting work; if used, must be declared in the report)
- (example) add missing ingredient entries required by newly added recipe templates
- (example) clean low-quality annotations in touched template/data files

### Acceptance Criteria
(these define "done"; executor must return yes/no per item)
- [ ] AC1: 
- [ ] AC2: 
- [ ] AC3: 

### End-to-End Validation (if applicable)
If this task modifies output layer, generator, data model, or cross-module contract, describe the validation step here:
- **Validation method**: (e.g., run full pipeline, AI simulation, regression test, schema diff)
- **Pass criteria**: 
- **Command / script**: 
- **Expected result**: 

### Constraints
- **Do NOT modify**: 
- **Must preserve**: 
- **Tech constraints**: 

### Verification
- **Command**: 
- **Expected Result**: 

### Abort Condition
(stop and write report if any of these happen)
- Max retries on same blocker: 3
- Same blocker means: same failure mode/root cause persists across attempts
- Stop if: (describe specific failure modes where effort is wasted)
- Timeout / effort limit: (e.g., "if this takes >30 min, stop and report")

### Reference
(relevant docs, previous reports, or code snippets by path)

## Report

> Owner: Executor AI. Fill this section after execution. Do not edit `## Dispatch`. Do not create a separate report file for new tasks unless the user explicitly requests the legacy format.

### Task Reference
- **Task ID**: {{TASK_ID}}
- **Executed By**: 
- **Dispatch Section**: `tasks/{{TASK_ID}}.md#dispatch`

### Attempt Log
| Attempt | Blocker ID / Failure Mode | What Tried | Result | Time/Effort |
|---------|----------------------------|-----------|--------|-------------|
| 1 | | | | |

### Acceptance Criteria Response
- [ ] AC1: **STATUS** (completed / partial / blocked / not started)
  - Evidence:

### End-to-End Validation Results
- **Validation method used**:
- **Result**: passed / failed / not performed
- **Evidence**:
- **Does this evidence justify updating a gate status?** yes / no / pending architect review

### Evaluation Evidence
| Dimension | AI Evidence | Human Review Needed | Suggested Score Effect |
|-----------|-------------|---------------------|------------------------|
| | | yes/no | no change / candidate increase / candidate decrease |

### Changes Made
| File | Change Type | Summary |
|------|-------------|---------|
| `path/to/file` | add / modify / delete | one sentence |

### Deviations / Blockers / Next Suggestions
- **Deviations**:
- **Blockers**:
- **Next Suggestions**:

## Architect Review

> Owner: Architect AI. Executor AI leaves this section blank unless explicitly instructed.

### Review Outcome
- **Status**: accepted / accepted with notes / needs reconcile / needs new dispatch / blocked
- **Reviewed By**:
- **Reviewed At**:

### Acceptance Decision
- [ ] AC1:

### Gate / Score / Board Updates
- **Gate changes**:
- **Score changes**:
- **Progress board updated**: yes / no

### Architect Notes
- 
