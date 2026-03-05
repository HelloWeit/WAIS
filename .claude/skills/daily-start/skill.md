---
name: daily-start
description: 技术管理者一键启动每日工作流，收集简报、进行主题问答并生成今日计划。Use when user says "/daily-start", "/start-day", "每日启动", "开工", or wants to start their work day.
---

# Daily-Start Skill

技术管理者专用的每日启动工作流，一键完成简报收集、主题问答和计划生成。

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
- `30_Tasks/` - 任务池
- `20_Projects/` - 项目
- `70_Strategy/` - 战略

## Workflow

### Step 1: 收集简报信息

1. **检查缓存**: `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`
2. **启动 RSS 子代理（推荐）**: 子代理仅负责 RSS 抓取、去重、摘要与落盘 digest
3. **主代理扫描状态**: 检查任务、项目、战略文件

缓存处理要求：
- 若当天 digest 缓存存在：直接复用缓存内容生成 brief
- 若当天 digest 缓存不存在：必须先生成并写入缓存，再生成 brief
- `/daily-start` 结束时，`10_Daily/YYYY-MM-DD_brief.md` 与 `60_Resources/.../YYYY-MM-DD-digest.md` 必须同时存在

#### RSS 子代理职责（强制边界）

- 子代理输入：RSS 源配置、时间窗口（过去 24 小时）、分类配额（AI TOP10 等）
- 子代理输出：`60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`
- 子代理只做信息收集与结构化摘要，不做任务创建、不改状态、不生成今日计划
- 主代理只读取 digest 结果进入后续问答与计划生成
- 若子代理失败：主代理回退为本地简化抓取，并在 brief 标注“RSS 部分降级”

### Step 2: 主题问答

使用 AskUserQuestion 工具进行 3 个问题，围绕“今日主题、关键推进、增量输入”展开。**重要：** 必须提供明确的 options 数组，用户可通过 "Other" 选项自由输入。

- 问题 1/2 的 options 不能只用固定模板，必须结合 Step 1 的扫描结果动态生成候选。
- 候选必须优先参考前一日工作：昨日未完成（carryover）、blocked 任务、3 天+未更新项目。
- 采用**两阶段问答**：
  1) 先连续完成问题 1/2/3（不打断）；
  2) 再统一进行追问，只追问问题 2（任务）和问题 3（想法/外部变化）的已选项。

**问题 1：今日主题（可被 focus 覆盖，多选）**
```json
{
  "question": "今天的主线主题是什么？",
  "header": "今日主题",
  "options": [
    {"label": "架构设计与技术决策", "description": "聚焦架构评审、技术方案与关键决策"},
    {"label": "核心项目交付推进", "description": "聚焦里程碑、路径拆解与进度推进"},
    {"label": "团队协同与资源协调", "description": "聚焦跨团队协作、人力与会议对齐"},
    {"label": "稳定性治理与风险处置", "description": "聚焦故障、技术债、质量与风险处理"}
  ],
  "multiSelect": true
}
```

**问题 2：今日关键推进事项（多选）**
```json
{
  "question": "今天必须推进或明确的关键事项有哪些？",
  "header": "关键事项",
  "options": [
    {"label": "项目里程碑推进", "description": "明确里程碑、负责人和完成标准"},
    {"label": "跨团队依赖协调", "description": "处理上下游依赖、排期和接口协作"},
    {"label": "关键会议/沟通", "description": "需要完成关键对齐、评审或决策沟通"},
    {"label": "风险/阻塞处理", "description": "处理延期风险、技术阻塞或资源冲突"},
    {"label": "无特别事项", "description": "今天没有新增关键事项"}
  ],
  "multiSelect": true
}
```

问题 2 的追问统一放在问题 1/2/3 完成后进行，采集每个已选项的具体内容（不能只保留标签）。

- 若选择“关键会议/沟通”，追问并记录：
  - 会议/沟通名称
  - 开始时间-结束时间（如 `10:30-11:00`）
  - 简要主题或目标（1 句话）
- 若选择“项目里程碑推进”，追问并记录：项目名、今日要推进到的节点、负责人。
- 若选择“跨团队依赖协调”，追问并记录：协作方、依赖事项、期望完成时间。
- 若选择“风险/阻塞处理”，追问并记录：风险点/阻塞点、影响范围、预期解决动作。

**问题 3：新输入（想法/机会/外部变化）**
```json
{
  "question": "今天是否有新的想法、机会或需要跟踪的外部变化？",
  "header": "新输入",
  "options": [
    {"label": "暂时没有", "description": "今天没有新增输入"},
    {"label": "有想法/机会要记录", "description": "有可行动的想法或机会需要进入 Inbox"},
    {"label": "有外部变化需跟踪", "description": "有政策、供应商或行业变化需要记录"}
  ],
  "multiSelect": false
}
```

问题 3 的追问统一放在问题 1/2/3 完成后进行，采集可落盘的具体信息（不能只保留标签）。

- 若选择“有想法/机会要记录”，追问并记录：
  - 想法/机会标题（短标题）
  - 核心内容（1-3 句话）
  - 建议下一步（转任务/转项目/转研究/暂存）
- 若选择“有外部变化需跟踪”，追问并记录：
  - 变化来源（政策/供应商/行业/竞品）
  - 变化要点（1-3 条）
  - 可能影响（对当前任务/项目的影响）
  - 跟踪动作与时间点（何时复查）

> **注意：** 用户选择 "Other" 可以自由输入文字。如果问题3选择了"有想法/机会要记录"、"有外部变化需跟踪"或在 Other 中输入了内容，必须保存到 Inbox。

#### 追问执行顺序（强制）

1. 先问完问题 1（主题）→ 问题 2（关键事项）→ 问题 3（新输入）
2. 再进入任务追问（基于问题 2 的选择）
3. 最后进入想法/变化追问（基于问题 3 的选择）

这样可避免中途打断，保证先定主题与任务全貌，再补充细节。

### Step 3: 生成计划 + 捕获想法

- 生成今日简报文件（`YYYY-MM-DD_brief.md`）
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

See `../morning/references/rss-sources.md` for complete RSS configuration.

### Quick Reference

| Category | Priority | Limit |
|----------|----------|-------|
| AI | P0 > P1 > P2 | TOP 10 |
| GovTech | - | TOP 3 |
| BigTech | P1 > P2 | TOP 5 |
| 互联网资讯 | P1 > P2 | TOP 5 |
| 奇思妙想 | P2 | TOP 3 |
| 技术团队与安全 | P1 | TOP 4 |
| 产品与架构 | P2 | TOP 2 |

Time Window: Past 24 hours only.

## Scan Directories

| Directory | Filter |
|-----------|--------|
| `30_Tasks/` | status: active |
| `20_Projects/` | status: active, 标记3天+未更新 |
| `70_Strategy/` | 战略方向文件 |
| `00_Inbox/` | status: pending |
| `10_Daily/` | 昨日笔记 |

## Optional Input

- `focus`: 指定今日主题（仅跳过问题1，问题2/3仍执行）
- `quick`: 快速模式（简化输出）

## Constraints

- 所有新想法必须保存到 Inbox
- 执行重点最多 3 个
- P0 任务最多 1 个
- 陈旧项目需要标记提醒
- 问题 1/2 必须参考前一日工作情况生成候选（固定选项仅作兜底）
- RSS 收集优先由子代理完成，主代理负责编排与消费结果

## Principles

- 想法 → Inbox → 后续处理
- 不直接创建任务/项目
- 保持工作流一致性
