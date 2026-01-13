# Review Notion Tickets via Curl

## Prompt Template

```
Review notion tickets for database [DATABASE_ID]
```

## Description

Review all tickets from a Notion database using curl commands. This works independently of the MCP server and is compatible with any project.

## Prerequisites

1. **NOTION_API_KEY** must be set in one of:
   - `.env` file in project root
   - System environment variable

2. **Database must be shared** with your Notion integration

## Workflow

### Step 1: Get API Key

Read the API key from `.env` file:

```bash
# Read from .env file
NOTION_API_KEY=$(grep -E "^NOTION_API_KEY=" .env | cut -d'=' -f2)
echo "API Key found: ${NOTION_API_KEY:0:10}..."
```

Or from environment variable:

```bash
echo "API Key: ${NOTION_API_KEY:0:10}..."
```

### Step 2: Test Connection

Verify the API key works:

```bash
curl -s -X GET "https://api.notion.com/v1/users/me" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28"
```

Expected response includes `"object": "user"` and workspace info.

### Step 3: Query Database

Fetch all tickets from the database:

```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"page_size": 100}'
```

### Step 4: Parse and Display

Save response to temp file and parse with Python:

```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{"page_size": 100}' > /tmp/notion_tickets.json
```

Parse with Python:

```python
import json
import sys
sys.stdout.reconfigure(encoding='utf-8')

with open('/tmp/notion_tickets.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

tickets = []
for page in data.get('results', []):
    props = page.get('properties', {})

    # Extract title
    title = ''
    title_prop = props.get('Ticket Title', {}).get('title', [])
    if title_prop:
        title = title_prop[0].get('text', {}).get('content', '')

    # Extract status
    status = props.get('Status', {}).get('status', {}).get('name', 'Unknown')

    # Extract priority
    priority = props.get('Priority', {}).get('select', {})
    priority_name = priority.get('name', 'None') if priority else 'None'

    # Extract team
    team = props.get('Team', {}).get('select', {})
    team_name = team.get('name', 'None') if team else 'None'

    page_id = page.get('id', '')
    tickets.append({
        'title': title,
        'status': status,
        'priority': priority_name,
        'team': team_name,
        'id': page_id
    })

# Group by status
by_status = {}
for t in tickets:
    s = t['status']
    if s not in by_status:
        by_status[s] = []
    by_status[s].append(t)

# Display summary
print(f'Total tickets: {len(tickets)}')
print()

# Display by status
for status in ['Not Started', 'In Progress', 'In Review', 'Blocked', 'Done']:
    items = by_status.get(status, [])
    if items:
        print(f'=== {status} ({len(items)}) ===')
        for t in items:
            title_display = t['title'][:55] + '...' if len(t['title']) > 55 else t['title']
            print(f"  [{t['priority']:8}] {title_display}")
            print(f"            Team: {t['team']} | ID: {t['id'][:8]}")
        print()
```

## Filter Options

### By Status

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
    "page_size": 100
  }'
```

### By Team

```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "filter": {
      "property": "Team",
      "select": {"equals": "Full-Stack"}
    },
    "page_size": 100
  }'
```

### By Priority

```bash
curl -s -X POST "https://api.notion.com/v1/databases/[DATABASE_ID]/query" \
  -H "Authorization: Bearer $NOTION_API_KEY" \
  -H "Notion-Version: 2022-06-28" \
  -H "Content-Type: application/json" \
  -d '{
    "filter": {
      "property": "Priority",
      "select": {"equals": "High"}
    },
    "page_size": 100
  }'
```

### Combined Filters

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
    "page_size": 100
  }'
```

## Output Format

```
Total tickets: 100

=== Not Started (53) ===
  [High    ] Fix logout redirect that sends users to wrong env...
            Team: Full-Stack | ID: 0707a4ef
  [High    ] Work on API integration with content APIs
            Team: Full-Stack | ID: 07462277

=== In Progress (1) ===
  [High    ] Continue dashboard components work
            Team: Design | ID: 14a2693b

=== Done (46) ===
  [High    ] Implement value calculation logic and expose via API
            Team: Full-Stack | ID: 00ec6a80
```

## Troubleshooting

### "API token is invalid"
- Check NOTION_API_KEY is set correctly
- Verify key starts with `ntn_` or `secret_`
- Regenerate key at notion.so/my-integrations

### "Database not found"
- Verify database ID is correct (32 hex chars, no dashes)
- Ensure database is shared with your integration
- Go to database in Notion > ... > Add connections

### "Could not find property"
- Property names are case-sensitive
- Check exact property names in your database schema
- Common: "Ticket Title", "Status", "Priority", "Team"

## Related

- [notion-curl-update.md](./notion-curl-update.md) - Update tickets via curl
- [fix-all-by-status.md](./fix-all-by-status.md) - Fix all tickets sequentially
- [fix-single.md](./fix-single.md) - Fix a single ticket