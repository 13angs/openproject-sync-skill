---
name: openproject-sync
description: Manage OpenProject work packages — list open WPs, create new WP, update status, set priority. Requires OpenProject URL and API key as secret.
metadata:
  require-secret: true
  require-secret-description: "OpenProject credentials in format: https://your-op-url.com::your-api-key"
---

# OpenProject Sync Skill

Manage work packages in OpenProject CE via REST API.

## Secret Format

Secret must be: `<base_url>::<api_key>`

Example: `https://openproject.example.com::abc123xyz`

## Available Actions

Call this skill with a JSON object specifying the action and parameters.

### list — List open work packages
```json
{
  "action": "list",
  "project_id": 404
}
```
Returns: array of work packages with id, subject, status, priority, assignee.

### list-query — List WPs from saved query
```json
{
  "action": "list-query",
  "query_id": 123
}
```

### get — Get single work package
```json
{
  "action": "get",
  "wp_id": 456
}
```

### create — Create new work package
```json
{
  "action": "create",
  "project_id": 404,
  "subject": "Task title here",
  "type_id": 1
}
```

### update — Update WP status
```json
{
  "action": "update",
  "wp_id": 456,
  "status_id": 7,
  "note": "Optional journal note"
}
```

### priority — Set WP priority
```json
{
  "action": "priority",
  "wp_id": 456,
  "priority_id": 9
}
```

## Priority IDs
- 7 = Don't Do Yet
- 8 = Do Next
- 9 = Do Now
- 10 = Done

## Status IDs (common)
- 1 = New
- 7 = In Progress
- 12 = Closed

## Notes
- All text (Thai included) safe to send in subject/note fields
- Milestone WPs use `date` field, not `startDate`/`dueDate`
- LockVersion handled automatically on update
