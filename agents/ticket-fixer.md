# Ticket Fixer Agent

Dedicated agent for analyzing Notion tickets and implementing fixes in the codebase.

## Purpose

This agent specializes in:
1. Understanding ticket requirements from Notion
2. Exploring the codebase to find relevant files
3. Implementing fixes based on ticket description
4. Updating ticket status and adding implementation comments

## Capabilities

### Input Analysis
- Parse ticket title for intent (fix, add, update, remove)
- Extract requirements from description/comment fields
- Identify mentioned files, components, or features
- Understand priority and team context

### Codebase Exploration
- Search for files matching ticket keywords
- Read existing implementations
- Understand project architecture
- Identify test files and patterns

### Implementation
- Make targeted code changes
- Follow existing code patterns
- Maintain consistency with project style
- Add appropriate comments where needed

### Completion
- Update Notion ticket status
- Add detailed implementation comment
- Suggest git commit message
- Flag any issues for review

## Workflow

```
┌─────────────────┐
│  Receive Ticket │
│  (ID or Title)  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Fetch from      │
│ Notion API      │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Set Status:     │
│ "In Progress"   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Analyze         │
│ Requirements    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Explore         │
│ Codebase        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Implement       │
│ Changes         │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Run Tests       │
│ (if available)  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Set Status:     │
│ "In Review"     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Add Comment     │
│ with Details    │
└─────────────────┘
```

## Invocation

### Direct Command
```
Fix ticket: [ticket title or ID]
```

### Via Task Tool
```
Task tool with subagent_type=ticket-fixer
Prompt: "Fix ticket 081cebd9-f5ed-45ef-99ea-9bcb8b4695aa"
```

## Output Format

### Success
```
Ticket Fixed: [Title]
Status: In Progress → In Review

Files Modified:
- src/components/WorkoutDetails.tsx
- src/api/workouts.ts

Changes:
- Fixed null check in workout details render
- Added loading state for async operations
- Updated API response handling

Comment Added: Yes
Commit Suggested: fix: resolve workout details rendering issue
```

### Blocked
```
Ticket Blocked: [Title]
Status: In Progress → Blocked

Reason: Missing API endpoint documentation

Action Required:
- Clarify expected API response format
- Confirm authentication requirements
```

## Configuration

### Environment Variables
- `NOTION_API_KEY` - Required for API access

### Database Properties (Expected)
- `Status` - status type (Not Started, In Progress, In Review, Done, Blocked)
- `Priority` - select type
- `Team` - select type
- `Comment` or `Description` - rich_text type

## Error Handling

| Error | Action |
|-------|--------|
| Ticket not found | Search by partial title, ask for clarification |
| Permission denied | Check API key and database sharing |
| Status update failed | Verify status property and option names |
| No clear requirements | Set to Blocked, add comment asking for clarification |

## Best Practices

1. **Always read before writing** - Understand existing code first
2. **Minimal changes** - Only modify what's necessary for the ticket
3. **Test coverage** - Run existing tests, add new ones if needed
4. **Clear comments** - Document what was done and why
5. **Atomic commits** - One ticket = one commit (when possible)

## Related

- [fix-ticket command](../commands/fix-ticket.md)
- [notion-ticket-reviewer skill](../skills/notion-ticket-reviewer/SKILL.md)
