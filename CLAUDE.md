# WIS - Work Intelligence Station

> 一个结构化的个人工作环境，通过 Agent Skills 辅助日常任务管理、信息收集和知识沉淀。

## 项目概述

WIS 是一个由 Agent Skills 驱动的个人工作站，结合 Obsidian 进行文件管理和可视化。

**它能帮你：**
- 管理每日任务和项目
- 收集和整理信息
- 沉淀可复用的知识
- 保持工作节奏（计划-执行-复盘）

**它不是：** 笔记工具、ToDo 管理器、新闻聚合器

---

## 目录结构

```
paios/
├── .claude/
│   └── skills/                      # Agent Skills
│       ├── ask/                     # 快速问答
│       ├── archive/                 # 归档
│       │   └── references/
│       ├── brainstorm/              # 头脑风暴
│       │   └── references/
│       ├── daily-start/             # 每日启动
│       │   └── references/
│       ├── knowledge/               # 知识沉淀
│       ├── morning/                 # 晨间简报
│       │   └── references/
│       ├── project/                 # 项目创建
│       │   └── references/
│       ├── research/                # 深度研究
│       ├── review/                  # 每日复盘
│       ├── status/                  # 状态管理
│       │   └── references/
│       ├── strategy/                # 战略判断
│       └── task/                    # 任务创建
│           └── references/
├── 00_Inbox/                        # 输入缓冲区（48h必须处理）
├── 10_Daily/                        # 每日文件
│   └── YYYY/
│       ├── YYYY-MM-DD_brief.md      # Morning Brief
│       ├── YYYY-MM-DD_plan.md       # 今日计划
│       └── YYYY-MM-DD_review.md     # 今日复盘
├── 20_Tasks/                        # 任务池（核心执行区）
├── 30_Projects/                     # 项目容器
├── 40_Research/                     # 研究输出
├── 50_Knowledge/                    # 知识资产（无时间依赖）
├── 60_Resources/                    # 素材池
├── 70_Strategy/                     # 战略层
├── 80_Opportunities/                # 机会池
├── 90_Archive/                      # 历史沉淀
└── 99_System/                       # 系统内核
    ├── templates/                   # 文件模板
    ├── schemas/                     # YAML Schema
    └── dashboards/                  # Dataview 面板
```

---

## 核心规则

### 任务生命周期

```
draft → active → blocked → done → archived
```

**硬性约束：**
- 同时 active 任务 **≤ 3**
- P0 任务 **≤ 1**
- 7 天未更新自动提醒

### 文件命名规范

| 类型 | 格式 | 示例 |
|------|------|------|
| 任务 | `TASK_YYYYMMDD_短标题.md` | `TASK_20260228_首页设计.md` |
| 研究 | `RESEARCH_主题_YYYYMMDD.md` | `RESEARCH_AI趋势_20260228.md` |
| 知识 | `KNOWLEDGE_主题.md` | `KNOWLEDGE_决策模型.md` |
| 想法 | `IDEA_YYYYMMDD_短标题.md` | `IDEA_20260228_新功能.md` |

### YAML 头部规范

所有文件必须包含：

```yaml
---
type: task | project | research | brief | plan | review | knowledge | strategy | opportunity | idea
status: draft | active | blocked | done | archived | processed
priority: P0 | P1 | P2
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
source: manual | agent | meeting | brief | brainstorm
---
```

---

## Agent Skills 速查

| Skill | 命令 | 职责 | 输出目录 |
|-------|------|------|----------|
| **daily-start** | `/daily-start` | 一键启动（简报+问答+计划） | `10_Daily/YYYY/` |
| **task** | `/task` | 创建任务 | `20_Tasks/` |
| **project** | `/project` | 想法→项目 | `30_Projects/` |
| **status** | `/start` `/add` `/update` | 生成今日计划 | `10_Daily/YYYY/` |
| **morning** | `/morning` `/brief` | 生成晨间简报 | `10_Daily/YYYY/` |
| **review** | `/review` | 复盘总结 | `10_Daily/YYYY/` |
| **research** | `/research` | 深度研究 | `40_Research/` |
| **knowledge** | `/knowledge` | 知识沉淀 | `50_Knowledge/` |
| **strategy** | `/strategy` | 战略判断 | `70_Strategy/` |
| **brainstorm** | `/brainstorm` | 交互式头脑风暴 | `00_Inbox/` |
| **archive** | `/archive` | 归档完成项目 | `90_Archive/` |
| **ask** | `/ask` | 快速问答（无文件） | - |

### Agent 职责边界

| Agent | 职责 | 禁止 |
|-------|------|------|
| Morning | 汇总趋势 | 不生成任务 |
| Task | 创建任务 | 不规划今日 |
| Status | 生成计划 | 不写研究 |
| Strategy | 方向判断 | 不写执行 |
| Research | 深度分析 | 不抽象知识 |
| Knowledge | 抽象模型 | 不写时间线 |
| Review | 复盘总结 | 不新增任务 |
| Brainstorm | 探索想法 | 必须输出到 Inbox |

---

## 每日工作流

```
外部信息
     ↓
Inbox（/brainstorm 输出到这里）
     ↓
Morning Brief (/daily-start 或 /morning)
     ↓
Opportunity
     ↓
Task (/task) 或 Project (/project)
     ↓
Status（今日计划）
     ↓
Execution
     ↓
Research（如需要 /research）
     ↓
Knowledge (/knowledge)
     ↓
Review (/review)
```

---

