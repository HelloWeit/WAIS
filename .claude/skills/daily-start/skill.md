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

## Initialization

首次启动时，Agent 会自动检测目录结构：

| 检测项 | 行为 |
|--------|------|
| 目录已存在（git clone 后） | 直接扫描内容，不重复创建 |
| 目录不存在 | 创建必要的目录结构 |
| 目录为空（只有 .gitkeep） | 正常启动，显示"暂无活跃任务" |

**核心目录：**
- `00_Inbox/` - 想法缓冲区
- `10_Daily/YYYY/` - 每日笔记
- `20_Tasks/` - 任务池
- `30_Projects/` - 项目
- `70_Strategy/` - 战略

## Workflow

### Step 1: 收集简报信息

1. **检查缓存**: `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`
2. **获取 RSS**: 按优先级抓取 AI/GovTech/BigTech 动态
3. **扫描状态**: 检查任务、项目、战略文件

### Step 2: 战略问答

使用 AskUserQuestion 工具进行 3 个问题。**重要：** 必须提供明确的 options 数组，用户可通过 "Other" 选项自由输入。

**问题 1：今日战略重点**
```json
{
  "question": "今天最重要的战略/技术决策或关注点是什么？",
  "header": "战略重点",
  "options": [
    {"label": "架构设计/评审", "description": "系统架构相关的设计或评审工作"},
    {"label": "技术选型/决策", "description": "技术栈、工具或方案的选择"},
    {"label": "团队/资源协调", "description": "人员、资源相关的协调工作"},
    {"label": "项目进度跟进", "description": "重点项目的进度推进"}
  ],
  "multiSelect": false
}
```

**问题 2：团队/项目事项**
```json
{
  "question": "有哪些需要关注的团队或项目事项？",
  "header": "团队事项",
  "options": [
    {"label": "无特别事项", "description": "今天没有特别的团队事项"},
    {"label": "团队1:1/会议", "description": "有一对一或团队会议"},
    {"label": "跨部门协调", "description": "需要与其他部门协作"},
    {"label": "项目风险处理", "description": "有项目风险需要处理"}
  ],
  "multiSelect": true
}
```

**问题 3：新想法/灵感**
```json
{
  "question": "有什么新的想法、灵感或发现的机会？",
  "header": "新想法",
  "options": [
    {"label": "暂时没有", "description": "今天没有新的想法"},
    {"label": "有想法要记录", "description": "有新想法需要记录到 Inbox"}
  ],
  "multiSelect": false
}
```

> **注意：** 用户选择 "Other" 可以自由输入文字。如果问题3选择了"有想法要记录"或在Other中输入了内容，必须保存到 Inbox。

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
