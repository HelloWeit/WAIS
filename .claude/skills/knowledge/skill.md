---
name: knowledge
description: 从研究成果中抽象出可复用的知识模型，写入知识库供后续引用。Use when user says "/knowledge", "知识沉淀", "抽象模型", or wants to extract reusable knowledge from research.
---

# Knowledge Skill

从研究文档中提取可复用的知识模型，建立个人知识库。

## When to Use

- 用户说 "/knowledge", "知识沉淀", "抽象模型"
- 完成一项研究后，想要沉淀知识
- 需要建立可复用的知识模型

## Input

| Field | Required | Description |
|-------|----------|-------------|
| source | Yes | 研究文档路径或内容引用 |

## Output

```
50_Knowledge/
└── KNOWLEDGE_主题.md
```

## Workflow

1. 读取指定的研究文档
2. 提取核心概念和模型
3. 删除时间敏感内容
4. 生成可复用的知识笔记
5. 添加到知识库索引

## Knowledge Criteria

知识必须满足：

- **无时间依赖**: 不包含过期信息
- **可复用**: 能被多个研究引用
- **结构化**: 清晰的模型或框架
- **可检索**: 合适的标签和索引

## Template Structure

```markdown
---
type: knowledge
category: [技术/管理/战略/工具]
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# KNOWLEDGE_主题

## 核心概念

## 模型/框架

## 应用场景

## 相关研究
- [[RESEARCH_xxx]]
```

## Constraints

- 必须无时间依赖
- 必须可复用
- 必须可被多个研究引用
- 删除所有时间敏感内容

## Best Practice

完成 `/research` 后，运行 `/knowledge` 沉淀知识。
