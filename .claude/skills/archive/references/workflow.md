# Archive Agent Skill

## 目标

归档完成的任务和项目，处理过的 Inbox 项目，保持活跃空间整洁同时保留历史记录。

---

## Step 1: 识别待归档项目

1. **搜索完成的任务：**
   - 查找 `20_Tasks/` 中 `status: done` 的文件

2. **搜索完成的项目：**
   - 查找 `30_Projects/` 中 `status: done` 的文件

3. **搜索已处理的 Inbox 项目：**
   - 查找 `00_Inbox/` 中 `status: processed` 的文件

4. **展示发现（使用 AskUserQuestion）：**

```
## 待归档项目

**已完成任务 ([N]):**
- [[TASK_xxx]] - 完成于 [date]
- [[TASK_yyy]] - 完成于 [date]

**已完成项目 ([N]):**
- [[Project1]] - 完成于 [date]
- [[Project2]] - 完成于 [date]

**已处理收件箱 ([N]):**
- 关于X的想法 - 已转为 [[TASK_xxx]]
- 关于Y的笔记 - 处理于 [date]

请选择归档方式:
1. 全部归档
2. 仅归档任务
3. 仅归档项目
4. 仅归档收件箱
5. 选择特定项目
```

---

## Step 2: 归档流程

### 对于任务

1. **读取任务文件**
2. **移动到归档：**
   - 路径：`90_Archive/Tasks/YYYY/TASK_*.md`
   - 按完成年份组织
3. **更新元数据：**
   - 添加 `archived: YYYY-MM-DD`

### 对于项目

1. **读取项目文件**
2. **移动到归档：**
   - 单文件：`90_Archive/Projects/YYYY/ProjectName.md`
   - 文件夹：`90_Archive/Projects/YYYY/ProjectName/`
3. **更新元数据：**
   - 添加 `archived: YYYY-MM-DD`

### 对于 Inbox 项目

1. **移动到归档：**
   - 路径：`90_Archive/Inbox/YYYY/MM/filename.md`
   - 按处理年月组织
2. **保留历史捕获时间线**

---

## Step 3: 总结报告

```
## 归档完成

**已归档 [N] 个任务至 `90_Archive/Tasks/YYYY/`:**
- [[TASK_xxx]] → 归档/Tasks/2026/
- [[TASK_yyy]] → 归档/Tasks/2026/

**已归档 [N] 个项目至 `90_Archive/Projects/YYYY/`:**
- [[Project1]] → 归档/Projects/2026/

**已归档 [N] 个收件箱条目至 `90_Archive/Inbox/YYYY/MM/`:**
- idea-note.md → 归档/Inbox/2026/02/

**库状态:**
- 活跃任务: [N]
- 活跃项目: [N]
- 收件箱条目: [N]
- 已归档任务 (总计): [N]
- 已归档项目 (总计): [N]

**建议:**
- [ ] 检查 blocked 状态的任务是否需要推进
- [ ] 处理剩余收件箱条目
```

---

## 归档目录结构

```
90_Archive/
├── Tasks/
│   └── 2026/
│       ├── TASK_20260228_xxx.md
│       └── TASK_20260215_yyy.md
├── Projects/
│   └── 2026/
│       ├── ProjectName.md
│       └── AnotherProject/
│           ├── AnotherProject.md
│           └── assets/
└── Inbox/
    ├── 2026/
    │   ├── 01/
    │   │   └── processed-idea.md
    │   └── 02/
    │       └── another-note.md
```

---

## 约束

- **保留所有内容** - 永不删除，只移动
- **按年份组织** - 使用完成年份进行文件夹组织
- **更新 frontmatter** - 添加归档日期
- **归档前确认** - 让用户审查将被归档的内容
- **维护链接** - Obsidian wikilinks 跨位置工作
- **记录操作** - 更新今日 daily note

---

## CLI 用法

```bash
/archive          # 查看待归档项目
/archive all      # 归档所有
/archive tasks    # 仅归档任务
/archive projects # 仅归档项目
/archive inbox    # 仅归档收件箱
```

---

## 边界情况

- **无完成任务：** 检查是否有 blocked 状态的任务需要推进
- **文件夹中混合状态：** 询问用户 - 归档整个文件夹还是仅某些文件？
- **有资源的大型项目：** 确认是否也归档资源
- **最近完成：** 提醒用户可能想先做项目回顾
