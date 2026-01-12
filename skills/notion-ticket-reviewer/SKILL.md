---
skill_name: notion-ticket-reviewer
applies_to_local_project_only: false
auto_trigger_regex:
    [notion ticket, review ticket, notion task, ticket reviewer, /notion-review, notion database]
tags: [notion, tickets, automation, review, mcp, workflow]
related_skills: []
---

# Notion Ticket Reviewer

Automatically fetch, analyze, fix, and update tickets from Notion databases using Claude Code and Notion MCP.

---

## Overview

This skill enables Claude Code to:
1. **Fetch tickets** from a Notion database
2. **Analyze requirements** from ticket descriptions
3. **Implement fixes** in the codebase automatically
4. **Update ticket status** to "Review" when complete
5. **Add comments** with implementation details

---

## Prerequisites

### 1. Notion MCP Server

Ensure Notion MCP is configured in your Claude Code settings:

```json
{
  "mcpServers": {
    "notion": {
      "command": "npx",
      "args": ["-y", "@notionhq/notion-mcp-server"],
      "env": {
        "NOTION_API_KEY": "your-notion-api-key"
      }
    }
  }
}
```

### 2. Notion API Key

1. Go to [Notion Integrations](https://www.notion.so/my-integrations)
2. Create a new integration
3. Copy the API key
4. Add it to your MCP configuration

### 3. Database Access

Share your Notion database with the integration:
1. Open your Notion database
2. Click "..." menu → "Add connections"
3. Select your integration

---

## Quick Start

### Basic Usage

```
User: Review my notion tickets and fix them

Claude: I'll fetch your pending tickets from Notion and work through them.

[Uses Notion MCP to query database]
[Analyzes each ticket]
[Implements fixes]
[Updates ticket status to "Review"]
```

### Command Syntax

```
/notion-review                              # Review all pending tickets
/notion-review database_id=<id>             # Specific database
/notion-review status="To Do"               # Filter by status
/notion-review assignee="John"              # Filter by assignee
```

---

## Workflow

### Step 1: Fetch Tickets

Use Notion MCP to query the database for actionable tickets:

```
MCP Tool: notion_query_database
Parameters:
  database_id: "your-database-id"
  filter: {
    "property": "Status",
    "status": {
      "equals": "To Do"
    }
  }
```

### Step 2: Analyze Requirements

For each ticket, extract:
- **Title**: What needs to be done
- **Description**: Detailed requirements
- **Priority**: Order of execution
- **Acceptance Criteria**: How to verify completion

### Step 3: Implement Changes

Claude Code will:
1. Read relevant files in the codebase
2. Make necessary changes based on ticket requirements
3. Follow project coding standards
4. Run tests if available

### Step 4: Update Ticket Status

After implementation, update the ticket:

```
MCP Tool: notion_update_page
Parameters:
  page_id: "ticket-page-id"
  properties: {
    "Status": {
      "status": {
        "name": "Review"
      }
    }
  }
```

### Step 5: Add Implementation Notes

Optionally add a comment with details:

```
MCP Tool: notion_create_comment
Parameters:
  page_id: "ticket-page-id"
  rich_text: [
    {
      "type": "text",
      "text": {
        "content": "Implementation complete:\n- Files modified: ...\n- Changes made: ...\n- Ready for review"
      }
    }
  ]
```

---

## Database Schema Requirements

### Required Properties

| Property | Type | Purpose |
|----------|------|---------|
| **Title** | Title | Ticket name/summary |
| **Status** | Status | Current state (To Do, In Progress, Review, Done) |
| **Description** | Rich Text | Detailed requirements |

### Recommended Properties

| Property | Type | Purpose |
|----------|------|---------|
| **Priority** | Select | High, Medium, Low |
| **Assignee** | Person | Who's responsible |
| **Due Date** | Date | Deadline |
| **Tags** | Multi-select | Categorization |
| **Project** | Relation | Link to project |

### Status Values

Configure these status options in your database:
- **To Do** - Ready to be worked on
- **In Progress** - Currently being worked on
- **Review** - Implementation complete, needs review
- **Done** - Completed and verified

---

## Notion MCP Tools Reference

### notion_search

Find databases or pages:

```json
{
  "query": "Project Tasks",
  "filter": {
    "property": "object",
    "value": "database"
  }
}
```

### notion_query_database

Query tickets with filters:

```json
{
  "database_id": "abc123",
  "filter": {
    "and": [
      {
        "property": "Status",
        "status": { "equals": "To Do" }
      },
      {
        "property": "Priority",
        "select": { "equals": "High" }
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

### notion_retrieve_page

Get full ticket details:

```json
{
  "page_id": "ticket-page-id"
}
```

### notion_update_page

Update ticket properties:

```json
{
  "page_id": "ticket-page-id",
  "properties": {
    "Status": {
      "status": { "name": "Review" }
    }
  }
}
```

### notion_create_comment

Add implementation notes:

```json
{
  "page_id": "ticket-page-id",
  "rich_text": [
    {
      "type": "text",
      "text": {
        "content": "Changes implemented in commit abc123"
      }
    }
  ]
}
```

---

## Example Workflows

### 1. Review All Pending Tickets

```
User: Review all my notion tickets

Claude: I'll fetch and process your pending tickets.

1. Querying Notion database for tickets with status "To Do"...
   Found 3 tickets:
   - [HIGH] Fix login redirect issue
   - [MEDIUM] Add loading spinner to dashboard
   - [LOW] Update footer copyright year

2. Starting with highest priority: "Fix login redirect issue"
   - Reading ticket description...
   - Analyzing requirements...
   - Implementing fix in auth.routes.ts...
   - Updating ticket status to "Review"...

3. Next: "Add loading spinner to dashboard"
   [continues...]

All tickets processed. Summary:
- 3 tickets moved to "Review"
- Files modified: auth.routes.ts, Dashboard.tsx, Footer.tsx
```

### 2. Process Specific Ticket

```
User: Fix the notion ticket about API error handling

Claude: I'll find and process that specific ticket.

1. Searching for ticket about "API error handling"...
   Found: "Implement proper error handling for API calls"

2. Reading requirements:
   - Add try-catch blocks to all API calls
   - Display user-friendly error messages
   - Log errors to console for debugging

3. Implementing changes:
   - Modified: apiService.ts
   - Modified: ErrorBoundary.tsx
   - Added: errorHandler.ts

4. Updating ticket status to "Review"
5. Adding comment with implementation details

Done! Ticket ready for review.
```

### 3. Filter by Priority

```
User: Only work on high priority notion tickets

Claude: I'll filter for high priority tickets only.

Querying with filter: Priority = "High"
Found 1 ticket: "Critical: Fix production database connection"

[Proceeds to analyze and implement...]
```

---

## Best Practices

### 1. Clear Ticket Descriptions

Write tickets with clear requirements:

```markdown
## Problem
Users cannot login after password reset

## Expected Behavior
After resetting password, users should be able to login immediately

## Acceptance Criteria
- [ ] User can login with new password
- [ ] No "invalid credentials" error
- [ ] Session is created correctly
```

### 2. Use Consistent Status Names

Ensure your database uses these exact status names:
- "To Do"
- "In Progress"
- "Review"
- "Done"

### 3. Include File References

When possible, mention relevant files in the ticket:

```markdown
Files to check:
- src/auth/login.ts
- src/services/authService.ts
```

### 4. Add Context

Include any relevant context:
- Related tickets
- Previous attempts
- Known constraints

---

## Troubleshooting

### "Notion MCP not available"

Ensure MCP server is configured:
1. Check `.claude/settings.json` for notion MCP
2. Verify API key is set
3. Restart Claude Code

### "Database not found"

1. Verify database ID is correct
2. Ensure integration has access to the database
3. Check database is shared with integration

### "Permission denied"

1. Verify API key permissions
2. Re-share database with integration
3. Check integration capabilities in Notion settings

### "Status update failed"

1. Verify "Status" property exists in database
2. Check status option names match exactly
3. Ensure property type is "Status" (not "Select")

---

## Configuration Options

### Environment Variables

```bash
NOTION_API_KEY=secret_xxx          # Required: Notion API key
NOTION_DATABASE_ID=abc123          # Optional: Default database
```

### Custom Status Mapping

If your database uses different status names:

```json
{
  "statusMapping": {
    "pending": "To Do",
    "working": "In Progress",
    "needs_review": "Review",
    "completed": "Done"
  }
}
```

---

## Integration with Git

After completing tickets, Claude can:

1. **Create commits** with ticket references:
   ```
   fix: Resolve login redirect issue

   Notion Ticket: https://notion.so/ticket-id
   ```

2. **Create PRs** linked to tickets

3. **Update ticket** with PR/commit links

---

## Security Considerations

1. **API Key Protection**: Never commit API keys to version control
2. **Minimal Permissions**: Only grant necessary permissions to integration
3. **Database Access**: Only share required databases with integration
4. **Sensitive Data**: Don't include secrets in ticket descriptions

---

## Related Documentation

- [Notion API Documentation](https://developers.notion.com/)
- [Notion MCP Server](https://github.com/notionhq/notion-mcp-server)
- [Claude Code MCP Guide](https://docs.anthropic.com/claude-code/mcp)
