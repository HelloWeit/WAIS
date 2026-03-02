---
name: start
description: 今日开工快捷入口，等价于 status skill 的 /start 行为。Use when user says "/start", "开始今天工作", or wants to start the day plan.
---

# Start Skill

`/start` 是 `status` skill 的快捷别名入口。

## Behavior

1. 扫描 `30_Tasks/` 中 active/blocked/draft(P0/P1) 任务
2. 读取最近 3 天 `10_Daily/` review
3. 生成/更新 `10_Daily/YYYY/YYYY-MM-DD_plan.md`

## Notes

- 输出结构与 `status` skill 保持一致
- 约束保持一致：Active Focus <= 3，P0 <= 1
