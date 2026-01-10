---
description: Convert PRD to AI design tool prompts (Aura.build, Gemini, v0, etc.)
argument-hint: "<prd-path> [--tool <aura|gemini|v0|generic>] [--screens-only] [--admin-only]"
---

# PRD to Design Prompts Generator

Convert a PRD into structured prompts for AI design tools.

## Usage

```bash
/prd-to-design-prompts <path-to-prd>
/prd-to-design-prompts <path-to-prd> --tool aura
/prd-to-design-prompts <path-to-prd> --tool gemini
/prd-to-design-prompts <path-to-prd> --screens-only
```

## Arguments

- `--tool <name>` - aura, gemini, v0, generic (default: generic)
- `--screens-only` - Only user-facing screens
- `--admin-only` - Only admin dashboard screens  
- `--style <name>` - minimal, bold, dark (default: minimal)

## Supported Tools

| Tool | Best For |
|------|----------|
| aura | Aura.build - HTML/Figma export |
| gemini | Google Gemini - detailed context |
| v0 | Vercel v0.dev - React components |
| generic | Any AI design tool |

---

## Execution Steps

### Step 1: Parse Arguments
Extract PRD path, tool selection, filters, and style preference from $ARGUMENTS.

### Step 2: Read PRD
Use Read tool to read the PRD file (supports PDF, MD, TXT).

### Step 3: Extract Screen Inventory

Find all screens from:
- Page Architecture / Sitemap
- Screen / Page Lists  
- User Flows
- Feature specifications

For each screen extract: name, category, platform, user type, components, data fields, actions.

### Step 4: Generate Design System Prompt

```
Design System for [Project]

Style: [minimal/bold/dark]

Colors:
- Primary: #1A1A1A
- Accent: #E63946  
- Background: #FFFFFF
- Text: #1A1A1A, #6B6B6B

Typography: Inter or SF Pro
Spacing: 4px, 8px, 16px, 24px, 32px
Cards: 12px radius, subtle shadow
Buttons: 8px radius, 44px touch target
```

### Step 5: Generate Screen Prompts

Use format based on selected tool:

**Generic Format:**
```
Create [platform] screen for "[Project]".

Screen: [Name]
Platform: [Mobile/Web]
User: [Type]

Layout:
- Header: [description]
- Content: [description]
- Navigation: [description]

Components: [list]
Data: [fields]
Actions: [interactions]
```

**Aura Format:**
```
Create [screen] for "[project]" [mobile/web].

Platform: [Mobile/Web]
Style: Modern minimal

Layout:
- [Section descriptions]

Components:
- [UI elements]

Actions:
- [Interactions]
```

**Gemini Format:**
```
Design UI for: [Screen Name]

Context:
- App: [Name]
- User: [Type]
- Platform: [Mobile/Web]

Requirements:
- [From PRD]

Visual Elements:
- [Needed components]

Style: [preference]
```

**v0 Format:**
```
Create React component for [Screen].

Features:
- [List]

UI:
- [Elements]

Style: Tailwind CSS, [preference]
```

### Step 6: Organize and Save

Save to: `.claude-project/design-prompts/[project]-[tool]-prompts.md`

Output structure:
```markdown
# [Project] - Design Prompts

> Source: [PRD filename]
> Tool: [target tool]
> Screens: [count]

## Design System
[Base prompt]

## Part 1: Common/Auth Screens
### 1.1 [Screen Name]
[Prompt]

## Part 2: User Screens
### 2.1 [Screen Name]
[Prompt]

## Part 3: Admin Screens
...
```

### Step 7: Report Summary

Output:
- Total screens generated
- Categories breakdown
- Output file location
- Next steps

---

## Screen Categories

| Category | Examples |
|----------|----------|
| Auth | Splash, Onboarding, Login, Signup |
| Home | Dashboard, Feed, Overview |
| Content | Detail views, Lists, Galleries |
| Creation | Forms, Editors, Upload |
| Search | Search, Filters, Results |
| Profile | Profile, Settings |
| Admin | Dashboard, Management tables |

## Style Presets

- **minimal** - White bg, subtle shadows, clean typography
- **bold** - Strong colors, high contrast
- **dark** - Dark bg (#1A1A1A), light text

## Example

```bash
/prd-to-design-prompts ./bside_PRD.pdf --tool aura --style minimal
```

Output: `.claude-project/design-prompts/bside-aura-prompts.md`
