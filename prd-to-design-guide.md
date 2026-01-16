# PRD to Design Guide - Universal Format

---

## HOW TO USE

| Phase | Action |
|-------|--------|
| 1 | Extract project info (name, type, pages, timeline) |
| 2 | Map features to reference apps → create design pillars |
| 3 | Define design system (colors, typography, spacing) |
| 4 | Convert pages to design briefs |
| 5 | Design all states, modals, dropdowns, notifications |
| 6 | Create responsive variants (Mobile, Tablet, Desktop) |
| 7 | Create deliverables checklist |

---

## EXTRACTION TABLES

### Project Info
| Extract | From PRD | Variable |
|---------|----------|----------|
| Project Name | Title | `[PROJECT]` |
| Type | App Type | `[TYPE]` |
| Platform | Platform section | `[PLATFORM]` |
| User Types | User Roles | `[USERS]` |
| Total Pages | Page Breakdown | `[PAGES]` |
| Timeline | Timeline section | `[TIMELINE]` |

### Feature → Reference Mapping
| PRD Feature | Reference App | Pattern |
|-------------|---------------|---------|
| Upvoting, ranking | Product Hunt | Vote button, card layout |
| Threaded comments | Reddit | Nested replies, vertical lines |
| Professional feed | LinkedIn | Card-based, achievement feel |
| Dashboard, analytics | Stripe, Linear | Clean stats, minimal |
| Stories, timeline | Instagram, Twitter | Social feed |
| Kanban, drag-drop | Trello, Asana | Task management |
| Chat, messaging | Slack, Discord | Message UI |
| E-commerce, cart | Amazon, Shopify | Shopping flow |

### Color Mapping
| PRD Field | Design Token | Default |
|-----------|--------------|---------|
| Main color | Primary | #6366F1 |
| Success states | Success | #10B981 |
| Warning states | Warning | #F59E0B |
| Error states | Error | #EF4444 |
| — | Background | #F9FAFB |
| — | Surface | #FFFFFF |
| — | Text | #111827 |
| — | Border | #E5E7EB |

---

## OUTPUT FORMAT

