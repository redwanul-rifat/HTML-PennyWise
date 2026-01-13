# Update Notion Tickets via Curl

## Prompt Template

```
Update ticket [PAGE_ID] status to [STATUS]
```

Or:

```
Add comment to ticket [PAGE_ID]: [COMMENT_TEXT]
```

## Description

Update ticket status and add comments to Notion tickets using curl commands. Works independently of the MCP server.

## Prerequisites

1. **NOTION_API_KEY** must be set in `.env` file or environment variable
2. **Page ID** of the ticket to update

## Update Status

### Set to "In Progress"

```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "properties": {
      "Status": {
        "status": {
          "name": "In Progress"
        }
      }
    }
  }'
```

### Set to "In Review"

```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "properties": {
      "Status": {
        "status": {
          "name": "In Review"
        }
      }
    }
  }'
```

### Set to "Done"

```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "properties": {
      "Status": {
        "status": {
          "name": "Done"
        }
      }
    }
  }'
```

### Set to "Blocked"

```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "properties": {
      "Status": {
        "status": {
          "name": "Blocked"
        }
      }
    }
  }'
```

## Add Comment

### Simple Comment

```bash
curl -s -X POST "https://api.notion.com/v1/comments" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {
      "page_id": "[PAGE_ID]"
    },
    "rich_text": [
      {
        "text": {
          "content": "Your comment text here"
        }
      }
    ]
  }'
```

### Implementation Complete Comment

```bash
curl -s -X POST "https://api.notion.com/v1/comments" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {
      "page_id": "[PAGE_ID]"
    },
    "rich_text": [
      {
        "text": {
          "content": "Implementation complete.\n\nFiles modified:\n- file1.ts\n- file2.ts\n\nChanges:\n- Description of changes\n\nTesting:\n- Tested locally"
        }
      }
    ]
  }'
```

## Update Multiple Properties

### Status + Comment Field

```bash
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "properties": {
      "Status": {
        "status": {
          "name": "In Review"
        }
      },
      "Comment": {
        "rich_text": [
          {
            "text": {
              "content": "Implementation complete - ready for review"
            }
          }
        ]
      }
    }
  }'
```

## Retrieve Comments

### Get All Comments on a Page

```bash
curl -s -X GET "https://api.notion.com/v1/comments?block_id=[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28"
```

## Workflow: Fix a Ticket

### Step 1: Start Work

```bash
# Set status to "In Progress"
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"status": {"name": "In Progress"}}}}'
```

### Step 2: Implement Changes

(Make code changes in the codebase)

### Step 3: Complete Work

```bash
# Set status to "In Review"
curl -s -X PATCH "https://api.notion.com/v1/pages/[PAGE_ID]" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"status": {"name": "In Review"}}}}'

# Add implementation comment
curl -s -X POST "https://api.notion.com/v1/comments" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "parent": {"page_id": "[PAGE_ID]"},
    "rich_text": [{"text": {"content": "Implementation complete.\n\nFiles: src/file.ts\nChanges: Fixed the bug\nTested: Yes"}}]
  }'
```

## Response Handling

### Success Response

```json
{
  "object": "page",
  "id": "page-id-here",
  "properties": {
    "Status": {
      "status": {
        "name": "In Progress"
      }
    }
  }
}
```

### Error Response

```json
{
  "object": "error",
  "status": 400,
  "code": "validation_error",
  "message": "Status is not a property that exists"
}
```

## Status Values Reference

| Status | Description |
|--------|-------------|
| **Not Started** | Ready to be worked on |
| **In Progress** | Currently being worked on |
| **In Review** | Implementation complete, needs review |
| **Blocked** | Cannot proceed due to dependency |
| **Done** | Completed and verified |

## Troubleshooting

### "Could not find property"
- Ensure "Status" property exists and is type "status" (not "select")
- Property names are case-sensitive

### "Validation error"
- Check status value matches exactly (e.g., "In Progress" not "in progress")
- Verify page_id format (UUID with or without dashes)

### "Object not found"
- Verify page_id is correct
- Ensure integration has access to the page

## Related

- [notion-curl-review.md](./notion-curl-review.md) - Review tickets via curl
- [fix-all-by-status.md](./fix-all-by-status.md) - Fix all tickets sequentially
- [fix-single.md](./fix-single.md) - Fix a single ticket