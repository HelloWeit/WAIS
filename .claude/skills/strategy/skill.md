---
name: strategy
description: 判断战略方向是否偏移，识别结构性机会，保持项目与战略对齐。Use when user says "/strategy", "战略", "方向", or wants to review strategic alignment.
---

# Strategy Skill

战略对齐检查工具，判断方向是否偏移，识别结构性机会。

## When to Use

- 用户说 "/strategy", "战略", "方向"
- 需要审视当前工作是否与战略对齐
- 识别新的战略机会

## Input

| Field | Required | Description |
|-------|----------|-------------|
| context | No | 当前上下文或困惑 |
| period | No | 审视周期（周/月/季） |

## Scan Directories

| Directory | Purpose |
|-----------|---------|
| `70_Strategy/` | 战略方向文件 |
| `30_Projects/` | 活跃项目 |
| `20_Tasks/` | 活跃任务 |

## Output

```
70_Strategy/
└── STRATEGY_主题_YYYYMMDD.md
```

## Workflow

1. **扫描战略文件**
   - 读取现有战略方向
   - 识别核心战略目标

2. **检查对齐情况**
   - 扫描项目和任务
   - 判断是否与战略对齐

3. **识别偏差**
   - 标记偏离战略的工作
   - 识别资源错配

4. **发现机会**
   - 识别结构性机会
   - 提出战略建议

5. **生成报告**
   - 输出战略审视报告

## Template

```markdown
---
type: strategy
period: [周/月/季]
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [战略]
---

# STRATEGY_主题_YYYYMMDD

## 核心战略
<!-- 当前核心战略方向 -->

## 对齐检查
| Project | Strategy | Aligned? |
|---------|----------|----------|
| ProjectA | Strategy1 | ✅ |
| ProjectB | Strategy2 | ⚠️ |

## 偏差分析
<!-- 识别的偏差和问题 -->

## 结构性机会
1. <!-- 机会 1 -->
2. <!-- 机会 2 -->

## 建议
- <!-- 战略建议 -->

## 行动
- [ ] <!-- 调整行动 -->
```

## Constraints

- **战略层级**：不写执行细节
- **不写任务**：只做战略层面的分析
- **链接项目**：所有项目必须链接到战略

## Best Practice

定期（每周/每月）运行 `/strategy` 进行战略审视。
