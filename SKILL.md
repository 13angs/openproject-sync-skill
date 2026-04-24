---
name: openproject-sync
description: Manage OpenProject work packages — list open WPs, create new WP, update status, set priority.
---

# OpenProject Sync

## Instructions

Call the `run_js` tool using `index.html` and a JSON string for `data` with the following fields:
- **action**: Required. One of `"list"`, `"list-query"`, `"get"`, `"create"`, `"update"`, `"priority"`.
- **op_url**: Required. The OpenProject base URL (e.g., `"https://openproject.example.com"`).
- **op_api_key**: Required. The OpenProject API key from My Account > API Access Token.
- **project_id**: Required for `list` and `create`. Numeric project ID.
- **query_id**: Required for `list-query`. Saved query ID.
- **wp_id**: Required for `get`, `update`, `priority`. Work package ID.
- **subject**: Required for `create`. Title of the new work package.
- **type_id**: Optional for `create`. Default is `1`.
- **status_id**: Required for `update`. `1`=New, `7`=In Progress, `12`=Closed.
- **priority_id**: Required for `priority`. `7`=Don't Do Yet, `8`=Do Next, `9`=Do Now, `10`=Done.
- **note**: Optional for `update`. Journal comment text.

**Constraints:**
- Always call `run_js` — never try to call the OpenProject API directly.
- If `op_url` or `op_api_key` are not known, ask the user before calling the tool.
- After a successful `create` or `update`, confirm the result to the user with WP id and subject/status.
- Priority IDs: 7=Don't Do Yet · 8=Do Next · 9=Do Now · 10=Done
- Status IDs: 1=New · 7=In Progress · 12=Closed
