# Status Agent Skill

## 目标

当你说"今天开工/新增工作/更新状态"时，自动：

- 扫描任务池（尤其是 active / blocked / draft）
- 结合你新增输入
- 输出今日计划（plan）
- 必要时把少数任务推进为 active（但要克制）

## 输入

- 触发词：
  - `start`：今天正式开工
  - `add`：新增工作（附一句话）
  - `update`：我刚完成/推进了某任务（附说明）
- 可选：今日主目标一句话（你回答 Strategy Agent 的结果也可直接输入）

## 扫描范围（本地文件）

- `20_Tasks/` 下：
  - status=active 的任务
  - status=blocked 的任务
  - status=draft 且 priority=P0/P1 的任务（可选抽样）
- 允许读取最近 3 天 `10_Daily/*_review.md`（用于连续性）

## 输出

- 目录：`10_Daily/<YYYY>/`
- 文件名：`YYYY-MM-DD_plan.md`
- YAML：

```yaml
---
type: plan
status: active
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [daily]
---
```

## 正文结构（固定）

```markdown
# Plan - YYYY-MM-DD

## Today Main Objective（今日主线）
- ...

## Active Focus（最多3个）
1. [[TASK_xxx]] - 为什么今天必须推进
2. ...
3. ...

## New Inputs（今日新增）
- ...

## Execution Blocks（时间块建议）
- 09:30-11:00：...
- 11:00-12:00：...
- 14:00-16:00：...
- 16:00-17:30：...

## Risks / Blockers
- ...

## Ask（需要你回答的1-3个问题）
1. ...
```

## 约束

- Active Focus **最多 3 个**（硬规则）
- 如果今天出现 P0，只能 1 个
- "Ask" 必须精炼（最多 3 问）

## CLI 用法

```
/start main:"今天主线一句话"
/add <新增工作描述>
/update <完成/推进说明>
```