```markdown
# [PROJECT] Design Guide

**Project:** [PROJECT] | **Type:** [TYPE] | **Pages:** [PAGES]
**Designer:** [NAME] | **Timeline:** [TIMELINE]

---

## 0. REFERENCES

### Inspiration
| App | Study For |
|-----|-----------|
| [App 1] | [Feature] |
| [App 2] | [Feature] |

### Design Pillars
| Feature | Reference | Pattern |
|---------|-----------|---------|
| [Area 1] | [App] | [Pattern] |
| [Area 2] | [App] | [Pattern] |

### Mood
| Attribute | Value |
|-----------|-------|
| Feel | [Professional/Playful/Minimal] |
| Style | [Clean/Rich/Flat] |
| Audience | [Description] |

---

## 1. UX STANDARDS

### Contrast (WCAG 2.1)
| Element | Ratio |
|---------|-------|
| Body text | 4.5:1 min |
| Large text (18px+) | 3:1 min |
| UI elements | 3:1 min |
| Focus states | 3:1 min |
| Placeholders | 3:1 min |

### Readability
| Rule | Value |
|------|-------|
| Body font | 16px min |
| Line length | 50-75 chars |
| Line height (body) | 1.5 |
| Line height (headings) | 1.2-1.3 |
| Paragraph gap | 1-1.5em |

### Consistency
| Element | Same Across All |
|---------|-----------------|
| Buttons | Color, height, radius |
| Inputs | Height, border, focus |
| Cards | Padding, radius, shadow |
| Icons | Family, size, stroke |
| Spacing | Grid (4px or 8px) |
| Animations | Duration, easing |

### Accessibility
| Rule | Requirement |
|------|-------------|
| Touch targets | 44px min (48px ideal) |
| Focus indicator | 2-3px outline |
| Color independence | Icon + text + color |
| Keyboard nav | All interactive elements |
| Alt text | All images |

---

## 2. RESPONSIVE DESIGN

### Device Targets
| Device | Width | Orientation | Priority |
|--------|-------|-------------|----------|
| Mobile | 320-428px | Portrait | Primary |
| Mobile L | 428-640px | Portrait/Landscape | Secondary |
| Tablet | 640-1024px | Both | Secondary |
| Desktop | 1024-1440px | Landscape | Primary |
| Large | 1440px+ | Landscape | Optional |

### Layout Adaptations
| Element | Mobile | Tablet | Desktop |
|---------|--------|--------|---------|
| Navigation | Bottom bar / Hamburger | Sidebar collapsed | Sidebar expanded |
| Grid columns | 1 | 2 | 3-4 |
| Cards | Full width, stacked | 2 per row | 3-4 per row |
| Sidebar | Hidden (drawer) | Collapsible | Fixed 240px |
| Modals | Full screen | Centered 90% | Centered 560px |
| Forms | Single column | Single column | Two column optional |

### Touch vs Mouse
| Interaction | Mobile/Tablet | Desktop |
|-------------|---------------|---------|
| Primary action | Tap | Click |
| Secondary | Long press | Right click / Hover |
| Navigation | Swipe | Scroll |
| Targets | 48px min | 36px min |
| Hover states | None | Required |

### Responsive Typography
| Element | Mobile | Tablet | Desktop |
|---------|--------|--------|---------|
| H1 | 28px | 32px | 40px |
| H2 | 22px | 26px | 32px |
| H3 | 18px | 20px | 24px |
| Body | 16px | 16px | 16px |
| Small | 14px | 14px | 14px |

### Responsive Spacing
| Token | Mobile | Desktop |
|-------|--------|---------|
| Page padding | 16px | 24px |
| Card padding | 16px | 20px |
| Section gap | 24px | 32px |
| Grid gap | 12px | 24px |

---

## 3. FULL FLOW DESIGN

### Screen Types to Design
| Screen Type | Description | Variants |
|-------------|-------------|----------|
| List/Browse | Grid or list of items | Empty, Loading, Loaded, Filtered |
| Detail | Single item view | Default, Editing, Read-only |
| Form | Data entry | New, Edit, Review |
| Dashboard | Overview with stats | Default, Loading |
| Settings | Configuration options | Sections, Nested |

### Screen States (Design All)
| State | Description | Elements |
|-------|-------------|----------|
| Empty | No data yet | Illustration, message, CTA |
| Loading | Fetching data | Skeleton or spinner |
| Loaded | Data displayed | Content |
| Error | Failed to load | Error message, retry button |
| Offline | No connection | Offline indicator |
| Partial | Some data loaded | Mixed skeleton + content |

### Overlay Screens
| Type | Trigger | Size | Close Method |
|------|---------|------|--------------|
| Modal | Button click | S/M/L/Fullscreen | X, Outside click, ESC |
| Drawer | Menu tap | 280px / 80% | Swipe, X, Outside |
| Bottom Sheet | Action tap | Auto height | Swipe down, X |
| Lightbox | Image click | Full viewport | X, Outside, ESC |

### Modal Templates

**Confirmation Modal:**
- Icon (warning/info)
- Title: "Are you sure?"
- Description: Context
- Actions: Cancel (secondary), Confirm (primary/destructive)

**Form Modal:**
- Title + Close (X)
- Form fields
- Actions: Cancel, Submit

**Info Modal:**
- Title + Close (X)
- Content (text, image, video)
- Actions: Close / CTA

**Success Modal:**
- Checkmark animation
- Title: "Success!"
- Description
- Actions: Done / Next step

### Dropdown Components
| Type | Trigger | Content | Position |
|------|---------|---------|----------|
| Menu dropdown | Click avatar/button | Links, actions | Below, align right |
| Select dropdown | Click input | Options list | Below, full width |
| Filter dropdown | Click filter pill | Checkboxes, radio | Below |
| Autocomplete | Type in input | Suggestions | Below |

### Dropdown Templates

**User Menu Dropdown:**
- Avatar + Name + Email
- Divider
- Profile link
- Settings link
- Divider
- Logout (red)

**Notification Dropdown:**
- Header: "Notifications" + Mark all read
- List of items (icon, text, time, unread dot)
- Footer: "View all" link

**Filter Dropdown:**
- Header: Filter name
- Options (checkbox/radio)
- Footer: Clear / Apply

### Notification Components
| Type | Position | Duration | Actions |
|------|----------|----------|---------|
| Toast success | Top-right | 3s auto | Dismiss |
| Toast error | Top-right | 5s auto | Dismiss, Retry |
| Toast info | Top-right | 4s auto | Dismiss, Action |
| Banner | Top of page | Persistent | Dismiss, CTA |
| Badge | On icon | Persistent | — |
| Dot indicator | Corner | Persistent | — |

### Flow Connections

**Page → Modal Flows:**
| Trigger | Opens | After Close |
|---------|-------|-------------|
| "Delete" button | Confirmation modal | Refresh list or redirect |
| "Edit" button | Edit form modal | Update item in place |
| "Add new" button | Create form modal | Add to list |
| Click image | Lightbox | Return to page |
| "Share" button | Share modal | Show toast |

**Page → Dropdown Flows:**
| Trigger | Opens | On Select |
|---------|-------|-----------|
| Avatar click | User menu | Navigate or action |
| Bell icon click | Notifications | Mark read, navigate |
| Filter pill click | Filter options | Apply filter, refresh |
| Sort dropdown | Sort options | Re-sort list |

---

## 4. UI SYSTEM

### Typography

#### Fonts
| Role | Font | Family | Fallback | Source |
|------|------|--------|----------|--------|
| Primary | [Font] | sans-serif | system-ui | [Source] |
| Mono | [Font] | monospace | Consolas | [Source] |

#### Weights
| Weight | Value | Use |
|--------|-------|-----|
| Regular | 400 | Body |
| Medium | 500 | Labels, buttons |
| Semibold | 600 | Headings |
| Bold | 700 | Titles |

#### Scale
| Level | Size | Weight | Height | Use |
|-------|------|--------|--------|-----|
| H1 | 32px | 700 | 1.2 | Page titles |
| H2 | 24px | 600 | 1.3 | Sections |
| H3 | 20px | 600 | 1.3 | Subsections |
| Body | 16px | 400 | 1.5 | Content |
| Small | 14px | 400 | 1.5 | Secondary |
| Caption | 12px | 500 | 1.4 | Labels |

### Spacing
| Token | Value | Use |
|-------|-------|-----|
| xs | 4px | Icon gaps |
| sm | 8px | Inline |
| md | 16px | Form fields |
| lg | 24px | Sections |
| xl | 32px | Large gaps |
| 2xl | 48px | Page sections |

### Components

#### Buttons
| Type | Height | Radius | Font |
|------|--------|--------|------|
| Primary | 48px | 6px | 14px/500 |
| Secondary | 48px | 6px | 14px/500 |
| Small | 36px | 4px | 14px/500 |

#### Inputs
| Property | Value |
|----------|-------|
| Height | 48px |
| Radius | 6px |
| Border | 1px solid gray-200 |
| Label | 14px/500, 8px above |

#### Cards
| Property | Value |
|----------|-------|
| Padding | 20px |
| Radius | 12px |
| Shadow | 0 1px 3px rgba(0,0,0,0.1) |

### States
| State | Style |
|-------|-------|
| Hover | Darken 10%, 150ms |
| Active | Scale 0.98, 100ms |
| Focus | 3px outline, 2px offset |
| Disabled | 50% opacity |
| Error | Red border + icon |
| Success | Green border + icon |

### Icons
| Property | Value |
|----------|-------|
| Library | [Lucide/Heroicons/etc] |
| Style | Outlined |
| Sizes | 16, 20, 24, 32px |

### Shadows
| Level | Value | Use |
|-------|-------|-----|
| sm | 0 1px 2px rgba(0,0,0,0.05) | Subtle |
| md | 0 1px 3px rgba(0,0,0,0.1) | Cards |
| lg | 0 4px 6px rgba(0,0,0,0.1) | Dropdowns |
| xl | 0 10px 15px rgba(0,0,0,0.1) | Modals |

---

## 5. BRANDING

### Colors

#### Primary
| Name | Hex | Use |
|------|-----|-----|
| Primary | #[HEX] | Buttons, links |
| Primary Hover | #[HEX] | Hover state |
| Primary Light | #[HEX] | Backgrounds |

#### Semantic
| Name | Hex | Light | Use |
|------|-----|-------|-----|
| Success | #10B981 | #D1FAE5 | Approved |
| Warning | #F59E0B | #FEF3C7 | Pending |
| Error | #EF4444 | #FEE2E2 | Errors |

#### Neutrals
| Name | Hex | Use |
|------|-----|-----|
| Gray 50 | #F9FAFB | Background |
| Gray 200 | #E5E7EB | Borders |
| Gray 500 | #6B7280 | Secondary text |
| Gray 900 | #111827 | Titles |

### Assets
| Element | Spec |
|---------|------|
| Logo | [SIZE], SVG |
| Favicon | 32px, PNG |
| OG Image | 1200x630px |

### Visual Style
| Element | Value |
|---------|-------|
| Icons | [Library], [Style] |
| Shadows | Soft |
| Radius | Rounded |
| Gradient | [Color1] → [Color2] |

---

## 6. PAGE BRIEFS

### [Section] Pages ([N])

**PAGE 1: [Name]**

Layout: [Pattern]

Responsive:
- Mobile: [Behavior]
- Tablet: [Behavior]
- Desktop: [Behavior]

Elements:
- [Element 1]
- [Element 2]

States:
- Empty: [Description]
- Loading: [Skeleton/Spinner]
- Error: [Message + Retry]

Modals:
- [Modal 1]: [Trigger] → [Content] → [Result]

Dropdowns:
- [Dropdown 1]: [Position], [Content]

Notifications:
- [Action] → [Toast type]: [Message]

---

## 7. PATTERNS

### Layouts
| Pattern | Structure | Use |
|---------|-----------|-----|
| Split | 50/50: Brand \| Form | Auth |
| Centered | Max 440px | Recovery |
| Sidebar | 240px + fluid | Dashboard |
| Two-col | 65/35 | Detail |
| Grid | 3-4 columns | Browse |

### Forms
| Rule | Implementation |
|------|----------------|
| Labels | Above, always visible |
| Required | Asterisk (*) |
| Validation | On blur, inline |
| Submit | Bottom, full-width mobile |

### Feedback
| Type | Position | Duration |
|------|----------|----------|
| Toast success | Top-right | 3s |
| Toast error | Top-right | 5s |
| Loading | Inline spinner | Until done |
| Empty | Centered | Persistent |

---

## 8. CHECKLIST

### UX Standards
- [ ] Contrast 4.5:1+ (body), 3:1+ (large)
- [ ] Font 16px+, line height 1.5
- [ ] Line length 50-75 chars
- [ ] Touch targets 44px+
- [ ] Focus states visible
- [ ] No color-only indicators
- [ ] Keyboard nav works

### Responsive
- [ ] Mobile layout (320-428px)
- [ ] Tablet layout (640-1024px)
- [ ] Desktop layout (1024px+)
- [ ] Touch targets 48px on mobile
- [ ] Navigation adapts per device
- [ ] Typography scales correctly

### Full Flow
- [ ] All screen states (empty, loading, error)
- [ ] All modals designed
- [ ] All dropdowns designed
- [ ] All notifications/toasts
- [ ] Transitions between states
- [ ] Flow connections documented

### UI Consistency
- [ ] Same button styles
- [ ] Same input styles
- [ ] Same card styles
- [ ] Same spacing grid
- [ ] Same icon family
- [ ] Same transitions

### Branding
- [ ] Primary color applied
- [ ] Font family correct
- [ ] Semantic colors used
- [ ] Shadows consistent

---

## 9. DELIVERABLES

### Per Device
- [ ] Mobile designs (all pages)
- [ ] Tablet designs (key pages)
- [ ] Desktop designs (all pages)

### Components
- [ ] All modals (confirmation, form, info, success)
- [ ] All dropdowns (user menu, notifications, filters)
- [ ] All notifications (toast success/error/info, banner)
- [ ] All states (empty, loading, error)

### Files
- [ ] Figma file (all pages)
- [ ] Component library
- [ ] Design tokens
- [ ] Icon set (SVG)

### Prototype
- [ ] Key user flows
- [ ] Modal open/close animations
- [ ] Dropdown interactions
- [ ] Page transitions

**Priority:**
1. Landing (first impression)
2. Auth (entry point)
3. Core features (main value)
4. Dashboard (daily use)
5. Admin (internal)
```

