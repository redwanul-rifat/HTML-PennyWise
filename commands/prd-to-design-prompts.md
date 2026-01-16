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

## Demo Pages

Below are 6 universal page templates that work for any project type.

---

## Page: 01-login
name: Login Page
category: auth

### SCREEN OVERVIEW
Create a login page for "[PROJECT_NAME]" - allows returning users to authenticate via email/password or social OAuth providers.

Purpose:
- Authenticate returning users
- Provide multiple login methods (email, Google, Apple)
- Quick access to password recovery
- Easy navigation to signup for new users

### LAYOUT INSTRUCTIONS

**OVERALL LAYOUT:**
- Split screen: 50% form (right), 50% branding panel (left)
- Form panel: Light background (surface color)
- Branding panel: Primary color gradient with illustration

**BRANDING PANEL (Left 50%):**
- Background: Linear gradient using primary/secondary colors
- Content (centered): Logo (48px), Headline "Welcome Back", Subtext (tagline)
- Illustration: Abstract or relevant to industry
- Pattern overlay: Subtle grid at 10% opacity

**FORM PANEL (Right 50%):**
- Content centered vertically, max-width 400px
- Header: "Sign In" (28px, bold), Subtitle (14px, gray)
- Form fields with 24px vertical gap

**FORM FIELDS:**
- Email Input: Label "Email Address", 48px height, mail icon
- Password Input: Label "Password", 48px height, lock icon, eye toggle
- Options Row: Checkbox "Remember me" (left), "Forgot Password?" link (right)
- Submit Button: "Sign In" (full-width, 48px, primary color)

**DIVIDER:** "Or continue with" with horizontal lines

**SOCIAL LOGIN ROW:**
- Google button (white bg, border)
- Apple button (black bg)

**FOOTER LINK:** "Don't have an account? Sign Up"

### KEY FEATURES
- Real-time email validation
- Password visibility toggle
- Remember me persists session
- Social OAuth (Google, Apple)
- Error states: Red border, error message below field
- Loading states on buttons
- Mobile: Branding panel hidden, form full-width

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Submit Login | Click "Sign In" button | Validate, authenticate, redirect to Dashboard |
| Toggle Password | Click eye icon | Show/hide password text |
| Forgot Password | Click link | Route to Forgot Password page |
| Google OAuth | Click Google button | OAuth flow, return with token |
| Navigate to Signup | Click "Sign Up" link | Route to Signup page |

### BRANDING ELEMENTS
- Primary gradient on branding panel
- Consistent input styling with brand colors
- Trust indicator: Lock icon near form
- Focus states use primary color

---

## Page: 02-signup
name: Sign Up Page
category: auth

### SCREEN OVERVIEW
Create a signup page for "[PROJECT_NAME]" - allows new users to create an account via email registration or social OAuth.

Purpose:
- Register new users
- Collect necessary profile information
- Ensure legal compliance (terms acceptance)
- Provide social signup shortcuts

### LAYOUT INSTRUCTIONS

**OVERALL LAYOUT:**
- Split screen: 50% form (right), 50% branding panel (left)
- Same structure as login for consistency

**BRANDING PANEL (Left 50%):**
- Gradient background with primary/secondary colors
- Logo, Headline: "Join [PROJECT_NAME]"
- Feature bullets with checkmarks (3-4 key benefits)
- Illustration: Person or icon representing growth/success

**FORM PANEL (Right 50%):**
- Header: "Create Account" (28px, bold)
- Subtitle: "Fill in your details to get started"

**SOCIAL SIGNUP (Top):**
- Google button, Apple button

**DIVIDER:** "Or register with email"

**FORM FIELDS:**
- Full Name: User icon, required
- Email Address: Mail icon, required
- Password: Lock icon, eye toggle, strength indicator, required
- Confirm Password: Lock icon, match validation, required
- Terms Checkbox: "I agree to Terms and Privacy Policy", required

**SUBMIT BUTTON:** "Create Account" (full-width, 48px, primary)

**FOOTER:** "Already have an account? Sign In"

### KEY FEATURES
- Real-time validation on all fields
- Password strength meter (Weak/Fair/Good/Strong)
- Email uniqueness check (async)
- Password match validation
- Terms must be accepted to submit
- Email verification sent after signup

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Submit Registration | Click "Create Account" | Validate, create account, send verification |
| Password Strength | On password input | Update strength meter |
| Password Match | On confirm blur | Show match indicator |
| Email Check | On email blur | Check if email exists |
| Navigate to Login | Click "Sign In" link | Route to Login page |

