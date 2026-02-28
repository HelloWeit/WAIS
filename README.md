
# 🧠 PAIOS

**Personal AI Operating System**
Version: 1.0

---

# 一、定位与目标

## 1.1 定位

PAIOS 是一个由 Agent 驱动的个人工作操作系统。

它不是：

* 笔记工具
* ToDo 管理器
* 新闻聚合器

它是：

> 个人认知组织系统 + 决策控制中枢 + 执行调度系统

---

## 1.2 目标

PAIOS v1.0 的目标：

* 建立结构化文件体系
* 建立任务生命周期管理
* 建立每日闭环工作流
* 建立研究沉淀机制
* 形成可持续运行模型

---

# 二、系统架构

## 2.1 目录结构

```
00_Inbox/
10_Daily/
20_Tasks/
30_Projects/
40_Research/
50_Knowledge/
60_Resources/
70_Strategy/
80_Opportunities/
90_Archive/
99_System/
```

---

## 2.2 目录职责定义

### 00_Inbox

作用：
所有临时想法、会议纪要、灵感、截图、链接的入口。

规则：

48 小时必须处理

处理后标记 status: processed

不允许长期存放

典型来源：

你手写想法

AI 生成草稿

外部资料

---

### 10_Daily

每日文件集中区。

文件类型：

* YYYY-MM-DD_brief.md
* YYYY-MM-DD_plan.md
* YYYY-MM-DD_review.md


---

### 20_Tasks

任务最小执行单元。
所有任务必须在此目录。

---

### 30_Projects

项目级容器。
项目包含多个任务。

---

### 40_Research

研究输出区。
禁止直接当知识库使用。

---

### 50_Knowledge

抽象后的长期知识资产。
必须无时间依赖。

---

### 60_Resources

纯素材区。
无结构化分析。

---

### 70_Strategy

年度/季度/阶段方向。

---

### 80_Opportunities

潜在机会池。
可转化为任务。

---

### 90_Archive

完成或终止的任务与项目。

---

### 99_System

模板、规则、Prompt、统计面板。

---

# 三、数据规范

## 3.1 所有文件必须包含 YAML 头部

标准模板：

```yaml
---
type: task | project | research | brief | plan | review | knowledge | strategy | opportunity
status: draft | active | blocked | done | archived
priority: P0 | P1 | P2
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
source: manual | agent | meeting | brief
---
```

---

## 3.2 命名规范

### 任务

```
TASK_YYYYMMDD_简要名称.md
```

### 研究

```
RESEARCH_主题_YYYYMMDD.md
```

### 知识

```
KNOWLEDGE_主题.md
```

---

# 四、任务生命周期模型

```
idea → draft → active → blocked → done → archived
```

规则：

* 同时 active 任务 ≤ 3
* P0 任务 ≤ 1
* 7 天未更新自动提醒

---

# 五、每日工作流（v1.0 标准闭环）

## 1️⃣ Morning Brief

输出：

* AI 关键动态
* 自定义相关趋势（比如 政务服务、技术）
* 可转行动点

---

## 2️⃣ Task Capture

将新想法转为任务。

---

## 3️⃣ Status 启动

扫描：

* 未完成任务
* 今日新增事项
* 形成今日计划

---

## 4️⃣ Execution

只执行 active 任务。

---

## 5️⃣ Research（按需）

深度研究并形成结构化输出。

---

## 6️⃣ Knowledge 沉淀

研究结束必须抽象为知识。

---

## 7️⃣ Review

生成：

* 完成情况
* 风险
* 明日预热

---

# 六、Agent 职责边界

| Agent     | 职责   | 禁止    |
| --------- | ---- | ----- |
| Morning   | 汇总趋势 | 不生成任务 |
| Task      | 创建任务 | 不规划今日 |
| Status    | 生成计划 | 不写研究  |
| Strategy  | 方向判断 | 不写执行  |
| Research  | 深度分析 | 不抽象知识 |
| Knowledge | 抽象模型 | 不写时间线 |
| Review    | 复盘总结 | 不新增任务 |

---

# 七、系统运行原则

### 原则 1

任务优先级必须明确。

### 原则 2

研究必须沉淀。

### 原则 3

每日必须闭环。

### 原则 4

系统负载必须受控。

---

# 八、系统指标（PAIOS 健康度）

每周统计：

* active 任务数量
* 完成率
* 新研究数量
* 知识沉淀数量
* 未处理 Inbox 数量

---

# 九、v1.0 成功标准

连续运行 30 天：

* 无任务失控
* 无研究堆积
* 每周至少 1 篇知识沉淀
* active 任务 ≤ 3

---

# 十、版本演进规划

### v2.0

加入 Dataview 自动统计
加入状态自动扫描

### v3.0

加入 MCP Agent 编排

---