## CLI 命令速查

```bash
# 🌅 每日启动（推荐）
/daily-start
/daily-start focus:"架构评审" quick

# 快速问答
/ask 什么是任务生命周期?

# 头脑风暴（输出到 Inbox）
/brainstorm 微服务架构拆分方案

# 创建任务
/task 完成首页设计 priority:P1

# 创建项目
/project 构建习惯追踪应用
/project 00_Inbox/MyIdea.md

# 今日开工
/start main:"完成核心功能"

# 新增工作
/add 紧急bug修复

# 更新状态
/update 完成API开发

# 复盘
/review done:"完成了xxx" blocked:"卡在xxx"

# 晨间简报
/morning

# 深度研究
/research AI Agent 在政务服务中的应用

# 知识沉淀
/knowledge from:research AI Agent应用

# 战略判断
/strategy context:"当前方向困惑"

# 归档
/archive
/archive all
```

---

## RSS 信息源

### AI & Agent (TOP 10)

| 优先级 | 来源 | URL |
|--------|------|-----|
| P0 | OpenAI | https://openai.com/blog/rss |
| P0 | Anthropic | https://www.anthropic.com/rss |
| P0 | TLDR AI | https://bullrich.dev/tldr-rss/ai.rss |
| P1 | The Rundown AI | https://rss.beehiiv.com/feeds/2R3C6Bt5wj.xml |
| P1 | Google AI | https://ai.googleblog.com/feeds/posts/default |
| P1 | Microsoft AI | https://blogs.microsoft.com/ai/feed/ |
| P2 | Meta AI | https://about.meta.com/rss/meta-ai/ |
| P2 | Apple AI | https://machinelearning.apple.com/rss |
| P2 | AI Weekly | https://aiweekly.co/rss.xml |

### GovTech (TOP 3)

| 来源 | URL |
|------|-----|
| 国务院 | https://www.gov.cn/rss/gov.xml |

### BigTech (TOP 5)

| 优先级 | 来源 | URL |
|--------|------|-----|
| P1 | GitHub | https://github.com/github/roadmap/issues.atom |
| P1 | AWS News | https://aws.amazon.com/new/feeds/current.xml |
| P1 | Google Cloud | https://cloud.google.com/blog/rss |
| P2 | Azure | https://azure.microsoft.com/updates/feed/ |
| P2 | Meta Engineering | https://engineering.fb.com/?format=RSS |
| P2 | Netflix Tech | https://netflixtechblog.com/feed |

---

## 模板与 Schema

### 模板路径

所有模板位于 `99_System/templates/`：

| 模板 | 用途 |
|------|------|
| `task.md` | 任务模板 |
| `project.md` | 项目模板 |
| `brief.md` | 晨间简报模板 |
| `plan.md` | 今日计划模板 |
| `review.md` | 复盘模板 |
| `research.md` | 研究模板 |
| `knowledge.md` | 知识模板 |
| `opportunity.md` | 机会模板 |
| `strategy.md` | 战略模板 |
| `idea.md` | 想法模板 |

### Schema 路径

所有 Schema 位于 `99_System/schemas/`：

| Schema | 用途 |
|--------|------|
| `task.schema.yaml` | 任务 YAML 校验 |
| `project.schema.yaml` | 项目 YAML 校验 |
| `research.schema.yaml` | 研究 YAML 校验 |
| `knowledge.schema.yaml` | 知识 YAML 校验 |
| `daily.schema.yaml` | 每日文件校验 |
| `idea.schema.yaml` | 想法 YAML 校验 |

---

## Obsidian 集成

### 可选插件

以下插件用于增强 Obsidian 内的手动操作体验（Agent Skills 独立运行，不依赖这些插件）：

| 插件 | 用途 |
|------|------|
| **Dataview** | 在 Obsidian 中动态查询任务/项目 |
| **Templater** | 手动创建文件时使用模板 |
| **Calendar** | 日历视图，快速导航每日笔记 |

### Dashboard 路径

- `99_System/dashboards/overview.md` - 任务概览
- `99_System/dashboards/health.md` - 系统健康度
- `99_System/dashboards/daily.md` - 每日视图

### Dataview 查询示例

```dataview
TABLE status, priority, due
FROM "20_Tasks"
WHERE status = "active"
SORT priority ASC
```

---

## 系统健康指标

每周检查：

- [ ] active 任务数量 ≤ 3
- [ ] P0 任务 ≤ 1
- [ ] 无 7 天未更新任务
- [ ] Inbox 项目 48h 内处理
- [ ] 每周至少 1 篇知识沉淀

---

## Skill 开发规范

遵循 Anthropic 官方 Skill Building Guide：

### SKILL.md 结构

```yaml
---
name: skill-name                    # kebab-case
description: WHAT + WHEN + 触发词   # 包含触发条件
---

# Skill Body

## When to Use
## Workflow
## Template
## Constraints
```

### 目录结构

```
skill-name/
├── SKILL.md              # 核心指令（必须）
└── references/           # 详细文档（可选）
    └── workflow.md
```

---

## 注意事项

1. **所有文件必须有 YAML 头部** - 这是 Agent 扫描的基础
2. **任务不要写成长文章** - 任务是最小可执行单元
3. **研究必须沉淀为知识** - 删除时间依赖内容
4. **每日必须闭环** - Morning → Plan → Execute → Review
5. **系统负载受控** - 严格遵守 active ≤ 3 规则
6. **所有想法先进入 Inbox** - 经过评估后再分类处理
