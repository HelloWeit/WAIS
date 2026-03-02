# 🧠 WAIS

**Work AI Station** - 个人 AI 工作站

[![GitHub](https://img.shields.io/badge/GitHub-HelloWeit/wais-blue)](https://github.com/HelloWeit/wais)

---

## 简介

WAIS 是一个由 Agent Skills 驱动的个人工作站，结合 Obsidian 进行文件管理和可视化。

**它能帮你：**
- 管理每日任务和项目
- 收集和整理信息
- 沉淀可复用的知识
- 保持工作节奏（计划-执行-复盘）

**它不是：** 笔记工具、ToDo 管理器、新闻聚合器

---

## 快速开始

### 1. 获取项目

```bash
git clone https://github.com/HelloWeit/wais.git
cd wais
```

> **说明：** 克隆后目录结构已完整（00_Inbox, 10_Daily, 20_Tasks 等），无需额外初始化或创建目录。

### 2. 开始使用

在项目目录下启动 Claude Code，即可使用 Agent Skills：

```bash
# 每日启动（推荐首次使用）
/daily-start

# 创建任务
/task 完成首页设计

# 头脑风暴
/brainstorm 微服务架构方案
```

> **首次启动时：** Agent 会自动检测现有目录内容。如果目录已存在，直接扫描内容；如果目录不存在，才会创建。

### 3. 可选：配置 Obsidian

如需在 Obsidian 中可视化管理和浏览文件：

1. 下载 [Obsidian](https://obsidian.md/)
2. 打开 Obsidian，选择「打开文件夹为仓库」
3. 选择 `wais` 目录

**可选插件：**

| 插件 | 用途 |
|------|------|
| Dataview | 动态查询任务/项目 |
| Templater | 手动创建文件时使用模板 |
| Calendar | 日历视图 |

> **注意：** Agent Skills 完全独立运行，Obsidian 和插件都是可选的可视化增强工具。

---

## 目录结构

```
wais/
├── .claude/
│   └── skills/                  # 12 个 Agent Skills
├── 00_Inbox/                    # 想法缓冲区
├── 10_Daily/                    # 每日笔记
│   └── YYYY/
├── 20_Tasks/                    # 任务池
├── 30_Projects/                 # 项目
├── 40_Research/                 # 研究
├── 50_Knowledge/                # 知识库
├── 60_Resources/                # 资源
├── 70_Strategy/                 # 战略
├── 80_Opportunities/            # 机会池
├── 90_Archive/                  # 归档
└── 99_System/                   # 系统
    ├── templates/               # 模板
    ├── schemas/                 # Schema
    └── dashboards/              # 看板
```

---

## Agent Skills

| 命令 | 用途 | 输出 |
|------|------|------|
| `/daily-start` | 一键启动（简报+问答+计划） | `10_Daily/` |
| `/morning` | 晨间简报 | `10_Daily/` |
| `/task` | 创建任务 | `20_Tasks/` |
| `/project` | 创建项目 | `30_Projects/` |
| `/status` | 状态管理 | `10_Daily/` |
| `/review` | 每日复盘 | `10_Daily/` |
| `/research` | 深度研究 | `40_Research/` |
| `/knowledge` | 知识沉淀 | `50_Knowledge/` |
| `/strategy` | 战略判断 | `70_Strategy/` |
| `/brainstorm` | 头脑风暴 | `00_Inbox/` |
| `/archive` | 归档 | `90_Archive/` |
| `/ask` | 快速问答 | 无文件 |

---

## 工作流

```
外部信息 → Inbox → Brief → Task/Project → Status → Execution → Research → Knowledge → Review
              ↑
        /brainstorm 输出到这里
```

### 每日闭环

```
08:00  /daily-start  →  brief + plan
09:00  Execution     →  执行任务
(随时)  /task        →  创建新任务
(按需)  /research    →  深度研究
18:00  /review       →  复盘总结
```

---

## 核心规则

### 任务生命周期

```
draft → active → blocked → done → archived
```

### 硬性约束

- Active 任务 **≤ 3**
- P0 任务 **≤ 1**
- 7 天未更新自动提醒
- Inbox 48h 内处理

### 文件命名

| 类型 | 格式 |
|------|------|
| 任务 | `TASK_YYYYMMDD_标题.md` |
| 研究 | `RESEARCH_主题_YYYYMMDD.md` |
| 知识 | `KNOWLEDGE_主题.md` |
| 想法 | `IDEA_YYYYMMDD_标题.md` |

---

## RSS 信息源

### AI & Agent (TOP 10)

| 优先级 | 来源 |
|--------|------|
| P0 | OpenAI, Anthropic, TLDR AI |
| P1 | The Rundown AI, Google AI, Microsoft AI |
| P2 | Meta AI, Apple AI, AI Weekly |

### GovTech (TOP 3)

- 国务院
- 国家政策法规

### BigTech (TOP 5)

| 优先级 | 来源 |
|--------|------|
| P1 | GitHub, AWS News, Google Cloud |
| P2 | Azure, Meta Engineering, Netflix Tech |

---

## Skill 开发

遵循 Anthropic 官方 Skill Building Guide：

```
skill-name/
├── SKILL.md              # 核心指令
└── references/           # 详细文档
```

SKILL.md 格式：

```yaml
---
name: skill-name
description: WHAT + WHEN + 触发词
---

# Skill Body
```

---

## 配置 Obsidian

### Dataview

设置 → Dataview → 开启：
- Enable JavaScript Queries
- Enable Inline Queries

### Templater

设置 → Templater：
- 模板文件夹：`99_System/templates`

### 推荐主题

- **Minimal** - 简洁高效
- **Things** - 清晰易读

---

## 常见问题

| 问题 | 解决方案 |
|------|---------|
| Dataview 不显示 | 检查 YAML 格式和缩进 |
| 模板无法插入 | 检查 Templater 模板路径 |
| Skill 不识别 | 确保在项目目录下运行 |

---

## 许可证

MIT License

---

## 更新日志

### 2026-02-28

- 完成 12 个 Agent Skills
- 按照 Anthropic 规范重构 SKILL.md
- 创建完整目录结构
- 添加 RSS 信息源配置
