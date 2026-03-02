---
name: update
description: 更新进度快捷入口，等价于 status skill 的 /update 行为。Use when user says "/update", "更新进度", or wants to record progress updates.
---

# Update Skill

`/update` 是 `status` skill 的快捷别名入口。

## Behavior

1. 接收完成/推进说明
2. 更新 `30_Tasks/` 对应任务状态与进展
3. 更新 `10_Daily/YYYY/YYYY-MM-DD_plan.md`

## Notes

- 输出结构与 `status` skill 保持一致
- 约束保持一致：Active Focus <= 3，P0 <= 1
