# Fix Ticket Command

Fix a single Notion ticket by analyzing requirements and implementing changes.

## Usage

```
/fix-ticket [ticket-id-or-title]
```

or

```
Fix ticket: [ticket title or ID]
```

## Arguments

| Argument | Required | Description |
|----------|----------|-------------|
| ticket-id-or-title | Yes | The Notion page ID or ticket title to fix |

## Workflow

### 1. Find Ticket
- Search by ID (UUID format) or title (partial match)
- Retrieve full ticket details from Notion

### 2. Update Status
- Set status to **"In Progress"**
- This signals to others that work has started

### 3. Analyze Requirements
Extract from ticket:
- Title: What needs to be done
- Description/Comment: Detailed requirements
- Related files mentioned
- Acceptance criteria (if any)

### 4. Explore Codebase
- Search for relevant files based on ticket description
- Read existing implementations
- Understand current architecture

### 5. Implement Fix
- Make necessary code changes
- Follow project coding standards
- Run tests if applicable

### 6. Complete Ticket
- Set status to **"In Review"**
- Add comment with:
  - Files modified
  - Changes made
  - Testing notes
  - Any blockers or notes for reviewer

### 7. Optional: Create Commit
```
git commit -m "fix: [ticket title]

Notion Ticket: https://notion.so/[ticket-id]
"
```

## Examples

### By Title
```
Fix ticket: Fix login validation bug
```

### By ID
```
Fix ticket: a1b2c3d4-e5f6-7890-abcd-ef1234567890
```

### With Plan Mode
```
Enter plan mode - Fix ticket: Add loading spinner to dashboard
```

## Status Flow

```
Not Started → In Progress → In Review → Done
                  ↓
               Blocked
```

## Curl Commands

### Get API Key from .env
```bash
NOTION_API_KEY=$(grep -E "^NOTION_API_KEY=" .env | cut -d'=' -f2)
```

### Search for Ticket by Title
```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"filter": {"property": "Ticket Title", "title": {"contains": "[SEARCH_TERM]"}}}'
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

## Related

- [notion-ticket-reviewer skill](../skills/notion-ticket-reviewer/SKILL.md)
- [ticket-fixer agent](../agents/ticket-fixer.md)