### BRANDING ELEMENTS
- Consistent with login page styling
- Feature highlights on branding panel
- Password strength uses semantic colors (red/yellow/green)
- Clear required field indicators

---

## Page: 03-dashboard
name: User Dashboard
category: user

### SCREEN OVERVIEW
Create a dashboard/home page for "[PROJECT_NAME]" - the logged-in user's home screen showing personalized overview, activity, and quick actions.

Purpose:
- Welcome user with personalized greeting
- Show activity summary and key stats
- Highlight notifications and updates
- Provide quick access to main features

### LAYOUT INSTRUCTIONS

**TOP NAVIGATION (Fixed, 64px):**
- Left: Logo "[PROJECT_NAME]"
- Center: Navigation tabs (Home, [Main Feature], [Secondary Feature], Settings)
- Right: Notification bell with badge, User avatar dropdown

**MAIN CONTENT (with sidebar):**

**LEFT SIDEBAR (240px, collapsible):**
- User profile card (avatar, name, role/status)
- Quick stats (3-4 key metrics)
- Quick Actions: Primary CTA button, Secondary links
- Recent items preview (3 items)

**MAIN CONTENT AREA:**

**WELCOME SECTION:**
- Greeting: "Welcome back, [First Name]!" (24px, bold)
- Subtitle: "Here's what's happening"
- Current date

**STATS CARDS ROW (3-4 cards):**
- Key metrics with icons, numbers, and trend indicators
- Click to view detailed data

**RECENT ACTIVITY SECTION:**
- Header: "Recent Activity" with "View All" link
- Timeline format feed (5 items)

**FEATURED CONTENT SECTION:**
- Header: "[Feature Name]" with "See All" link
- Horizontal card scroll (3-4 visible)

### KEY FEATURES
- Real-time notification updates
- Collapsible sidebar
- Pull to refresh on mobile
- Quick stats click-through to details
- Responsive grid layout

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Navigate Main Feature | Click nav tab | Route to main feature page |
| View Notifications | Click bell icon | Show notification dropdown |
| Open User Menu | Click avatar | Show dropdown (Profile, Settings, Logout) |
| Logout | Click "Logout" | Clear session, redirect to Landing |
| Toggle Sidebar | Click collapse button | Collapse/expand sidebar |
| Stat Card Click | Click card | Route to detailed view |

### BRANDING ELEMENTS
- Consistent primary accent color
- Card-based layout with soft shadows
- Status colors (green/yellow/red)
- Clean, professional dashboard aesthetic

---

## Page: 04-list-browse
name: Browse/List Page
category: core

### SCREEN OVERVIEW
Create a browse/list page for "[PROJECT_NAME]" - displays items in a filterable, searchable grid or list view.

Purpose:
- Discover and browse items
- Filter and search content
- Quick actions (save, share, etc.)
- Navigate to item details

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Browse [Items]" (28px, bold)
- Subtitle: "Discover [items] from [source]"

**SEARCH & FILTER BAR (Sticky):**
- Search Input: "Search [items]..."
- Filter Pills: Category, Tags, Status, Date
- Sort Dropdown: Most Recent, Most Popular, A-Z
- "Clear All Filters" link

**RESULTS HEADER:**
- Left: "[N] [Items] Found"
- Right: View toggle (Grid / List)

**ITEMS GRID (Card Layout):**
- 3 columns desktop, 2 tablet, 1 mobile
- 24px gap between cards

**ITEM CARD DESIGN:**
- Thumbnail Image (16:9 or square)
- Category Badge (top-left corner)
- Status Badge (top-right, optional)
- Title (truncated to 2 lines)
- Description (truncated to 2-3 lines)
- Meta Row: Creator/Author, Date
- Tags Row (optional)
- Actions Row: Primary action, Save/Bookmark, Share

**PAGINATION / INFINITE SCROLL:**
- Load more on scroll or "Load More" button
- Show skeleton cards while loading

**EMPTY STATE:**
- Illustration
- "No [items] found"
- Suggestion or CTA button

### KEY FEATURES
- Real-time search (debounced 300ms)
- Filter state saved in URL (shareable)
- Infinite scroll with loading skeletons
- View toggle (Grid/List)
- Optimistic UI for save/bookmark

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Search | Type in search | Filter results, update URL |
| Apply Filter | Select filter option | Filter results, update count |
| Clear Filters | Click "Clear All" | Reset all filters |
| Toggle View | Click Grid/List | Switch layout mode |
| View Item | Click card/title | Route to Detail page |
| Save Item | Click bookmark | Add to saved, show toast |
| Share Item | Click share | Copy URL, show toast |
| Load More | Scroll bottom | Load next page |

