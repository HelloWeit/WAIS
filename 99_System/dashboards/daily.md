# PAIOS Dashboard - Daily View

## Today's Plan

```dataview
LIST
FROM "10_Daily"
WHERE type = "plan" AND created = date(today)
```

## Today's Brief

```dataview
LIST
FROM "10_Daily"
WHERE type = "brief" AND created = date(today)
```

## Recent Reviews

```dataview
LIST
FROM "10_Daily"
WHERE type = "review"
SORT created DESC
LIMIT 7
```

## Week at a Glance

```dataview
TABLE
  type as "Type",
  created as "Date"
FROM "10_Daily"
WHERE created >= date(today) - dur(7 days)
SORT created DESC
```
