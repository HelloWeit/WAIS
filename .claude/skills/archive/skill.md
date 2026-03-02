---
name: archive
description: 归档完成的任务、项目和已处理的 Inbox 项目，按年份组织存储。Use when user says "/archive", "归档", "清理", or needs to clean up completed items.
---

# Archive Skill

归档已完成的任务、项目和已处理的 Inbox 项目，保持工作区整洁。

## When to Use

- 用户说 "/archive", "归档", "清理"
- 需要整理已完成的工作项
- 定期清理工作区

## Scan Directories

| Directory | Filter |
|-----------|--------|
| `30_Tasks/` | status: done |
| `20_Projects/` | status: done |
| `00_Inbox/` | status: processed |

## Output Directories

```
90_Archive/
├── Tasks/
│   └── YYYY/
│       └── TASK_*.md
├── Projects/
│   └── YYYY/
│       └── *.md
└── Inbox/
    └── YYYY/
        └── MM/
            └── *.md
```

## Workflow

1. 扫描符合归档条件的文件
2. 列出待归档项目，征求用户确认
3. 移动文件到对应归档目录
4. 更新 frontmatter 添加 `archived: YYYY-MM-DD`

## Constraints

- **保留所有内容，永不删除**
- 按年份组织归档
- 归档前必须用户确认
- 更新 frontmatter 记录归档日期
