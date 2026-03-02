---
name: status
description: 扫描任务池生成今日计划，管理任务状态和优先级。Use when user says "/start", "/add", "/update", "今天开工", "新增工作", or wants to manage daily tasks.
---

# Status Skill

扫描任务池，生成今日计划，管理任务状态。

## When to Use

- 用户说 "/start", "/add", "/update"
- 用户说 "今天开工", "新增工作"
- 需要查看或更新任务状态

## Input

| Field | Required | Description |
|-------|----------|-------------|
| main | No | 今日主线目标 |
| new | No | 新增工作描述 |
| update | No | 完成或推进说明 |

## Output

```
10_Daily/YYYY/
└── YYYY-MM-DD_plan.md
```

## Directory Detection

执行前会检测必要目录：

- 如果 `10_Daily/YYYY/` 不存在，自动创建
- 如果 `20_Tasks/` 不存在，自动创建
- 不覆盖已有内容，只做增量操作

## Scan Directories

| Directory | Filter |
|-----------|--------|
| `20_Tasks/` | status: active, blocked, draft (P0/P1) |
| `10_Daily/` | 最近 3 天 review |

## Workflow

### /start - 开始今日工作
1. 扫描活跃任务
2. 识别 P0/P1 任务
3. 生成今日计划

### /add - 新增工作
1. 创建新任务
2. 设置优先级
3. 更新今日计划

### /update - 更新进度
1. 更新任务状态
2. 记录进度说明
3. 更新计划文件

## Template

```markdown
---
type: plan
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [daily]
---

# Plan YYYY-MM-DD

## Main Focus
<!-- 今日主线目标 -->

## Active Focus (max 3)
1. [[TASK_xxx]] - Task 1
2. [[TASK_xxx]] - Task 2
3. [[TASK_xxx]] - Task 3

## P0 (max 1)
- [[TASK_xxx]] - Critical Task

## P1 Tasks
- [[TASK_xxx]] - Task A
- [[TASK_xxx]] - Task B

## Pending
<!-- 等待中的任务 -->

## Notes
<!-- 今日笔记 -->
```

## Constraints

- Active Focus 最多 3 个
- P0 最多 1 个
- Ask 最多 3 问（保持简洁）

## Task Status Flow

```
draft → active → blocked → done → archived
```
