---
name: add
description: 新增工作快捷入口，等价于 status skill 的 /add 行为。Use when user says "/add", "新增工作", or wants to append work into today's plan.
---

# Add Skill

`/add` 是 `status` skill 的快捷别名入口。

## Behavior

1. 接收新增工作描述
2. 在 `30_Tasks/` 创建或补充任务项
3. 更新 `10_Daily/YYYY/YYYY-MM-DD_plan.md` 的 New Inputs/Active Focus

## Notes

- 输出结构与 `status` skill 保持一致
- 约束保持一致：Active Focus <= 3，P0 <= 1
