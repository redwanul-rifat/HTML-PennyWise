# Fix All Tickets by Status

## Prompt Template

```
Fix all tickets with status "[STATUS]" for database [DATABASE_ID]
```

## Description

Processes and fixes all tickets with a specific status, one by one sequentially. Each ticket goes through the full fix workflow before moving to the next.

## Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `DATABASE_ID` | Yes | - | The Notion database ID (32-character hex string) |
| `STATUS` | No | "Not Started" | The status to filter tickets by |

## Workflow

```
1. FETCH TICKETS
   └── Query database with status filter
   └── Sort by Priority (Critical → Low)
   └── Store ticket list

2. DISPLAY OVERVIEW
   └── Show total count
   └── List all tickets to be processed
   └── Confirm to proceed

3. FOR EACH TICKET (sequential):
   │
   ├── 3a. SET IN PROGRESS
   │   └── Update Status: "[STATUS]" → "In Progress"
   │
   ├── 3b. ANALYZE
   │   └── Parse ticket title for intent
   │   └── Extract requirements from Comment/Description
   │   └── Identify mentioned files, components, features
   │
   ├── 3c. EXPLORE CODEBASE
   │   └── Search for relevant files
   │   └── Read existing implementations
   │   └── Understand context
   │
   ├── 3d. IMPLEMENT
   │   └── Make targeted code changes
   │   └── Follow existing patterns
   │   └── Run tests if applicable
   │
   ├── 3e. COMPLETE
   │   └── Update Status: "In Progress" → "In Review"
   │   └── Add comment with implementation details
   │
   └── 3f. LOG PROGRESS
       └── Mark ticket as done in progress tracker
       └── Show "[X/N] completed"

4. HANDLE ERRORS
   └── If blocked: Set status to "Blocked", add comment
   └── Log error and continue to next ticket (or stop)
   └── User can resume with "Continue fixing tickets"

5. FINAL SUMMARY
   └── Show total processed
   └── List completed tickets
   └── List blocked/failed tickets
   └── Suggest git commit for all changes
```

## Example Usage

### Default (Not Started)
```
Fix all tickets with status "Not Started" for database 12345678-1234-1234-1234-123456789abc
```

### Blocked Tickets
```
Fix all tickets with status "Blocked" for database 12345678-1234-1234-1234-123456789abc
```

### With Team Filter
```
Fix all tickets with status "Not Started" for database [DATABASE_ID]
Filter: Team = "Full-Stack"
```

### Continue After Interruption
```
Continue fixing tickets
```

## Curl Commands

### Get API Key from .env
```bash
NOTION_API_KEY=$(grep -E "^NOTION_API_KEY=" .env | cut -d'=' -f2)
```

### Query Tickets by Status
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

### Query with Team Filter
```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "filter": {
      "and": [
        {"property": "Status", "status": {"equals": "Not Started"}},
        {"property": "Team", "select": {"equals": "Full-Stack"}}
      ]
    },
    "sorts": [{"property": "Priority", "direction": "ascending"}],
    "page_size": 100
  }'
```

### Set Status to In Progress
```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"status": {"name": "In Progress"}}}}'
```

### Set Status to In Review
```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"status": {"name": "In Review"}}}}'
```

### Set Status to Blocked
```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"status": {"name": "Blocked"}}}}'
```

### Add Comment
```bash
curl -s -X POST "https://api.notion.com/v1/comments" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {"page_id": "[PAGE_ID]"},
    "rich_text": [{"text": {"content": "[COMMENT_TEXT]"}}]
  }'
```

## API Filter

### Default (Not Started)
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

### With Team Filter
```json
{
  "filter": {
    "and": [
      {
        "property": "Status",
        "status": {
          "equals": "Not Started"
        }
      },
      {
        "property": "Team",
        "select": {
          "equals": "Full-Stack"
        }
      }
    ]
  },
  "sorts": [
    {
      "property": "Priority",
      "direction": "ascending"
    }
  ]
}
```

## Output Format

### Starting
```
Found [N] tickets with status "Not Started":

1. [CRITICAL] Fix authentication bug - ID: a1b2c3d4...
2. [HIGH] Implement search - ID: e5f67890...
3. [MEDIUM] Update styles - ID: abcd1234...

Starting sequential processing...
```

### Progress (Per Ticket)
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[1/3] Processing: Fix authentication bug
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Status: Not Started → In Progress
Analyzing requirements...
Found relevant files: src/auth/login.ts, src/utils/validation.ts
Implementing fix...
Status: In Progress → In Review
Comment added.

[1/3] COMPLETED
```

### Final Summary
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BATCH PROCESSING COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Total: 3 tickets processed

Completed (2):
  - Fix authentication bug
  - Update styles

Blocked (1):
  - Implement search (missing API docs)

Files Modified:
  - src/auth/login.ts
  - src/utils/validation.ts
  - src/styles/main.css

Suggested commit:
  fix: resolve multiple tickets (auth bug, styles update)
```

### Blocked/Error
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[2/3] BLOCKED: Implement search
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Reason: Missing API endpoint documentation
Status: In Progress → Blocked
Comment added with clarification request.

Continuing to next ticket...
```

## Status Transitions

| From | To | Trigger |
|------|-----|---------|
| Not Started | In Progress | Ticket picked for processing |
| Blocked | In Progress | Ticket picked for retry |
| In Progress | In Review | Implementation complete |
| In Progress | Blocked | Cannot proceed |

## Options

### Stop on First Error
```
Fix all tickets with status "Not Started" for database [DATABASE_ID]
Option: Stop on error
```

### Skip Confirmation
```
Fix all tickets with status "Not Started" for database [DATABASE_ID]
Option: Auto-confirm
```

### Dry Run
```
Fix all tickets with status "Not Started" for database [DATABASE_ID]
Option: Dry run (show plan only)
```

## Related

- [fix-single.md](./fix-single.md) - Fix a single ticket
- [review-all.md](./review-all.md) - Review all tickets first
- [filter-by-team.md](./filter-by-team.md) - Filter by team
- [filter-by-project.md](./filter-by-project.md) - Filter by project