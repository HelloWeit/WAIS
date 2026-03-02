# WAIS Dashboard - System Health

## Active Task Count

```dataview
TABLE length(rows) as "Count"
FROM "20_Tasks"
WHERE status = "active"
GROUP BY true
```

**Rule: Active ≤ 3**

## P0 Tasks

```dataview
LIST
FROM "20_Tasks"
WHERE priority = "P0" AND status != "done" AND status != "archived"
```

**Rule: P0 ≤ 1**

## Stale Tasks (7+ days no update)

```dataview
LIST
FROM "20_Tasks"
WHERE status != "done" AND status != "archived"
  AND date(today) - file.mtime >= dur(7 days)
SORT file.mtime ASC
```

## Unprocessed Inbox Items

```dataview
LIST
FROM "00_Inbox"
WHERE status != "processed"
SORT created DESC
```

**Rule: 48h must process**
