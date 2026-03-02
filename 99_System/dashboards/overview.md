# WIS Dashboard - Task Overview

```dataview
TABLE
  priority as "P",
  status as "Status",
  project as "Project",
  due as "Due"
FROM "20_Tasks"
WHERE status != "archived"
SORT priority ASC, due ASC
```

## Active Tasks (≤3)

```dataview
LIST
FROM "20_Tasks"
WHERE status = "active"
SORT priority ASC
```

## Blocked Tasks

```dataview
LIST
FROM "20_Tasks"
WHERE status = "blocked"
SORT updated DESC
```

## Recent Drafts

```dataview
LIST
FROM "20_Tasks"
WHERE status = "draft"
SORT created DESC
LIMIT 10
```
