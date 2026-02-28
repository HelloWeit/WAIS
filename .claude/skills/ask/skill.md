---
name: ask
description: 快速问答，不产生任何文件。Use when user says "/ask", "快速问答", or asks a quick question that doesn't need file output.
---

# Ask Skill

快速问答工具，直接回答问题，不创建任何文件。

## When to Use

- 用户说 "/ask" 或 "快速问答"
- 用户需要一个简单答案，不需要文档输出
- 快速验证概念或获取信息

## Behavior

1. 检查现有知识库（可选，快速浏览 `50_Knowledge/` 目录）
2. 直接回答问题
3. 结束 - **不产生任何文件**

## Constraints

- **禁止创建任何文件**
- **禁止创建计划**
- **禁止生成子 agent**
- 保持回答简洁直接

## Position

工作流之外的轻量级问答工具，适合不需要留痕的快速咨询。
