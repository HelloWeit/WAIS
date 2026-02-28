---
name: task
description: 将想法转换为标准任务文件，设置优先级和下一步行动。Use when user says "/task", "创建任务", "新任务", or wants to create a new task.
---

# Task Skill

将想法转换为标准任务文件。

## When to Use

- 用户说 "/task", "创建任务", "新任务"
- 需要将想法或工作项转化为任务
- 从 Inbox 中提取任务

## Input

| Field | Required | Description |
|-------|----------|-------------|
| description | Yes | 任务一句话描述 |
| source | No | 来源 (brief/meeting/inbox/manual) |
| project | No | 关联项目 |
| priority | No | 优先级 (P0/P1/P2) |
| due | No | 截止日期 |

## Output

```
20_Tasks/
└── TASK_YYYYMMDD_短标题.md
```

## Workflow

1. **收集任务信息**
   - 任务描述
   - 优先级
   - 关联项目
   - 截止日期

2. **创建任务文件**
   - 使用任务模板
   - 生成 Next Actions

3. **更新关联**
   - 如有项目，更新项目任务列表

## Template

```markdown
---
type: task
status: draft
priority: P1
source: [brief/meeting/inbox/manual]
project: [[ProjectName]]
created: YYYY-MM-DD
updated: YYYY-MM-DD
due: YYYY-MM-DD
tags: [tag1, tag2]
---

# TASK_YYYYMMDD_短标题

## Description
<!-- 任务一句话描述 -->

## Context
<!-- 任务背景 -->

## Next Actions
- [ ] Action 1
- [ ] Action 2

## Notes
<!-- 任务笔记 -->

## Related
- Project: [[ProjectName]]
- Strategy: [[STRATEGY_xxx]]
```

## Priority Levels

| Priority | Description | Limit |
|----------|-------------|-------|
| P0 | 紧急且重要 | 最多 1 个 |
| P1 | 重要不紧急 | - |
| P2 | 一般优先级 | - |

## Status Flow

```
draft → active → blocked → done → archived
                    ↓
                  cancelled
```

## Constraints

- 不允许把任务写成长文章
- 不允许同时创建项目
- 必须给出至少 1 条 Next Actions
- P0 任务需要特别说明紧急原因

## Best Practice

从 Inbox 中提取任务，确保任务来源清晰。