# 十一、核心定义

PAIOS 的本质：

> 通过结构化规则，把个人决策过程外显化，并通过 Agent 协同放大认知杠杆。

---

# 十二、项目结构

```
paios/
├── vault/                          # Obsidian Vault 根目录
│   ├── 00_Inbox/                   # 输入缓冲区
│   ├── 10_Daily/                   # 每日文件（brief/plan/review）
│   │   └── 2026/
│   ├── 20_Tasks/                   # 任务池
│   ├── 30_Projects/                # 项目容器
│   ├── 40_Research/                # 研究输出
│   ├── 50_Knowledge/               # 知识资产
│   ├── 60_Resources/               # 素材池
│   ├── 70_Strategy/                # 战略层
│   ├── 80_Opportunities/           # 机会池
│   ├── 90_Archive/                 # 历史沉淀
│   └── 99_System/                  # 系统内核
│       ├── templates/              # 文件模板
│       ├── schemas/                # YAML Schema
│       └── dashboards/             # Dataview 面板
├── .skills/                        # Agent Skills（隐藏目录）
│   ├── task/                       # 任务 Agent
│   ├── status/                     # 状态 Agent
│   ├── morning/                    # Morning Brief Agent
│   ├── review/                     # 复盘 Agent
│   ├── research/                   # 研究 Agent
│   ├── knowledge/                  # 知识 Agent
│   ├── strategy/                   # 战略 Agent
│   ├── daily-start/                # 每日启动 Agent
│   ├── ask/                        # 快速问答 Agent
│   ├── brainstorm/                 # 头脑风暴 Agent
│   ├── archive/                    # 归档 Agent
│   └── project/                    # 项目创建 Agent
├── README.md                       # 项目说明
├── CLAUDE.md                       # Claude 指引文件
└── content.md                      # 详细文档
```

---

# 十三、CLI 命令速查

| 命令 | 作用 | 示例 |
|------|------|------|
| `/daily-start` | 一键启动（简报+问答+计划） | `/daily-start main:"完成核心功能"` |
| `/ask` | 快速问答（不创建文件） | `/ask 什么是任务生命周期?` |
| `/brainstorm` | 交互式头脑风暴 | `/brainstorm 构建知识图谱` |
| `/task` | 创建任务 | `/task 完成首页设计` |
| `/project` | 想法→项目 | `/project 构建习惯追踪应用` |
| `/start` | 今日开工 | `/start main:"完成核心功能"` |
| `/add` | 新增工作 | `/add 紧急bug修复` |
| `/update` | 更新状态 | `/update 完成API开发` |
| `/review` | 今日复盘 | `/review done:"xxx"` |
| `/morning` | 生成简报 | `/morning` |
| `/research` | 深度研究 | `/research AI Agent趋势` |
| `/knowledge` | 知识沉淀 | `/knowledge from:research xxx` |
| `/strategy` | 战略判断 | `/strategy` |
| `/archive` | 归档完成项目 | `/archive` |

---

# 十四、RSS 信息源

```yaml
ai:
  - TLDR AI: https://bullrich.dev/tldr-rss/ai.rss
  - The Rundown AI: https://rss.beehiiv.com/feeds/2R3C6Bt5wj.xml
govtech: []
bigtech: []
```

---

# 十五、Obsidian 集成配置

## 15.1 安装 Obsidian

