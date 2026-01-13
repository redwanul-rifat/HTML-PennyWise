# Review All Tickets

## Prompt Template

```
Enter plan mode - Review notion tickets for database [DATABASE_ID]
```

## Description

Fetches all tickets from a Notion database and presents them grouped by category, priority, or status.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `DATABASE_ID` | Yes | The Notion database ID (32-character hex string) |

## Default Filter

- Status: **Not Started** (ready to work on)
- Sorted by: Priority (Critical → Low)

## Output Format

```
Found [N] tickets:

### [Category 1]
1. [PRIORITY] Title - ID: xxx...
2. [PRIORITY] Title - ID: xxx...

### [Category 2]
1. [PRIORITY] Title - ID: xxx...
...
```

## Example Usage

### Basic Review
```
Enter plan mode - Review notion tickets for database [YOUR_DATABASE_ID]
```

### With Status Filter
```
Enter plan mode - Review notion tickets for database [YOUR_DATABASE_ID]
Filter: Status = "Blocked"
```

### With Priority Filter
```
Enter plan mode - Review notion tickets for database [YOUR_DATABASE_ID]
Filter: Priority = "Critical" OR "Urgent"
```

## Curl Commands

### Get API Key from .env
```bash
NOTION_API_KEY=$(grep -E "^NOTION_API_KEY=" .env | cut -d'=' -f2)
```

### Query Database
```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "filter": {
      "property": "Status",
      "status": {"equals": "Not Started"}
    },
    "sorts": [{"property": "Priority", "direction": "ascending"}],
    "page_size": 100
  }'
```

### With Status Filter
```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "filter": {
      "property": "Status",
      "status": {"equals": "Blocked"}
    },
    "page_size": 100
  }'
```

## API Filter Reference

```json
{
  "filter": {
    "property": "Status",
    "status": {
      "equals": "Not Started"
    }
  },
  "sorts": [
    {
      "property": "Priority",
      "direction": "ascending"
    }
  ]
}
```

## Next Steps After Review

After reviewing tickets, you can:
1. Fix a specific ticket: `Fix ticket: [title or ID]`
2. Filter further: Add team or project filter
3. Export: Request a summary or export

## Related

- [fix-single.md](./fix-single.md) - Fix a single ticket
- [filter-by-team.md](./filter-by-team.md) - Filter by team
- [filter-by-project.md](./filter-by-project.md) - Filter by project
