# Project Progress Board

> Default file: `tasks/progress-board.md`
> Alternative: add this section to your project `README.md` or any existing doc
> Default maintainer: architect AI; executor AI may update when explicitly asked
> User should only need to point the architect AI to the board path

## Phase / Sprint: {{NAME}}

## Summary
- Total Tasks: 
- Completed ACs:  / 
- Blocked: 
- Current Phase: Foundation / Output Convergence / Closed-Loop Validation / Expansion

## Gate Status

Track the phase gates defined in `tasks/T000-blueprint.md`. Only the architect AI updates gate status after reviewing evidence.

| Gate | Phase | Status | Pass Criteria Summary | Evidence | Last Updated |
|------|-------|--------|----------------------|----------|--------------|
| F1 | Foundation | locked / in-progress / passed / failed | | | |
| F2 | Foundation | locked / in-progress / passed / failed | | | |
| O1 | Output Convergence | locked / in-progress / passed / failed | | | |
| V1 | Closed-Loop Validation | locked / in-progress / passed / failed | | | |

**Gate status rules:**
- `locked` = criteria defined but work not yet started
- `in-progress` = work ongoing; may be blocked by active tasks
- `passed` = all pass criteria evidenced and reviewed by architect
- `failed` = validation attempted and failed; must re-converge before retry

**Blocking map:**
| Gate | Blocks These Task Types | Until Status Is |
|------|------------------------|-----------------|
| F1 | expansion in any dimension | passed |
| O1 | expansion in output/UX dimensions | passed |

## Project Health Scorecard

> Use the same dimensions defined in `tasks/T000-blueprint.md`. Update scores only when there is evidence from completed tasks, user review, tests, or concrete artifacts.
> Scores represent capability maturity against the defined standard, not sentiment or effort.
> AI Evidence = implementation correctness, structure, tests, logs, screenshots, diffs, artifact checks, and architecture consistency.
> Human Review Evidence = usefulness, workflow fit, trust, taste, market/category fit, and whether the artifact feels real in the intended context.

| Dimension | Current Score | Target Score | AI Evidence | Human Review Evidence | Gap To Standard | Next Action |
|-----------|---------------|--------------|-------------|-----------------------|-----------------|-------------|
| | / 100 | / 100 | | | | |

## Task Registry

| Task ID | Name | Status | AC Progress | Blocker | Task Type | Task File |
|---------|------|--------|-------------|---------|-----------|-----------|
| | | not started / in progress / review / done | / | | conv / exp | `tasks/T001.md` |

## Active Context
(what the executor is currently working on; executor may update this when explicitly asked, otherwise architect maintains it)

## Recent Decisions
(architecture decisions from last 3 tasks; prevents re-discussion)

## Up Next
(top 3 upcoming tasks; populated by architect review after gate check)

## Document Hygiene
(record periodic cleanup of old task files, stale docs, unused templates/evals, and archive moves)

| Date | Trigger | Action | Files / Folders | Notes |
|------|---------|--------|-----------------|-------|
| | | | | |
