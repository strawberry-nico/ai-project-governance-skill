# AI Project Governance Skill

> English below each Chinese section.

一套给 AI Agent 使用的项目治理规则，用来防止多轮任务、报告、验收和交接之后，项目慢慢跑偏。

A project-governance protocol for AI agents. It helps keep long-running agentic projects aligned across task files, reports, reviews, and handoffs.

## 这个 Skill 解决什么问题

很多 AI 项目不是死在“不会写代码”，而是死在“越做越散”：

- Agent 一直在干活，但没人知道项目是否还在原目标上。
- report 写得很乐观，但没有真实验收证据。
- progress board 看起来在推进，其实已经和代码/产物脱节。
- 当前任务没做完，Agent 又开始派发新任务。
- 基础还不稳，就开始扩展新功能。
- 多个 Agent 接力后，边界、任务状态、验收标准都变模糊。

这个 skill 的目标不是让 Agent 多写文档，而是让 Agent 在关键节点先判断：

- 当前任务到底做完了吗？
- 证据够不够？
- 是否应该先纠偏，而不是继续派新任务？
- 现在能不能进入下一阶段？
- 项目状态文件是不是还描述真实情况？

Many AI projects do not fail because agents cannot code. They fail because the project slowly loses alignment:

- work continues, but nobody knows whether it still serves the original goal
- reports sound confident without real acceptance evidence
- progress boards drift away from code and artifacts
- new tasks are dispatched before current work is accepted
- unstable foundations get expanded too early
- handoffs between agents blur scope, status, and acceptance criteria

This skill gives agents a file-backed operating protocol for those moments.

## 适合谁用

适合你，如果你：

- 用 AI Agent / Codex / Claude Code / 其他 coding agent 做项目
- 会把任务拆成 task 文件、report、review、progress board
- 需要一个 Agent 做架构/验收，另一个 Agent 做执行
- 关心 AC、证据、阶段门、项目状态，而不只是“Agent 说完成了”
- 经常遇到 Agent 没修完当前问题就开始做新东西
- 想让项目先收敛，再扩展

不适合：

- 一次性小改动
- 简单问答
- 不需要文件化验收的临时任务

Use this if you:

- run projects with AI agents, Codex, Claude Code, or other coding agents
- split work into task files, reports, reviews, and progress boards
- want one agent to act as architect/reviewer while another executes
- care about acceptance criteria, evidence, gates, and project state
- have seen agents create new work instead of fixing current drift
- want convergence before expansion

This is overkill for one-off edits or simple Q&A.

## 核心机制

这个 skill 把 Agent 工作分成三种模式：

| 模式 / Mode | 什么时候用 / When | Agent 应该做什么 / What The Agent Does |
|-------------|-------------------|-----------------------------------------|
| **Review / 验收** | review report, 验收, 复查, update progress-board | 检查 AC、证据、gate、score、board 是否真实 |
| **Reconcile / 纠偏** | check drift, 有没有跑偏, 补齐没做好 | 优先修复当前范围内的 drift，不默认派新任务 |
| **Dispatch / 派发** | dispatch next task, 派发任务, 拆任务 | 写清楚边界、AC、验证方法、owner、执行顺序 |

如果用户意图不清楚，默认走最保守路径：

```text
Review > Reconcile > Dispatch
```

也就是说：能先验收，就不要先派发；能先纠偏，就不要新开任务。

The skill routes work into three modes:

- **Review**: evaluate evidence and status
- **Reconcile**: repair in-scope drift before creating new work
- **Dispatch**: create a bounded task handoff only when allowed

If intent is ambiguous, the least expansive path wins:

```text
Review > Reconcile > Dispatch
```

## 最重要的判断

这个 skill 强行区分三件事：

- **Task done**：这个任务的 AC 是否完成。
- **Gate passed**：项目是否稳定到可以进入下一阶段。
- **Score improved**：有证据表明某项能力真的变强。

一个任务可以完成，但 gate 仍然不通过。

一个项目可以有很多 task 文件，但仍然不能扩展。

这是这个 skill 的核心价值。

The skill separates three things agents often mix together:

- **Task done**: acceptance criteria are satisfied.
- **Gate passed**: the project stage is stable enough to build on.
- **Score improved**: evidence shows a capability moved closer to the intended standard.

A task can be done while a gate still fails.

A project can have many task files and still be stuck in the foundation stage.

## 通用安装 / 给任何 Agent 使用

这个仓库本质上是一组规则文件，不绑定某一个 Agent。

如果你的 Agent 支持自定义 skills / rules / instructions：

1. 下载或 clone 这个仓库。
2. 让 Agent 把 `SKILL.md` 当作入口规则。
3. 当进入某个模式时，让 Agent 读取对应 reference：
   - `references/review-mode.md`
   - `references/reconcile-mode.md`
   - `references/dispatch-mode.md`
4. 当需要创建文件时，使用 `assets/` 里的模板。

最小提示词：

```text
Use the ai-project-governance rules in SKILL.md.
First decide whether this is Review, Reconcile, or Dispatch.
Then load the matching reference file before acting.
Do not invent missing project state.
```

This repository is a set of agent rules. It is not tied to one runtime.

For any agent system that supports custom instructions, skills, or rule files:

1. Clone or download this repository.
2. Use `SKILL.md` as the entrypoint instruction.
3. Load the matching reference file after choosing a mode.
4. Use templates from `assets/` when creating project artifacts.

## Codex 安装方式

