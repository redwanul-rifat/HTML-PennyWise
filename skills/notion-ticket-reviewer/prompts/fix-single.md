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
   └── Search by title or ID
   └── Fetch ticket details from Notion API

2. SET IN PROGRESS
   └── Update Status: "Not Started" → "In Progress"

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
   └── Update Status: "In Progress" → "In Review"
   └── Add comment with implementation details
   └── Suggest git commit message
```

## Example Usage

### By Title
```
Fix ticket: Fix workout details sections
```

### By ID
```
Fix ticket: 081cebd9-f5ed-45ef-99ea-9bcb8b4695aa
```

### With Context
```
Fix ticket: Fix workout details sections
Context: After syncing with Saiful, need to update the workout details component
```

## Output Format

### Success
```
Ticket Fixed: [Title]
Status: Not Started → In Progress → In Review

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

- [review-all.md](./review-all.md) - Review all tickets first
- [../../../commands/fix-ticket.md](../../../commands/fix-ticket.md) - Full command documentation
- [../../../agents/ticket-fixer.md](../../../agents/ticket-fixer.md) - Agent documentation
