---
skill_name: notion-ticket-reviewer
applies_to_local_project_only: false
auto_trigger_regex:
    [notion ticket, review ticket, notion task, ticket reviewer, /notion-review, notion database, fix ticket]
tags: [notion, tickets, automation, review, curl, workflow]
related_skills: []
---

# Notion Ticket Reviewer

Automatically fetch, analyze, fix, and update tickets from Notion databases using Claude Code.

---

## Overview

This skill enables Claude Code to:
1. **Fetch tickets** from a Notion database
2. **Filter** by status, priority, team, or project
3. **Analyze requirements** from ticket descriptions
4. **Implement fixes** in the codebase automatically
5. **Update ticket status** to "In Progress" → "In Review"
6. **Add comments** with implementation details

---

## Quick Start

### Review All Tickets
```
Enter plan mode - Review notion tickets for database [YOUR_DATABASE_ID]
```

### Fix a Single Ticket
```
Fix ticket: Fix login validation bug
```
or
```
Fix ticket: a1b2c3d4-e5f6-7890-abcd-ef1234567890
```

### Filter by Team
```
Enter plan mode - Review notion tickets
Filter: Team = "Full-Stack", Status = "Not Started"
```

---

## Workflow: One-by-One Ticket Fixing

### Step 1: List Tickets
```
Enter plan mode - Review notion tickets for database [DATABASE_ID]
```
- Shows all "Not Started" tickets
- Grouped by category (Features, Bug Fixes, Improvements, etc.)
- Displays: Priority, Team, Title, ID

### Step 2: Select & Start Ticket
```
Fix ticket: [ticket title or ID]
```
- Sets status to **"In Progress"**
- Analyzes ticket requirements
- Explores relevant codebase files

### Step 3: Implement
Claude will:
- Read relevant files based on ticket description
- Make necessary code changes
- Follow project coding standards
- Run tests if applicable

### Step 4: Complete
After implementation:
- Sets status to **"In Review"**
- Adds comment with:
  - Files modified
  - Changes made
  - Testing notes
- Optionally creates git commit

### Step 5: Next Ticket
```
Fix next ticket
```
or select another ticket by name/ID

---

## Database Schema (Team Tickets)

### Core Properties

| Property | Type | Values |
|----------|------|--------|
| **Ticket Title** | title | Ticket name/summary |
| **Status** | status | Blocked, Not Started, In Progress, In Review, Done |
| **Priority** | select | Critical, Urgent, High, Medium, Low |
| **Team** | select | Full-Stack, Design, Mobile, Operation |
| **Comment** | rich_text | Additional notes/description |

### Relationship Properties

| Property | Type | Purpose |
|----------|------|---------|
| **Assignee** | relation | Person assigned to ticket |
| **Assigner** | relation | Person who created ticket |
| **Related Project** | relation | Link to project database |

### Date Properties

| Property | Type | Purpose |
|----------|------|---------|
| **Due Date** | date | Deadline |
| **Start Date** | created_time | When ticket was created |
| **End Date** | date | Completion date |
| **Duration** | date | Time range |

### Additional Properties

| Property | Type | Purpose |
|----------|------|---------|
| **Category** | multi_select | Tags for categorization |
| **URL** | url | Reference link |
| **Attachments** | url | File links |
| **Files & media** | files | Uploaded files |

---

## Status Values

| Status | Color | Description |
|--------|-------|-------------|
| **Blocked** | red | Cannot proceed due to dependency |
| **Not Started** | gray | Ready to be worked on |
| **In Progress** | blue | Currently being worked on |
| **In Review** | purple | Implementation complete, needs review |
| **Done** | green | Completed and verified |

---

## Priority Values

| Priority | Color | Description |
|----------|-------|-------------|
| **Critical** | orange | Must fix immediately |
| **Urgent** | purple | Fix today |
| **High** | red | Fix this sprint |
| **Medium** | yellow | Fix when possible |
| **Low** | green | Nice to have |

