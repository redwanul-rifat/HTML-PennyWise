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

## Implementation Notes

### Updating Status via API

```python
import urllib.request
import json
import os

def update_ticket_status(page_id, status):
    url = f'https://api.notion.com/v1/pages/{page_id}'
    headers = {
        'Authorization': f'Bearer {os.environ["NOTION_API_KEY"]}',
        'Notion-Version': '2022-06-28',
        'Content-Type': 'application/json'
    }
    data = json.dumps({
        'properties': {
            'Status': {
                'status': {'name': status}
            }
        }
    }).encode('utf-8')

    req = urllib.request.Request(url, data=data, headers=headers, method='PATCH')
    with urllib.request.urlopen(req) as response:
        return json.loads(response.read().decode('utf-8'))
```

### Adding Comment via API

```python
def add_comment(page_id, comment_text):
    url = 'https://api.notion.com/v1/comments'
    headers = {
        'Authorization': f'Bearer {os.environ["NOTION_API_KEY"]}',
        'Notion-Version': '2022-06-28',
        'Content-Type': 'application/json'
    }
    data = json.dumps({
        'parent': {'page_id': page_id},
        'rich_text': [{
            'type': 'text',
            'text': {'content': comment_text}
        }]
    }).encode('utf-8')

    req = urllib.request.Request(url, data=data, headers=headers, method='POST')
    with urllib.request.urlopen(req) as response:
        return json.loads(response.read().decode('utf-8'))
```

## Related

- [notion-ticket-reviewer skill](../skills/notion-ticket-reviewer/SKILL.md)
- [ticket-fixer agent](../agents/ticket-fixer.md)
