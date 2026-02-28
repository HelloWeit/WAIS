---
name: brainstorm
description: 技术管理者交互式探索想法，从技术/团队/战略维度头脑风暴，输出结构化笔记到 Inbox。Use when user says "/brainstorm", "头脑风暴", "探索想法", or wants to explore ideas interactively.
---

# Brainstorm Skill

技术管理者专用的交互式头脑风暴工具，帮助从多个维度探索想法。

## When to Use

- 用户说 "/brainstorm", "头脑风暴", "探索想法"
- 需要从多维度思考一个技术问题
- 想要产生新的想法或解决方案

## User Role

- 架构师
- 技术经理
- 技术专家
- 技术团队负责人

## Exploration Dimensions

### 技术维度
- 架构设计
- 技术选型
- 技术债务

### 团队维度
- 资源配置
- 协作效率
- 团队能力

### 战略维度
- 业务对齐
- 风险评估
- 机会识别

## Workflow

### Phase 1: 交互探索
- 选择探索维度（技术/团队/战略）
- 通过问答引导深入思考
- 使用 AskUserQuestion 工具进行交互

### Phase 2: 综合
- 整理探索过程中产生的想法
- 生成结构化的想法笔记

### Phase 3: 输出到 Inbox
- 保存到 `00_Inbox/IDEA_YYYYMMDD_短标题.md`
- 使用 idea 模板格式

## Output

```
00_Inbox/
└── IDEA_YYYYMMDD_短标题.md
```

## Next Steps

用户可以选择：
- `/task` - 将想法转为任务
- `/project` - 将想法转为项目
- `/research` - 深入研究该想法

## Constraints

- **必须输出到 Inbox**
- **禁止直接创建任务或项目**
- 保持工作流一致性：想法 → Inbox → 分类处理

## Principle

所有想法先进入 Inbox，经过评估后再决定是转为任务、项目还是深入研究。