---

## Filter Examples

### By Status
```python
filter = {
    "property": "Status",
    "status": {"equals": "Not Started"}
}
```

### By Priority
```python
filter = {
    "property": "Priority",
    "select": {"equals": "High"}
}
```

### By Team
```python
filter = {
    "property": "Team",
    "select": {"equals": "Full-Stack"}
}
```

### Combined Filters
```python
filter = {
    "and": [
        {"property": "Status", "status": {"equals": "Not Started"}},
        {"property": "Priority", "select": {"equals": "High"}},
        {"property": "Team", "select": {"equals": "Full-Stack"}}
    ]
}
```

---

## API Reference

### Query Database
```bash
curl -X POST "https://api.notion.com/v1/databases/DATABASE_ID/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"filter": {"property": "Status", "status": {"equals": "Not Started"}}}'
```

### Update Ticket Status
```bash
curl -X PATCH "https://api.notion.com/v1/pages/PAGE_ID" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"properties": {"Status": {"status": {"name": "In Progress"}}}}'
```

### Add Comment
```bash
curl -X POST "https://api.notion.com/v1/comments" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"parent": {"page_id": "PAGE_ID"}, "rich_text": [{"text": {"content": "Implementation complete"}}]}'
```

---

## Prerequisites

### 1. Notion API Key
1. Go to [notion.so/my-integrations](https://www.notion.so/my-integrations)
2. Create new integration
3. Copy the Internal Integration Secret (starts with `ntn_` or `secret_`)

### 2. Add to .env File
Add your API key to the project's `.env` file:
```
NOTION_API_KEY=ntn_your_key_here
```

### 3. Share Database
1. Open your Notion database
2. Click "..." → "Add connections"
3. Select your integration

### 4. Test Connection
```bash
NOTION_API_KEY=$(grep -E "^NOTION_API_KEY=" .env | cut -d'=' -f2)
curl -s -X GET "https://api.notion.com/v1/users/me" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28"
```

---

## Troubleshooting

### "API token is invalid"
1. Check `NOTION_API_KEY` in `.env` file
2. Verify key starts with `ntn_` or `secret_`
3. Regenerate key at notion.so/my-integrations if needed

### "Database not found"
1. Verify database ID is correct (32 hex chars)
2. Ensure integration has access to the database
3. Re-share database with integration

### "Status update failed"
1. Verify "Status" property exists
2. Check status option names match exactly
3. Ensure property type is "Status" (not "Select")

### Test curl connection
```bash
NOTION_API_KEY=$(grep -E "^NOTION_API_KEY=" .env | cut -d'=' -f2)
curl -s -X GET "https://api.notion.com/v1/users/me" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28"
```

---

## Related Files

- `databases/example-config.json` - Database configuration template
- `prompts/review-tickets.md` - Review tickets via curl
- `prompts/update-ticket.md` - Update ticket status via curl
- `prompts/fix-single.md` - Fix single ticket prompt
- `prompts/fix-all-by-status.md` - Fix all tickets by status
- `prompts/filter-by-team.md` - Filter by team prompt
- `prompts/filter-by-project.md` - Filter by project prompt

---

## Example Session

```
User: Enter plan mode - Review notion tickets for database [YOUR_DATABASE_ID]

Claude: Found 15 tickets:

### Features
1. [HIGH] Fix login validation bug - ID: a1b2c3d4...
2. [HIGH] Implement search functionality - ID: e5f67890...

### Bug Fixes
3. [HIGH] Resolve API timeout issue - ID: abcd1234...
...

User: Fix ticket: Fix login validation bug

Claude:
1. Setting status to "In Progress"...
2. Reading ticket description...
3. Analyzing requirements:
   - Fix form validation on empty fields
4. Exploring codebase for relevant files...
5. Found: src/components/LoginForm.tsx...
6. Implementing fix...
7. Setting status to "In Review"
8. Adding implementation comment

Done! Ticket ready for review.
```
