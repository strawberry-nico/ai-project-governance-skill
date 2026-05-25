# Gates and Scorecard

Use this reference when Dispatch, Review, or Reconcile needs gate, scorecard, architecture-health, or technical-debt judgment.

## Core Meaning

Phase gates prevent expansion work from building on unstable foundations.

Scorecard dimensions measure demonstrated capability against the user's intended outcome and a reasonable external/productized standard. They are not praise, effort, confidence, or mood.

## Gate Rules

### G1. Blueprint Defines Gates

`tasks/T000-blueprint.md` must define phase gates before broad task dispatch starts. Each gate needs pass criteria that can be evidenced.

### G2. Gate Before Dispatch

Every dispatch declares:

- **Task type**: `convergence` or `expansion`
- **Blocked by**: gate IDs required before active dispatch
- **If blocked**: backlog, not active

Expansion tasks must not be dispatched as active unless all blocked-by gates are `passed`.

Convergence tasks may be dispatched to repair, validate, connect, or unblock gates that are `locked`, `failed`, or `in-progress`.

### G3. Score Blocks Expansion

For any evaluation dimension below the project threshold, default `60/100`:

- Allowed: convergence tasks that repair, tighten, or validate the dimension
- Blocked: expansion tasks that add capability in that dimension

If the project has no T000 or scorecard, do not estimate scores from vibes. Treat the score threshold as unavailable governance evidence. For Dispatch, use explicit ACs, board state, gate evidence, and user goals as a temporary readiness check, and note that a scorecard should be created or backfilled before broad expansion work.

### G4. End-to-End Validation

Any task touching output layer, generator, data model, or cross-module contract must include end-to-end validation in ACs.

Valid evidence may include:

- Full pipeline run
- Regression test
- Schema contract check
- AI simulation
- User validation
- Screenshot or artifact review when visual/user-facing output is the true surface

The gate cannot be marked `passed` until this validation is evidenced in the report and reviewed.

### G5. Task Done Is Not Gate Passed

Task AC completion means the task is done.

Gate pass means the stage is stable enough to build the next stage on top of it.

A project with many done tasks and no passed gates is still in the earlier stage.

### G6. Architecture Health Gate

Code-changing tasks must answer:

- Did coupling increase between modules?
- Did cohesion decrease inside any module?
- Did new code smells appear, such as long functions, duplicated logic, boundary leakage, missing guard clauses, hard-coded dependencies, global state, or hidden side effects?
- Did testability degrade?

If architecture health degraded, classify it as strategic debt or accidental debt before accepting the task.

## Typical Phase Lifecycle

| Stage | Purpose | Typical Gates | Exit Condition |
|-------|---------|---------------|----------------|
| Phase 1: Foundation | Architecture, data layer, and core contracts are stable and testable | F1 core modules decoupled; F2 knowledge/state boundaries defined; F3 schema contracts enforced | All F-gates passed |
| Phase 2: Output Convergence | User-facing outputs are coherent and meet quality bar | O1 output surfaces stable; O2 UX validated; O3 no unsupported precision or false claims | All O-gates passed |
| Phase 3: Closed-Loop Validation | Full loop runs end-to-end with feedback | V1 simulation/sandbox run passes; V2 real feedback collected; V3 review-to-adjustment cycle shown | All V-gates passed |
| Phase 4: Expansion | New capabilities, users, platforms, or commercial surfaces | E1 scalability readiness; E2 operational/commercial readiness | Expansion gates passed |

Not every project needs all phases. T000 should define the phases that fit the project.

## Gate States

| State | Meaning | Who Updates |
|-------|---------|-------------|
| `locked` | Criteria undefined or not yet reachable | Architect AI |
| `in-progress` | Criteria defined and work is ongoing | Architect AI or executor when explicitly asked |
| `passed` | All pass criteria are evidenced and reviewed | Architect AI |
| `failed` | Validation attempted and failed | Architect AI |

## Scorecard Rules

- Define 5-9 project-specific dimensions in T000.
- Reuse the same dimensions in the progress board.
- Each dimension must state why it matters, what capability it represents, how evidence is observed, and what target state means.
- Update scores only when evidence shows the artifact moved closer to or further from the standard.
- Keep AI evidence and human review evidence separate.
- Each dispatch should primarily affect 1-3 dimensions.
- If a proposed task affects no dimension and unblocks no dimension, challenge it before dispatching.

Recommended dimensions for code-heavy projects:

- Technical Architecture
- Architecture Health
- Technical Debt
- UX Clarity
- Business Workflow Fit
- Data Quality
- Knowledge Governance
- Reliability
- Delivery Readiness
- Maintainability

Do not reuse this list blindly. Pick dimensions that fit the project.

## Module Boundary Strictness

T000 should tag important modules by volatility:

- **Core subdomain**: competitive advantage or high volatility. Use strict governance: contract coupling only, no cross-layer calls, architecture review on every change.
- **Supporting subdomain**: necessary but not differentiating. Use moderate governance: model coupling may be acceptable.
- **Generic subdomain**: solved problem or off-the-shelf area. Use lightweight governance unless provider switching risk requires strong contracts.

Avoid uniform strictness. Core modules need more discipline than generic plumbing.

## Debt Handling

Distinguish:

- **Strategic debt**: intentional, tracked, with a payback plan.
- **Accidental debt**: unrecognized mess that compounds future work.

Communicate debt in business terms, for example: "This adds about X hours per sprint in workaround cost."

Accidental debt that blocks acceptance should be repaired before the task is marked done. Strategic debt may pass only if it is explicitly tracked in the board or review notes with a payback plan.

## Review Source Rule

AI Evidence can verify implementation correctness, structure, tests, logs, screenshots, diffs, artifact checks, and architecture consistency.

Human Review Evidence is needed for usefulness, workflow fit, trust, taste, market/category fit, and whether the artifact feels real in the intended context.
