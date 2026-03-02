# Task Agent Skill

## 目标

把「想法/brief 行动点/会议输入」转成 **标准任务文件**，并写入 `vault/30_Tasks/`。

## 输入（用户一句话 + 可选上下文）

- 必填：任务一句话描述（自然语言）
- 可选：
  - 来源引用：某条 brief、某条 inbox、某个项目
  - 期望产出：文档/方案/Demo/PPT/排查结论
  - 优先级倾向：P0/P1/P2

## 输出（文件落盘）

- 目录：`30_Tasks/`
- 文件名：`TASK_YYYYMMDD_短标题.md`
  - 短标题规则：中文不超过 12 字；含空格用 `-`；避免"关于/一些/整理"
- YAML 必须包含：

```yaml
---
type: task
status: draft
priority: P1
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
source: manual|brief|meeting|inbox|agent
project: ""            # 可空；建议是 [[20_Projects/xxx]]
due: ""                # 可空；YYYY-MM-DD
---
```

## Inbox 后处理（来源为 inbox 时必须执行）

- 更新源文件 frontmatter：`status: processed`, `archived: YYYY-MM-DD`
- 移动源文件到 `90_Archive/Inbox/YYYY/MM/`
- 移动后 `00_Inbox/` 不再保留该原文件

## 正文结构（固定）

```markdown
# <任务标题>

## Intent（要解决什么）
- ...

## Output（交付物）
- ...

## Next Actions（下一步最小动作）
- [ ] ...

## Dependencies（依赖/阻塞）
- ...

## Links（关联）
- 来源：...
- 相关：...
```

## 约束（非常重要）

- **不允许**把任务写成长文章
- **不允许**同时创建项目（项目另一个 skill 做）
- **必须**给出 "Next Actions" 至少 1 条，且是可执行动作

## CLI 用法

```
/task <一句话>
/task from:brief <编号/引用> <一句话补充>
```