如果你使用 Codex skills，可以 clone 到本地 skills 目录：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/strawberry-nico/ai-project-governance-skill.git ~/.codex/skills/ai-project-governance
```

然后重启 Codex，或按你的环境重新加载 skills。

For Codex skills:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/strawberry-nico/ai-project-governance-skill.git ~/.codex/skills/ai-project-governance
```

Then restart Codex or reload skills if needed.

## 快速使用

在项目里可以这样问：

```text
使用 ai-project-governance 验收 tasks/T012.md，并更新 progress-board。
```

```text
使用 ai-project-governance 检查 T012 有没有跑偏，先纠偏，不要派新任务。
```

```text
Use ai-project-governance to dispatch the next task based on T000 and progress-board.
```

Agent 应该读取项目事实，例如：

- `AGENTS.md`
- `README.md`
- `tasks/T000-blueprint.md`
- `tasks/progress-board.md`
- 当前 `tasks/Txxx.md`
- report、测试日志、截图、schema、产物等证据

文件不存在就跳过，不能脑补项目状态。

In a project, ask:

```text
Use ai-project-governance to review tasks/T012.md and update the progress board.
```

The agent should read project facts when they exist and skip missing files instead of inventing state.

## 项目里会用到哪些文件

推荐项目里有这些文件：

| 文件 / File | 用途 / Purpose |
|-------------|----------------|
| `tasks/T000-blueprint.md` | 项目边界、scorecard、phase gates、任务拆解 |
| `tasks/Txxx.md` | 单个执行任务，包含 Dispatch / Report / Architect Review |
| `tasks/progress-board.md` | 当前阶段、任务状态、gate、score、blocker、下一步 |

不是第一天就必须全部有。

如果缺少这些文件，Agent 应该说明缺什么，而不是自己编。

Recommended project files:

- `tasks/T000-blueprint.md`
- `tasks/Txxx.md`
- `tasks/progress-board.md`

Missing files should be reported as missing baseline, not fabricated.

## 任务文件长什么样

新任务推荐一个文件：

```text
tasks/T013.md
```

包含三段：

```markdown
## Dispatch
架构/调度方写：目标、范围、AC、验证、允许文件、禁止文件、owner、顺序。

## Report
执行方写：改了什么、AC 完成情况、验证结果、blocker。

## Architect Review
验收方写：accepted / needs reconcile / needs new dispatch / blocked。
```

已有项目可以保留旧格式。

这个 skill 会读取并维护已有混合格式，不会为了格式好看强制迁移历史任务。

New tasks use one file with:

- `## Dispatch`
- `## Report`
- `## Architect Review`

Existing projects can keep older or mixed task formats.

## 三个典型场景

### 1. Review / 验收

用户：

```text
验收 T012，更新 progress-board。
```

Agent：

- 检查每个 AC 是否有证据
- 检查 report 是否只是口头说完成
- 检查 gate / score / board 是否需要更新
- 如果证据不足，返回 `Needs reconcile`
- 不默认创建新任务

### 2. Reconcile / 纠偏

用户：

```text
T012 是不是跑偏了？先纠偏，不要派新任务。
```

Agent：

- 先分类 drift
- 只修当前任务范围内的问题
- 可以修和当前 drift 直接相关的 board/report 错误
- 不顺手做跨文件 cleanup
- 新范围必须停下来问

### 3. Dispatch / 派发

用户：

```text
根据当前进度派发下一个任务。
```

Agent：

- 检查当前 phase、gate、board、依赖、owner、执行顺序
- 如果基础不稳，不能派 expansion
- 可以派 convergence 任务来修 gate
- 只在允许时写 `tasks/Txxx.md`

## 防止哪些问题

这个 skill 主要防止：

- 当前任务没完成就派新任务
- 把 report 当成证据
- 没有验证就让 gate passed
- 基础不稳就扩展功能
- progress-board 变成“看起来很忙”的假状态
- 实现代码和治理记录混在一起
- 静默复活旧入口、旧字段、旧脚本
- 没有 scorecard 却编分数

It tries to prevent:

- dispatching new work before current work is accepted
- treating reports as evidence
- passing gates without validation
- expanding unstable features
- stale progress boards
- hidden legacy resurrection
- invented scorecard numbers

## 仓库结构

```text
.
├── SKILL.md
├── README.md
├── assets/
│   ├── project-blueprint-template.md
│   ├── task-dispatch-template.md
│   ├── lightweight-task-template.md
│   ├── execution-report-template.md
│   └── progress-board-template.md
└── references/
    ├── dispatch-mode.md
    ├── reconcile-mode.md
    ├── review-mode.md
    ├── gates-scorecard.md
    ├── document-maintenance.md
    └── example-workflow.md
```

## 设计说明

`SKILL.md` 故意保持较短，只负责触发、路由和硬规则。

详细规则放在 `references/`，需要时再读，减少上下文占用。

模板放在 `assets/`，只有创建项目文件时才用。

`SKILL.md` is intentionally short. It routes the task and points the agent to the right reference file.

Detailed rules live in `references/`.

Templates live in `assets/`.

## 从 ai-task-bridge 迁移

旧的 `T012-dispatch.md` / `T012-report.md` 仍然可以读。

新任务建议：

1. 在 `tasks/T000-blueprint.md` 里补 phase gates。
2. 在 progress board 里补 gate status 和 scorecard。
3. 新任务使用单文件 `tasks/Txxx.md`。
4. 不要为了迁移而重做旧任务，除非当前 gate 需要旧证据。

Existing split files such as `T012-dispatch.md` and `T012-report.md` remain readable.

For new work, prefer single-file `tasks/Txxx.md` with phase gates and progress-board evidence.
