# Filter by Team

## Prompt Template

```
Enter plan mode - Review notion tickets
Filter: Team = "[TEAM_NAME]", Status = "Not Started"
```

## Description

Filter tickets by team assignment to see work relevant to a specific team.

## Available Teams

| Team | Description |
|------|-------------|
| **Full-Stack** | Backend API, frontend web, integrations |
| **Design** | UI/UX, visual design, prototypes |
| **Mobile** | iOS, Android, React Native |
| **Operation** | DevOps, infrastructure, deployment |

## Example Usage

### Full-Stack Team
```
Enter plan mode - Review notion tickets for database [DATABASE_ID]
Filter: Team = "Full-Stack", Status = "Not Started"
```

### Design Team
```
Enter plan mode - Review notion tickets for database [DATABASE_ID]
Filter: Team = "Design"
```

### Multiple Teams
```
Enter plan mode - Review notion tickets for database [DATABASE_ID]
Filter: Team = "Full-Stack" OR Team = "Mobile"
```

### Team + Priority
```
Enter plan mode - Review notion tickets for database [DATABASE_ID]
Filter: Team = "Full-Stack", Priority = "High"
```

## API Filter

### Single Team
```json
{
  "filter": {
    "and": [
      {
        "property": "Team",
        "select": {
          "equals": "Full-Stack"
        }
      },
      {
        "property": "Status",
        "status": {
          "equals": "Not Started"
        }
      }
    ]
  }
}
```

### Multiple Teams
```json
{
  "filter": {
    "and": [
      {
        "or": [
          {"property": "Team", "select": {"equals": "Full-Stack"}},
          {"property": "Team", "select": {"equals": "Mobile"}}
        ]
      },
      {
        "property": "Status",
        "status": {
          "equals": "Not Started"
        }
      }
    ]
  }
}
```

## Output Format

```
Found [N] tickets for team [TEAM_NAME]:

### Critical/Urgent
1. [CRITICAL] Title - ID: xxx...
2. [URGENT] Title - ID: xxx...

### High Priority
3. [HIGH] Title - ID: xxx...

### Medium/Low Priority
4. [MEDIUM] Title - ID: xxx...
5. [LOW] Title - ID: xxx...
```

## Common Use Cases

### Daily Standup
```
Enter plan mode - Review notion tickets
Filter: Team = "Full-Stack", Status = "In Progress"
```

### Sprint Planning
```
Enter plan mode - Review notion tickets
Filter: Team = "Full-Stack", Status = "Not Started", Priority = "High" OR "Critical"
```

### Blocked Items
```
Enter plan mode - Review notion tickets
Filter: Team = "Full-Stack", Status = "Blocked"
```

## Related

- [review-all.md](./review-all.md) - Review all tickets
- [filter-by-project.md](./filter-by-project.md) - Filter by project