### BRANDING ELEMENTS
- Consistent card styling
- Category colors
- Save animation
- Clean, scannable layout

---

## Page: 05-detail-view
name: Detail Page
category: core

### SCREEN OVERVIEW
Create a detail page for "[PROJECT_NAME]" - shows complete information about a single item with actions and related content.

Purpose:
- Display full item information
- Enable actions (save, share, edit)
- Show related content
- Facilitate engagement (comments, etc.)

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Breadcrumb: "[Items] > [Category] > [Title]"
- Back button: "← Back to [Items]"

**MAIN CONTENT (2-column: 65% content, 35% sidebar):**

**LEFT COLUMN - MAIN CONTENT:**
- Header Section: Title (32px), Meta badges, Author/Creator row
- Media Section: Main image/video, thumbnail gallery
- Content Section: Full description (rich text)
- Additional Sections: Based on item type (specs, features, etc.)
- Tags Section: Tag pills

**RIGHT COLUMN - SIDEBAR (Sticky):**
- Action Card: Primary CTA button, Save button, Share button
- Creator/Author Card: Avatar, name, bio, "View Profile" link
- Stats Card: Views, saves, engagement metrics
- Related Items: 3-4 related item cards

**COMMENTS SECTION (Below main, full width):**
- Header: "Comments ([N])" with sort dropdown
- Comment input (if logged in)
- Comments list with replies

### KEY FEATURES
- Image gallery with lightbox
- Sticky sidebar on scroll
- Share with multiple options
- Related content recommendations
- Comment threading

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Primary Action | Click CTA button | Execute main action |
| Save Item | Click "Save" | Add to saved, update button |
| Share | Click share | Open share modal/dropdown |
| View Gallery | Click thumbnail | Open lightbox |
| View Creator | Click creator name | Route to profile |
| Post Comment | Submit comment | Add to list |
| Navigate Tag | Click tag | Route to filtered list |
| Back to List | Click back | Route to list page |

### BRANDING ELEMENTS
- Content hierarchy with brand typography
- Action buttons use primary color
- Consistent card styling
- Professional content presentation

---

## Page: 06-form
name: Create/Edit Form
category: core

### SCREEN OVERVIEW
Create a form page for "[PROJECT_NAME]" - allows users to create or edit content with structured input sections.

Purpose:
- Collect structured information
- Guide users through input process
- Validate and save data
- Support media uploads

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Create [Item]" or "Edit [Item]" (28px, bold)
- Subtitle: "Fill in the details below"
- Progress indicator (optional, for multi-step)

**FORM LAYOUT:**
- Single column, max-width 720px, centered
- Sticky action bar at bottom

**SECTION 1: BASIC INFORMATION**
- Title/Name: Text input, required, character counter
- Category: Dropdown select, required
- Tags: Tag input with autocomplete (min/max limits)

**SECTION 2: CONTENT**
- Description: Rich text editor, required, min/max characters
- Additional fields based on item type

**SECTION 3: MEDIA**
- Images: Drag & drop upload area, thumbnails, reorder
- Videos: Upload or URL input (optional)

**SECTION 4: SETTINGS**
- Visibility: Radio cards (Public/Private)
- Other settings as needed

**FORM ACTIONS (Sticky bottom bar):**
- "Save as Draft" (secondary/outlined)
- "Submit" or "Save Changes" (primary)
- "Cancel" (text button)

### KEY FEATURES
- Auto-save draft (every 30 seconds)
- Real-time validation with inline errors
- Rich text editor
- Drag-drop media upload with preview
- Character counters
- Progress saved if navigating away

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Enter Field | Type in input | Update value, validate |
| Add Tag | Select from autocomplete | Add tag pill |
| Remove Tag | Click X on tag | Remove tag |
| Upload Media | Drag/drop or click | Upload, show preview |
| Remove Media | Click X on preview | Remove from list |
| Reorder Media | Drag thumbnail | Update order |
| Save Draft | Click "Save as Draft" | Save, show toast |
| Auto-save | Every 30 seconds | Silent save, show indicator |
| Submit | Click "Submit" | Validate all, submit, redirect |
| Cancel | Click "Cancel" | Confirm discard, navigate back |

### BRANDING ELEMENTS
- Consistent form field styling
- Section dividers
- Progress indicators use brand colors
- Clear required field markers
- Professional form layout

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
