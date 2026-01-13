# Fix Single Ticket

## Prompt Template

```
Fix ticket: [TICKET_TITLE_OR_ID]
```

## Description

Analyzes a single ticket, implements the fix in the codebase, and updates the ticket status with implementation details.

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `TICKET_TITLE_OR_ID` | Yes | The ticket title (partial match) or page ID |

## Workflow

```
1. FIND TICKET
   └── Search by title or ID via curl
   └── Fetch ticket details from Notion API

2. SET IN PROGRESS
   └── Update Status via curl: "Not Started" → "In Progress"

3. ANALYZE
   └── Parse ticket title for intent
   └── Extract requirements from Comment/Description
   └── Identify mentioned files, components, features

4. EXPLORE CODEBASE
   └── Search for relevant files
   └── Read existing implementations
   └── Understand context

5. IMPLEMENT
   └── Make targeted code changes
   └── Follow existing patterns
   └── Run tests if applicable

6. COMPLETE
   └── Update Status via curl: "In Progress" → "In Review"
   └── Add comment via curl with implementation details
   └── Suggest git commit message
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

### Add Comment
```bash
curl -s -X POST "https://api.notion.com/v1/comments" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"parent": {"page_id": "[PAGE_ID]"}, "rich_text": [{"text": {"content": "[COMMENT_TEXT]"}}]}'
```

## Example Usage

### By Title
```
Fix ticket: Fix login validation bug
```

### By ID
```
Fix ticket: a1b2c3d4-e5f6-7890-abcd-ef1234567890
```

### With Context
```
Fix ticket: Fix login validation bug
Context: Users report validation not triggering on empty fields
```

## Output Format

### Success
```
Ticket Fixed: [Title]
Status: Not Started → In Progress → In Review

Files Modified:
- src/components/LoginForm.tsx
- src/utils/validation.ts

Changes:
- Fixed validation trigger on empty fields
- Added proper error messages
- Updated form submission handling

Comment Added: Yes
Commit Suggested: fix: resolve login form validation issue
```

### Blocked
```
Ticket Blocked: [Title]
Status: Not Started → Blocked

Reason: Missing API endpoint documentation

Action Required:
- Clarify expected API response format
- Confirm authentication requirements

Comment Added: Yes (with clarification request)
```

## Status Transitions

| From | To | Trigger |
|------|-----|---------|
| Not Started | In Progress | `Fix ticket:` command |
| In Progress | In Review | Implementation complete |
| In Progress | Blocked | Cannot proceed |
| Blocked | In Progress | Issue resolved |

## Comment Template

When completing a ticket, the following comment is added:

```
## Implementation Complete

**Files Modified:**
- [file1.ts]
- [file2.tsx]

**Changes:**
- [Change 1 description]
- [Change 2 description]

**Testing:**
- [Test notes or N/A]

**Commit:** `fix: [commit message suggestion]`

---
*Updated by Claude Code*
```

## Related

- [review-tickets.md](./review-tickets.md) - Review all tickets
- [update-ticket.md](./update-ticket.md) - Update ticket status
- [fix-all-by-status.md](./fix-all-by-status.md) - Fix all tickets by status
- [../../../commands/fix-ticket.md](../../../commands/fix-ticket.md) - Full command documentation
