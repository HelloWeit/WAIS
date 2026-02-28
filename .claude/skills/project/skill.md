---
name: project
description: 将想法或 Inbox 笔记转换为结构化的项目笔记，创建项目计划和初始任务。Use when user says "/project", "新建项目", "创建项目", or wants to start a new project.
---

# Project Skill

将想法或 Inbox 笔记转换为结构化的项目笔记。

## When to Use

- 用户说 "/project", "新建项目", "创建项目"
- 需要将想法转化为正式项目
- 从 Inbox 中提取项目并初始化

## Input

| Field | Required | Description |
|-------|----------|-------------|
| source | No | Inbox 文件路径或内联描述 |

## Output

```
30_Projects/
└── <ProjectName>.md

20_Tasks/
└── TASK_*.md  (初始任务)
```

## Workflow

1. **收集上下文**
   - 如果指定了 source，读取 Inbox 文件
   - 否则询问用户项目描述

2. **创建项目计划**
   - 使用 C.A.P. 结构
   - 定义目标和里程碑

3. **用户确认**
   - 展示项目计划
   - 征求用户确认

4. **创建项目笔记**
   - 生成项目文件
   - 创建初始任务

5. **后续处理**
   - 归档源 Inbox 文件（如适用）
   - 更新相关链接

## C.A.P. Structure

| Section | Content |
|---------|---------|
| **C**ontext | 项目背景和目标 |
| **A**ctions | 关键行动和任务 |
| **P**rogress | 进度跟踪 |

## Template

```markdown
---
type: project
status: active
priority: P1
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
strategy: [[STRATEGY_xxx]]
---

# ProjectName

## Context
<!-- 项目背景和目标 -->

## Goals
- [ ] Goal 1
- [ ] Goal 2

## Actions
- [ ] Task 1 → [[TASK_xxx]]
- [ ] Task 2 → [[TASK_xxx]]

## Progress
<!-- 进度跟踪 -->

## Notes
<!-- 项目笔记 -->
```

## Constraints

- 先检查项目是否已存在（避免重复）
- 使用 C.A.P. 结构组织
- 项目通过 frontmatter 链接战略方向
- 初始任务不超过 5 个
