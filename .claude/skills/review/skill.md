---
name: review
description: 总结今日完成情况，更新任务状态，提取改进点和学习心得。Use when user says "/review", "复盘", "今日总结", or wants to do a daily review.
---

# Review Skill

每日复盘工具，总结完成情况，更新状态，提取学习心得。

## When to Use

- 用户说 "/review", "复盘", "今日总结"
- 一天工作结束需要回顾
- 需要更新任务状态

## Input

| Field | Required | Description |
|-------|----------|-------------|
| done | No | 完成的任务列表 |
| blocked | No | 阻塞的任务 |
| new | No | 新增事项 |

## Output

```
10_Daily/YYYY/
└── YYYY-MM-DD_review.md
```

## Workflow

1. **扫描今日工作**
   - 读取今日计划
   - 检查任务状态变化

2. **收集反馈**
   - 询问完成情况
   - 记录阻塞问题

3. **更新状态**
   - 更新任务 frontmatter
   - 记录进度

4. **提取学习**
   - 总结今日收获
   - 识别改进点

## Template

```markdown
---
type: review
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [daily]
---

# Review YYYY-MM-DD

## 完成事项
- [x] Task 1
- [x] Task 2

## 进行中
- [ ] Task 3 (进度: 50%)

## 阻塞
- [ ] Task 4 - 阻塞原因: xxx

## 新增
- Task 5

## Learnings
1. <!-- 学习心得 1 -->
2. <!-- 学习心得 2 -->

## 改进点
- <!-- 改进建议 -->

## 明日关注
- <!-- 明天需要关注的点 -->
```

## Constraints

- **禁止新增任务**（只更新状态）
- 必须更新相关任务状态
- 提取至少 1 条 Learning
- 记录所有阻塞问题

## Best Practice

每日结束前运行 `/review`，保持任务状态同步。
