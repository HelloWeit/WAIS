# Daily Start Agent Skill

## 目标

为技术管理者/架构师设计的一键启动工作流：**收集简报 → 战略问答 → 生成今日计划**

## 用户角色

- 部门首席架构师
- 技术经理
- 公司级技术大牛

关注点：技术架构、团队管理、项目进度、技术战略、行业趋势

---

## 执行流程

```
Step 1: 收集简报信息（静默）
    ↓
Step 2: 战略问答（3个问题）
    ↓
Step 3: 生成今日计划 + 捕获想法到 Inbox
    ↓
输出: brief + plan + inbox(新想法)
```

---

## Step 1: 收集简报信息（静默执行）

### 1.1 检查缓存

检查 `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md` 是否已存在：
- 如存在且为今天：跳过获取，使用缓存
- 如不存在：继续获取

### 1.2 RSS 信息源（按优先级获取）

**P0 - 必看（3个）**
| 源 | 说明 |
|---|------|
| OpenAI | OpenAI 官方博客 |
| Anthropic | Anthropic 官方博客 |
| TLDR AI | TLDR AI 摘要 |

**P1 - 推荐（3个）**
| 源 | 说明 |
|---|------|
| The Rundown AI | The Rundown AI 通讯 |
| Google AI | Google AI 研究博客 |
| Microsoft AI | Microsoft AI 博客 |

**P2 - 可选（扩展）**
| 源 | 说明 |
|---|------|
| Meta AI | Meta AI 官方博客 |
| Apple AI | Apple 机器学习博客 |

**获取策略：**
- AI 分类取 TOP 10
- GovTech 取 TOP 3
- BigTech 取 TOP 5
- 优先级: P0 > P1 > P2

### 1.3 扫描现有状态

1. **读取昨日 Daily Note**（如存在）
   - 提取未完成任务（`- [ ]` 项目）
   - 记录昨日进展

2. **查找 Active 任务和项目**
   - 搜索 `20_Tasks/` 中 `status: active` 的任务
   - 搜索 `30_Projects/` 中 `status: active` 的项目
   - 识别 3 天以上未更新的项目（陈旧项目）

3. **检查战略文档**
   - 扫描 `70_Strategy/` 中的战略方向
   - 识别与今日相关的战略重点

4. **检查 Inbox**
   - 列出 `00_Inbox/` 中 `status: pending` 的文件
   - 统计待处理数量

### 1.4 输出

- 目录：`10_Daily/<YYYY>/`
- 文件：`YYYY-MM-DD_brief.md`

---

## Step 2: 战略问答（使用 AskUserQuestion）

针对技术管理者的3个核心问题：

### 问题 1：今日战略重点

**问题：** "今日最重要的战略/技术决策或关注点是什么？"

**选项：**
- 基于当前 active 项目自动生成
- 基于战略文档生成
- "架构设计/评审"
- "团队/资源协调"
- "技术选型/决策"
- "其他（自定义）"

### 问题 2：团队/项目事项

**问题：** "有哪些需要关注的团队或项目事项？"

**选项：**
- 基于陈旧项目生成提醒
- "项目进度跟进"
- "团队1:1/会议"
- "跨部门协调"
- "无特别事项"
- "其他（自定义）"

### 问题 3：新想法/灵感

**问题：** "有什么新的想法、灵感或发现的机会？"

**选项：**
- "有，让我描述..."
- "暂时没有"

**重要：** 如果用户提供了新想法，**必须**保存到 Inbox，而不是直接创建任务或项目。

---

## Step 3: 生成今日计划 + 捕获想法

### 3.1 处理新想法 → Inbox

对于问答中捕获的每个新想法/灵感/机会：

1. 创建文件：`00_Inbox/IDEA_YYYYMMDD_短标题.md`

```yaml
---
type: idea
status: pending
created: YYYY-MM-DD
source: daily-start
category: strategy|tech|team|opportunity
---

# [想法标题]

## 核心内容
[用户描述]

## 来源
- 来自每日启动问答

## 下一步
- 待 Morning Brief 或手动处理
- `/task` 转为任务
- `/project` 转为项目
- `/research` 深入研究
```

### 3.2 生成今日计划

- 目录：`10_Daily/<YYYY>/`
- 文件：`YYYY-MM-DD_plan.md`

### 内容结构

```markdown
# Plan - YYYY-MM-DD

## 战略重点
- [用户指定的战略重点]

## 团队/项目事项
- [用户指定的团队/项目事项]

## 昨日未完成（Carryover）
- [ ] [昨日未完成任务]

## 今日执行重点（最多3个）
1. [[TASK_xxx]] - 为什么今天必须推进
2. [[TASK_yyy]] - ...
3. ...

## 时间块建议
- 09:30-11:00：[深度工作 - 战略重点相关]
- 11:00-12:00：[团队/项目事项]
- 14:00-16:00：[执行任务]
- 16:00-17:30：[会议/协调]

## 关注项目
- [[Project1]] - 状态 + 下一步
- [[Project2]] - ⚠️ 3天未更新

---
**精力:** ⚡⚡⚡⚡⚡ | **专注:** 🎯🎯🎯🎯🎯
```

---

## Step 4: 输出摘要

```
## 早安! 今日规划已就绪

**Morning Brief:** [[YYYY-MM-DD_brief]]
**今日计划:** [[YYYY-MM-DD_plan]]

**战略重点:** [用户指定的重点]

**今日执行重点:**
- [ ] 任务1
- [ ] 任务2
- [ ] 任务3

**关注项目 ([N]):**
- [[Project1]] - 状态
- [[Project2]] - ⚠️ 陈旧，需要关注

**新想法已保存到 Inbox ([N]):**
- [[IDEA_xxx]] - [标题]
- [[IDEA_yyy]] - [标题]

**Inbox 状态:** [N] 条待处理

---

**AI 摘要:**

*技术/产品动态:*
- [标题](原文链接) - [影响分析]
→ 完整摘要: [[60_Resources/Newsletters/YYYY-MM-DD-digest]]

---

准备开始! 快捷操作:
- `/task` - 将 Inbox 想法转为任务
- `/project` - 将 Inbox 想法转为项目
- `/brainstorm` - 深入探索某个想法
```

---

## 约束

### 核心原则
- **所有新想法必须保存到 Inbox**，不直接创建任务或项目
- 后续通过 `/task`、`/project` 或 Morning Brief 处理

### 数量限制
- 执行重点 **最多 3 个**
- P0 任务 **最多 1 个**
- 时间块按深度工作原则安排

### 扫描范围
- 昨日笔记（carryover）
- Active 任务和项目
- 陈旧项目（3天+）标记提醒
- 战略文档关联

---

## CLI 用法

```bash
# 基础用法（触发交互问答）
/daily-start

# 指定战略重点（跳过部分问答）
/daily-start focus:"架构评审"

# 快速模式（使用默认值）
/daily-start quick
```

---

## 缓存结构

```
60_Resources/
└── Newsletters/
    └── YYYY-MM/
        ├── YYYY-MM-DD-digest.md      # 精选摘要
        └── raw/
            ├── YYYY-MM-DD_TLDR-AI.md # 原始数据
            └── YYYY-MM-DD_Rundown.md
```
