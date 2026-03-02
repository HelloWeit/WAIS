# Project Agent Skill

## 目标

将想法或 Inbox 笔记转换为结构化的项目笔记。

---

## 输入方式

1. **文件路径**：Inbox 笔记路径（如 `/project 00_Inbox/MyIdea.md`）
2. **内联文本**：简短的项目想法描述（如 `/project 构建习惯追踪应用`）
3. **无输入**：列出 `00_Inbox/` 文件让用户选择

---

## Step 1: 收集上下文

1. **读取输入**
   - 如是文件：读取内容
   - 如是内联：作为项目描述

2. **搜索相关内容**
   - 检查 `20_Projects/` 是否有类似项目
   - 检查 `30_Tasks/` 是否有相关任务
   - 检查 `40_Research/` 和 `50_Knowledge/` 避免重复

3. **识别相关领域**
   - 从现有研究中识别相关领域

---

## Step 2: 创建项目计划

在 `20_Projects/_plans/` 创建计划文件（如不存在则创建目录）：

```markdown
# 启动计划: [项目名称]

## 来源
- 收件箱文件: [路径或"内联输入"]

## 目标
[一句话总结项目目标]

## 项目结构
- 领域: [相关领域]
- 类型: project
- 预估规模: [小型/中型/大型]

## 建议行动项
- [ ] 定义成功标准
- [ ] 分解为阶段/里程碑
- [ ] 识别依赖项或阻碍因素
- [ ] 创建初始任务

## 项目大纲草案
### 背景
[这解决什么问题，为什么重要]

### 行动（阶段）
- 阶段1: [描述]
- 阶段2: [描述]

### 成功指标
- [ ] 指标1
- [ ] 指标2

## 澄清问题
**问:** 这个项目的时间线/截止日期是什么？
**答:**

**问:** 优先级是多少？（P0=紧急, P1=高, P2=中）
**答:**
```

---

## Step 3: 用户确认

使用 AskUserQuestion 让用户：
1. 审查计划
2. 回答澄清问题
3. 确认或修改

---

## Step 4: 创建项目笔记

### 项目 Frontmatter

```yaml
---
type: project
status: active
priority: P1
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [project, relevant-tags]
due: YYYY-MM-DD (or empty)
---
```

### 项目内容结构（C.A.P.）

```markdown
# [项目名称]

## Context（背景）
- 目标
- 为什么重要
- 背景信息

## Actions（行动）
- [ ] 阶段1: [描述]
  - [ ] 任务1
  - [ ] 任务2
- [ ] 阶段2: [描述]

## Progress（进展）
- YYYY-MM-DD: 项目启动
```

### 保存位置

- 小型项目：`20_Projects/<ProjectName>.md`
- 中/大型项目：`20_Projects/<ProjectName>/<ProjectName>.md`

---

## Step 5: 后续处理

1. **更新今日 Daily Note**
   - 添加项目链接

2. **归档 Inbox（如适用）**
   - 更新 frontmatter：`status: processed`, `archived: YYYY-MM-DD`
   - 移动到 `90_Archive/Inbox/YYYY/MM/`
   - 移动后 `00_Inbox/` 不再保留原文件

3. **创建初始任务**
   - 在 `30_Tasks/` 创建项目相关任务

---

## 输出摘要

```
## 项目创建完成

**项目笔记:** [[ProjectName]] 位于 20_Projects/
**项目结构:** [结构说明]
**收件箱归档:** [归档路径] (如适用)

**已创建任务:**
- [[TASK_xxx]]
- [[TASK_yyy]]

**建议的下一步:**
- [ ] 下一步1
- [ ] 下一步2
```

---

## 约束

- 项目通过 frontmatter 链接到领域，而非文件夹层次
- 使用 wikilinks `[[NoteName]]` 连接相关笔记
- 不要创建重复文件 - 先检查项目是否已存在

---

## CLI 用法

```bash
/project                                  # 列出 Inbox 选择
/project 00_Inbox/MyIdea.md              # 从 Inbox 文件
/project 构建个人知识管理系统              # 内联描述
```
