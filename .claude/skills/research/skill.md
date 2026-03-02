---
name: research
description: 深度研究某主题，输出结构化研究文档，包含可落地建议。Use when user says "/research", "研究", or wants to do deep research on a topic.
---

# Research Skill

深度研究特定主题，输出结构化的研究文档。

## When to Use

- 用户说 "/research", "研究"
- 需要深入了解某个技术或业务主题
- 为决策提供研究支持

## Input

| Field | Required | Description |
|-------|----------|-------------|
| topic | Yes | 研究主题 |
| questions | No | 具体研究问题 |
| task | No | 关联任务 ID |
| project | No | 关联项目名称 |
| source | No | 来源文件路径（可为 `00_Inbox/`） |

## Output

```
40_Research/
└── RESEARCH_主题_YYYYMMDD.md
```

## Workflow

1. **明确研究范围**
   - 确定主题和研究问题
   - 识别关联任务/项目

2. **信息收集**
   - 网络搜索
   - 读取相关文档
   - 查询知识库

3. **分析与综合**
   - 整理发现
   - 提取关键洞察
   - 形成结论

4. **生成报告**
   - 结构化输出
   - 包含可落地建议

5. **处理 Inbox 源文件（如适用）**
   - 当来源文件在 `00_Inbox/`：
   - 更新 frontmatter：`status: processed`, `archived: YYYY-MM-DD`
   - 移动到 `90_Archive/Inbox/YYYY/MM/`
   - 通过移动实现从 Inbox 删除原文件

## Template

```markdown
---
type: research
topic: [研究主题]
status: done
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
task: [[TASK_xxx]]
project: [[ProjectName]]
---

# RESEARCH_主题_YYYYMMDD

## 研究问题
<!-- 要回答的核心问题 -->

## 背景
<!-- 研究背景和上下文 -->

## 发现
<!-- 主要研究发现 -->

## 分析
<!-- 深入分析 -->

## 结论
<!-- 研究结论 -->

## 建议
<!-- 可落地的行动建议 -->

## 参考资料
- [来源1](url)
- [来源2](url)
```

## Constraints

- 必须包含可落地建议
- 禁止直接当作知识库使用
- 完成后建议触发 `/knowledge` 沉淀知识
- 若来源为 Inbox，必须完成归档并从 Inbox 移除原文件

## Next Steps

- `/knowledge` - 从研究中抽象知识模型
- `/task` - 根据建议创建任务
- `/project` - 根据建议创建项目
