---
name: daily-start
description: 技术管理者一键启动每日工作流，收集简报、进行战略问答并生成今日计划。Use when user says "/daily-start", "/start-day", "每日启动", "开工", or wants to start their work day.
---

# Daily-Start Skill

技术管理者专用的每日启动工作流，一键完成简报收集、战略问答和计划生成。

## When to Use

- 用户说 "/daily-start", "/start-day", "每日启动", "开工"
- 每日开始工作时
- 需要快速进入工作状态

## User Role

- 架构师
- 技术经理
- 技术专家
- 技术团队负责人

## Workflow

### Step 1: 收集简报信息

1. **检查缓存**: `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`
2. **获取 RSS**: 按优先级抓取 AI/GovTech/BigTech 动态
3. **扫描状态**: 检查任务、项目、战略文件

### Step 2: 战略问答

使用 AskUserQuestion 工具进行 3 个问题：

| # | Question | Purpose |
|---|----------|---------|
| 1 | 今天战略/技术决策的重点是什么？ | 明确主线 |
| 2 | 有什么团队/项目事项需要关注？ | 团队同步 |
| 3 | 有什么新想法或灵感？ | 捕获想法 → Inbox |

### Step 3: 生成计划 + 捕获想法

- 生成今日计划文件
- 新想法保存到 Inbox

## Output Files

```
10_Daily/YYYY/
├── YYYY-MM-DD_brief.md    # 晨间简报
└── YYYY-MM-DD_plan.md     # 今日计划

00_Inbox/
└── IDEA_*.md              # 新想法（如有）
```

## RSS Sources

See `references/rss-sources.md` for complete RSS configuration.

### Quick Reference

| Category | Priority | Limit |
|----------|----------|-------|
| AI | P0 > P1 > P2 | TOP 10 |
| GovTech | - | TOP 3 |
| BigTech | P1 > P2 | TOP 5 |

## Scan Directories

| Directory | Filter |
|-----------|--------|
| `20_Tasks/` | status: active |
| `30_Projects/` | status: active, 标记3天+未更新 |
| `70_Strategy/` | 战略方向文件 |
| `00_Inbox/` | status: pending |
| `10_Daily/` | 昨日笔记 |

## Optional Input

- `focus`: 指定战略重点（跳过问答）
- `quick`: 快速模式（简化输出）

## Constraints

- 所有新想法必须保存到 Inbox
- 执行重点最多 3 个
- P0 任务最多 1 个
- 陈旧项目需要标记提醒

## Principles

- 想法 → Inbox → 后续处理
- 不直接创建任务/项目
- 保持工作流一致性