---

## QUICK REFERENCE

```
UX STANDARDS
├── Contrast:    4.5:1 body | 3:1 large | 3:1 UI
├── Readability: 16px min | 50-75 chars | 1.5 line-height
├── Consistency: Same buttons | inputs | cards | icons | grid
└── Accessibility: 44px targets | Focus visible | Icon+text+color

RESPONSIVE
├── Mobile:  320-428px | 1 col | Bottom nav | Full-screen modals
├── Tablet:  640-1024px | 2 col | Collapsed sidebar | 90% modals
└── Desktop: 1024px+ | 3-4 col | Fixed sidebar | Centered modals

FULL FLOW (Design All)
├── States:      Empty | Loading | Loaded | Error | Offline
├── Modals:      Confirmation | Form | Info | Success
├── Dropdowns:   User menu | Notifications | Filters | Select
└── Toasts:      Success (3s) | Error (5s) | Info (4s)

TYPOGRAPHY
├── Scale:   H1=32 | H2=24 | H3=20 | Body=16 | Small=14 | Caption=12
├── Weight:  400 body | 500 labels | 600 headings | 700 titles
└── Height:  1.2 headings | 1.5 body

SPACING
├── Grid:    4px or 8px base
└── Scale:   4 | 8 | 16 | 24 | 32 | 48

COMPONENTS
├── Buttons: 48px | 6px radius
├── Inputs:  48px | 6px radius
└── Cards:   20px padding | 12px radius

COLORS
├── Primary:   Actions, links, focus
├── Success:   Approved, positive (green)
├── Warning:   Pending, caution (yellow)
├── Error:     Rejected, danger (red)
└── Neutral:   Gray 50-900
```

---

**Version:** 4.0 | **Format:** Universal + Responsive + Full Flow