1. 下载并安装 [Obsidian](https://obsidian.md/)
2. 打开 Obsidian，选择「打开文件夹为仓库」
3. 选择 `paios/vault` 目录作为 Vault 根目录

## 15.2 必装插件

在 Obsidian 设置 → 第三方插件 中安装以下插件：

| 插件 | 用途 | 必要性 |
|------|------|--------|
| **Dataview** | 数据查询与统计面板 | ⭐⭐⭐ 必装 |
| **Templater** | 高级模板功能 | ⭐⭐⭐ 必装 |
| **Calendar** | 日历视图 | ⭐⭐ 推荐 |
| **Tasks** | 任务管理增强 | ⭐⭐ 推荐 |
| **QuickAdd** | 快速添加内容 | ⭐ 可选 |
| **Periodic Notes** | 周期性笔记 | ⭐ 可选 |

## 15.3 配置 Dataview

1. 设置 → 第三方插件 → Dataview → 开启
2. 开启以下选项：
   - Enable JavaScript Queries
   - Enable Inline Queries

## 15.4 配置 Templater

1. 设置 → 第三方插件 → Templater → 开启
2. 设置模板文件夹：`99_System/templates`
3. 配置快捷键：
   - `Cmd/Ctrl + T`：插入模板

## 15.5 推荐主题

- **Minimal**：简洁高效
- **Things**：清晰易读
- **Blue Topaz**：功能丰富

---

# 十六、每日工作流（Obsidian + AI Agent）

## 每日闭环流程图

```
┌─────────────────────────────────────────────────────────────┐
│                        每日闭环                              │
├─────────────────────────────────────────────────────────────┤
│  08:00  Daily Start      →  /daily-start  →  brief + plan  │
│    ↓                                                         │
│  09:00  Execution        →  在 Obsidian 中执行任务          │
│    ↓                                                         │
│  (随时) Task Capture     →  /task → 20_Tasks/               │
│    ↓                                                         │
│  (按需) Research         →  /research → 40_Research/        │
│    ↓                                                         │
│  18:00  Review           →  /review → 10_Daily/*_review     │
└─────────────────────────────────────────────────────────────┘
```

## 16.1 早晨：Daily Start（08:00）⭐ 推荐

**在 AI Agent 中执行：**
```
/daily-start
/daily-start main:"今天的主线目标"
```

**AI 将生成：**
- Step 1: 收集 RSS 信息，生成 Morning Brief
- Step 2: 扫描任务池，生成今日计划

**输出文件：**
- `10_Daily/YYYY/YYYY-MM-DD_brief.md`
- `10_Daily/YYYY/YYYY-MM-DD_plan.md`

## 16.2 开工：Status 启动（单独使用）

**在 AI Agent 中执行：**
```
/start main:"今天的主线目标"
```

## 16.3 执行：任务管理（09:00-18:00）

### 创建新任务

**方式一：AI Agent（推荐）**
```
/task 完成用户登录功能
/task from:brief 3 跟进AI动态中的机会点
```

**方式二：Obsidian Templater**
1. 在 `20_Tasks/` 目录新建文件
2. 按 `Cmd/Ctrl + T` 插入任务模板
3. 填写任务内容

### 更新任务状态

在 Obsidian 中直接编辑任务的 YAML 头部：
```yaml
status: active  # draft → active → blocked → done → archived
```

### 查看任务看板

打开 `99_System/dashboards/overview.md` 查看 Dataview 面板。

## 16.4 研究：深度分析（按需）

**在 AI Agent 中执行：**
```
/research AI Agent 在政务服务中的应用
```

## 16.5 沉淀：知识抽象（研究完成后）

**在 AI Agent 中执行：**
```
/knowledge from:research AI Agent 在政务服务中的应用
```

## 16.6 收盘：Review 复盘（18:00）

**在 AI Agent 中执行：**
```
/review done:"完成了xxx" blocked:"卡在xxx"
```

---

# 十七、Obsidian 高效操作技巧

## 17.1 快捷键配置

| 功能 | 推荐快捷键 |
|------|-----------|
| 插入模板 | `Cmd/Ctrl + T` |
| 快速切换文件 | `Cmd/Ctrl + O` |
| 全局搜索 | `Cmd/Ctrl + Shift + F` |
| 命令面板 | `Cmd/Ctrl + P` |
| 返回 | `Cmd/Ctrl + [` |
| 前进 | `Cmd/Ctrl + ]` |

## 17.2 工作区布局

推荐创建以下工作区：

1. **Morning**：左侧 Calendar，右侧今日 brief + plan
2. **Focus**：全屏当前任务文档
3. **Review**：左侧任务列表，右侧 review 文档

保存方式：右侧边栏 → 工作区 → 保存当前工作区

## 17.3 常用 Dataview 查询

### 查看所有活跃任务
```dataview
LIST
FROM "20_Tasks"
WHERE status = "active"
SORT priority ASC
```

### 查看本周完成情况
```dataview
TABLE completed as "完成时间"
FROM "20_Tasks"
WHERE status = "done" AND completed >= date(today) - dur(7 days)
SORT completed DESC
```

---

# 十八、启动步骤

## 18.1 初始化（一次性）

- [x] 建立目录结构
- [x] 写 README
- [x] 建立 YAML 模板
- [ ] 安装 Obsidian
- [ ] 安装 Dataview 插件
- [ ] 安装 Templater 插件
- [ ] 配置模板文件夹

## 18.2 每日启动

1. 打开 Obsidian，进入 `vault` 仓库
2. 打开 AI Agent（Claude Code / Gemini CLI）
3. 执行 `/daily-start` 一键生成简报和计划
4. 开始执行任务

## 18.3 每日收盘

1. 执行 `/review` 生成复盘
2. 在 Obsidian 中检查任务状态
3. 确保所有 Inbox 项目已处理

---

# 十九、故障排查

| 问题 | 解决方案 |
|------|---------|
| Dataview 不显示数据 | 检查 YAML 格式，确保缩进正确 |
| 模板无法插入 | 检查 Templater 模板文件夹路径 |
| 找不到文件 | 使用 `Cmd/Ctrl + O` 快速切换 |
| 任务状态不更新 | 检查 YAML 中 status 字段拼写 |
