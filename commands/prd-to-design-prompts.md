---
description: Generate AURA.build design prompts from PRD content
argument-hint: "<prd-file> [--template <type>] [--output <file>]"
---

# PRD to Design Prompts

Converts a PRD (Product Requirements Document) into structured design prompts for AURA.build.

---

## Usage

```bash
/prd-to-design-prompts <prd-file>
/prd-to-design-prompts <prd-file> --template saas
/prd-to-design-prompts <prd-file> --output ./prompts/my-project.md
```

## Arguments

| Argument | Description | Default |
|----------|-------------|---------|
| `<prd-file>` | Path to PRD markdown file | (required) |
| `--template <type>` | Design template to use | auto-detect |
| `--output <file>` | Output file path | `./[project]-design-prompts.md` |

---

## Template Presets

Use `--template` flag or auto-detect from PRD keywords:

| Template | Design System | Best For | Keywords |
|----------|---------------|----------|----------|
| `saas` | Dark zinc-950, violet accent, Inter | SaaS, dashboards, B2B | dashboard, analytics, subscription |
| `ecommerce` | Light white, emerald accent, Plus Jakarta | Online stores, marketplaces | shop, cart, checkout, product |
| `landing` | Bold slate-900, amber accent, Poppins | Marketing, portfolios | landing, marketing, showcase |
| `social` | Modern zinc-900, pink accent, SF Pro | Social apps, community | feed, profile, posts, messaging |
| `mobile-app` | Minimal neutral-950, blue accent, System UI | Mobile-first apps | app, mobile, iOS, Android |
| `admin` | Functional gray-100, slate accent, Inter | Admin panels, CMS | admin, management, CRM |
| `fintech` | Secure slate-950, green accent, IBM Plex | Finance, banking | banking, payments, wallet |
| `healthcare` | Clean blue-50, sky accent, Open Sans | Medical, wellness | health, medical, appointments |
| `education` | Engaging white, purple accent, Nunito | Learning platforms | courses, learning, students |

---

## Universal Format

### Output Frontmatter Template

```yaml
---
project_name: "[PROJECT_NAME]"
total_pages: [PAGE_COUNT]
template: "[TEMPLATE_TYPE]"
design_system:
  type: "[APP_TYPE]"
  style: "[STYLE]"
  industry: "[INDUSTRY]"
  primary_color: "[PRIMARY_HEX]"
  secondary_color: "[SECONDARY_HEX]"
  font: "[FONT_FAMILY]"
  icons: "[ICON_LIBRARY]"
---
```

### Design System Template

```markdown
## Design System

[PROJECT_NAME] - [APP_TYPE] for [INDUSTRY].
Style: [STYLE] with [PRIMARY_HEX] primary and [SECONDARY_HEX] secondary.

**Colors:**
- Primary: [PRIMARY_HEX] ([COLOR_NAME])
- Secondary: [SECONDARY_HEX] ([COLOR_NAME])
- Success: #10B981 (Emerald)
- Warning: #F59E0B (Amber)
- Error: #EF4444 (Red)
- Background: [BG_HEX]
- Surface: [SURFACE_HEX]
- Text Primary: [TEXT_PRIMARY_HEX]
- Text Secondary: [TEXT_SECONDARY_HEX]
- Border: [BORDER_HEX]

**Typography:**
- Font Family: [FONT_FAMILY]
- Monospace: [MONO_FONT]

**Styling:**
- Card Radius: [CARD_RADIUS]px
- Button Radius: [BTN_RADIUS]px
- Shadow: [SHADOW_STYLE]
- Icons: [ICON_LIBRARY] ([ICON_STYLE] style)
```

### Page Prompt Template

```markdown
## Page: [NN]-[page-slug]
name: [Page Name]
category: [auth/user/core/admin/marketing]

### SCREEN OVERVIEW
Create a [page type] page for "[PROJECT_NAME]" - [brief description].

Purpose:
- [Purpose 1]
- [Purpose 2]

### LAYOUT INSTRUCTIONS
**OVERALL LAYOUT:**
- [Layout description]

**[SECTION 1]:**
- [Elements]

**[SECTION 2]:**
- [Elements]

### KEY FEATURES
- [Feature 1]
- [Feature 2]

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| [Action] | [Trigger] | [Behavior] |

### BRANDING ELEMENTS
- [Brand element 1]
- [Brand element 2]
```

---

## Extraction Rules

### From PRD → Variables

| PRD Section | Extract To | Example |
|-------------|------------|---------|
| Title/Name | `[PROJECT_NAME]` | "TaskFlow" |
| App Type | `[APP_TYPE]` | "Web Application" |
| Target Users | `[INDUSTRY]` | "Project Management" |
| Brand Colors | `[PRIMARY_HEX]`, `[SECONDARY_HEX]` | "#6366F1", "#8B5CF6" |
| Features List | Page list | Login, Dashboard, etc. |
| User Flows | Page relationships | Login → Dashboard |

### Page Categories

| Category | Common Pages |
|----------|--------------|
| auth | Login, Signup, Forgot Password, Reset Password, Email Verification |
| user | Dashboard, Profile, Settings, Notifications |
| core | List/Browse, Detail View, Create Form, Edit Form |
| admin | Admin Dashboard, User Management, Reports, Analytics, CMS |
| marketing | Landing, About, Pricing, Contact, FAQ |

### Page Generation Rules

1. **Extract features** from PRD → List all screens needed
2. **Group by category** (auth, user, core, admin, marketing)
3. **Number sequentially** (01, 02, 03...)
4. **Use kebab-case** for slugs (e.g., `forgot-password`)
5. **Estimate count**: Auth (4) + Core features + Admin (if needed)

---

## Related Commands

- `/prompts-to-aura` - Execute design prompts on AURA.build using Playwright MCP
- `/prd-to-design-guides` - Generate comprehensive design guide from PRD

---

## Tips

1. **Extract carefully** - Read the full PRD before generating prompts
2. **Match template** - Use appropriate template for the project type
3. **Be specific** - Include exact colors, sizes, spacing in prompts
4. **Cover all states** - Empty, loading, error, success
5. **Number pages** - Use 01, 02, 03 format for sorting
6. **Use consistent naming** - kebab-case for slugs, Title Case for names
