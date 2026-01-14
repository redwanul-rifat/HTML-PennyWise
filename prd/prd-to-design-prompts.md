---
project_name: "Crowd Builder"
total_pages: 20
design_system:
  type: "Web Application (Desktop-first, Responsive)"
  style: "Modern SaaS, Professional, Clean"
  industry: "Investment/Startup Platform"
  primary_color: "#6366F1"
  secondary_color: "#8B5CF6"
  font: "Inter"
  icons: "Lucide Icons"
---

# Crowd Builder - AURA.build Design Prompts

## Design System

Crowd Builder - Web Application (Desktop-first, Responsive) for Investment/Startup Platform.
Style: Modern SaaS, Professional, Clean with #6366F1 (Indigo) primary and #8B5CF6 (Violet) secondary colors.

**Colors:**
- Primary: #6366F1 (Indigo)
- Secondary: #8B5CF6 (Violet)
- Success: #10B981 (Emerald)
- Warning: #F59E0B (Amber)
- Error: #EF4444 (Red)
- Background: #F9FAFB (Light Gray)
- Surface: #FFFFFF (White)
- Text Primary: #111827 (Gray 900)
- Text Secondary: #6B7280 (Gray 500)
- Border: #E5E7EB (Gray 200)

**Typography:**
- Font Family: Inter
- Monospace: JetBrains Mono

**Styling:**
- Card Radius: 8px
- Button Radius: 6px
- Input Radius: 4px
- Shadow: 0 1px 3px rgba(0,0,0,0.1)
- Transition: 200ms ease
- Icons: Lucide Icons (outlined style)

---

## Page: 01-login
name: Login Page
category: auth

### SCREEN OVERVIEW
Create a login page for "Crowd Builder" - a crowd-owned startup investment platform. The login page allows returning users to authenticate via email/password or social OAuth providers (Google, Apple). Design should be clean, trustworthy, and quick to complete.

Purpose:
- Authenticate returning users
- Provide multiple login methods
- Quick access to password recovery
- Easy navigation to signup for new users

### LAYOUT INSTRUCTIONS

**OVERALL LAYOUT:**
- Split screen: 50% form (right), 50% branding panel (left)
- Form panel: White background
- Branding panel: Indigo gradient with illustration

**BRANDING PANEL (Left 50%):**
- Background: Linear gradient (indigo-600 to violet-600)
- Content (centered): Logo (white, 48px), Headline: "Welcome Back" (white, 32px), Subtext: "Turn ideas into reality with community power"
- Abstract illustration: People collaborating on ideas
- Pattern overlay: Subtle dot grid at 10% opacity

**FORM PANEL (Right 50%):**
- Content centered vertically, max-width 400px
- Top: "Sign In" (28px, bold)
- Subtitle: "Enter your credentials to continue" (14px, gray)

**FORM FIELDS (24px vertical gap):**
- Email Input: Label "Email Address", 48px height, mail icon, placeholder "you@example.com"
- Password Input: Label "Password", 48px height, lock icon, eye toggle
- Options Row: Checkbox "Remember me" (left), "Forgot Password?" link (right)
- Submit Button: "Sign In" (full-width, 48px, indigo)

**DIVIDER:** "Or continue with" with horizontal lines

**SOCIAL LOGIN ROW:**
- Google button (white bg, border)
- Apple button (black bg)

**FOOTER LINK:** "Don't have an account? Sign Up"

### KEY FEATURES
- Real-time email validation
- Password visibility toggle
- Remember me persists session
- Social OAuth redirects (Google, Apple)
- Error states: Red border, error message below field
- Loading states on buttons
- Mobile: Branding panel hidden, form full-width

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Submit Login | Click "Sign In" button | Validate fields, send auth request, show loading state |
| Login Success | Valid credentials | Store auth token, redirect to User Dashboard |
| Login Failed | Invalid credentials | Show error message below form, highlight invalid fields |
| Toggle Password Visibility | Click eye icon | Show/hide password text |
| Remember Me | Check/uncheck checkbox | Persist session token beyond browser close |
| Forgot Password | Click "Forgot Password?" link | Route to Forgot Password Page |
| Google OAuth | Click Google button | Redirect to Google OAuth flow, return with token |
| Apple OAuth | Click Apple button | Redirect to Apple OAuth flow, return with token |
| Navigate to Sign Up | Click "Sign Up" link | Route to Sign Up Page |

### BRANDING ELEMENTS
- Indigo gradient on branding panel
- Consistent input styling with brand colors
- Trust indicator: Lock icon near form
- Professional, minimal design
- Focus states use brand primary color

---

## Page: 02-signup
name: Sign Up Page
category: auth

### SCREEN OVERVIEW
Create a sign up page for "Crowd Builder" - a crowd-owned startup investment platform. The signup page allows new users to create an account via email registration or social OAuth. It collects essential information and requires agreement to terms before account creation.

Purpose:
- Register new users
- Collect necessary profile information
- Ensure legal compliance (terms acceptance)
- Provide social signup shortcuts

### LAYOUT INSTRUCTIONS

**OVERALL LAYOUT:**
- Split screen: 50% form (right), 50% branding panel (left)
- Same structure as login page for consistency

**BRANDING PANEL (Left 50%):**
- Background: Linear gradient (indigo-600 to violet-600)
- Content: Logo (white, 48px), Headline: "Join Crowd Builder" (white, 32px), Feature bullets with checkmarks
- Illustration: Person with lightbulb and upward graph

**FORM PANEL (Right 50%):**
- Header: "Create Account" (28px, bold)
- Subtitle: "Fill in your details to get started"

**SOCIAL SIGNUP (Top):**
- Google button, Apple button

**DIVIDER:** "Or register with email"

**FORM FIELDS:**
- Full Name: User icon, placeholder "John Doe", required
- Email Address: Mail icon, placeholder "you@example.com", required
- Password: Lock icon, eye toggle, password strength indicator, required
- Confirm Password: Lock icon, eye toggle, match validation, required
- Terms Checkbox: "I agree to the Terms of Service and Privacy Policy", required

**SUBMIT BUTTON:** "Create Account" (full-width, 48px, indigo)

**FOOTER:** "Already have an account? Sign In"

### KEY FEATURES
- Real-time validation on all fields
- Password strength meter updates live
- Email uniqueness check (async)
- Password match validation
- Terms must be accepted to submit
- Social signup auto-fills name/email
- Email verification sent after signup

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Submit Registration | Click "Create Account" button | Validate all fields, check email uniqueness, create account |
| Registration Success | Account created | Show "Check your email" message, send verification email |
| Registration Failed | Validation error | Show inline errors, highlight invalid fields |
| Google OAuth Signup | Click Google button | Redirect to OAuth, auto-fill name/email on return |
| Apple OAuth Signup | Click Apple button | Redirect to OAuth, auto-fill name/email on return |
| Password Strength Check | On password input | Update strength meter (Weak/Fair/Good/Strong) |
| Password Match Validation | On confirm password blur | Show match/mismatch indicator |
| Email Uniqueness Check | On email blur (debounced) | Async check if email exists, show error if taken |
| View Terms | Click "Terms of Service" link | Open Terms page in new tab or modal |
| View Privacy Policy | Click "Privacy Policy" link | Open Privacy Policy in new tab or modal |
| Navigate to Login | Click "Sign In" link | Route to Login Page |
| Toggle Password Visibility | Click eye icons | Show/hide password text |

### BRANDING ELEMENTS
- Consistent with login page styling
- Feature highlights on branding panel
- Password strength uses semantic colors (red/yellow/green)
- Clear required field indicators
- Professional, trustworthy design

---

## Page: 03-forgot-password
name: Forgot Password Page
category: auth

### SCREEN OVERVIEW
Create a forgot password page for "Crowd Builder" platform. The forgot password page allows users to initiate password recovery by entering their email address. A reset link is sent to their email.

Purpose:
- Allow users to recover access to their accounts
- Send password reset link via email
- Provide clear feedback on success/failure

### LAYOUT INSTRUCTIONS

**LAYOUT:**
- Centered card on light gray background
- Card: White, max-width 440px, 48px padding, rounded, shadow

**CARD CONTENT:**
- Back Link: "← Back to Login" (top-left, gray, 14px)
- Icon: Key icon in circle (64px, indigo-100 bg, indigo icon)
- Title: "Forgot Password?" (24px, bold, centered)
- Description: "No worries! Enter your email address and we'll send you a link to reset your password." (16px, gray, centered)
- Email Input: Label "Email Address", 48px height, mail icon
- Submit Button: "Send Reset Link" (full-width, 48px, indigo)

**SUCCESS STATE (replaces form):**
- Checkmark icon in green circle
- "Check Your Email" (24px, bold)
- "We've sent password reset instructions to [email]"
- "Didn't receive it? Resend" link
- "Back to Login" button

### KEY FEATURES
- Email validation before submit
- Rate limiting (max 3 requests per hour)
- Success message shows masked email
- Resend option after 60 seconds
- Clear error messages

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Submit Reset Request | Click "Send Reset Link" button | Validate email, send reset email, show loading state |
| Reset Request Success | Email sent successfully | Show success state with masked email |
| Reset Request Failed | Email not found/invalid | Show error message "No account found with this email" |
| Rate Limit Exceeded | Too many requests | Show warning "Too many attempts. Please try again later." |
| Resend Reset Link | Click "Resend" link (after 60s) | Send another reset email, restart countdown |
| Navigate to Login | Click "Back to Login" link/button | Route to Login Page |
| Email Validation | On input blur | Validate email format, show inline error |

### BRANDING ELEMENTS
- Clean, centered card design
- Indigo icon accent
- Success state uses green/emerald
- Consistent with auth page styling

---

## Page: 04-reset-password
name: Reset Password Page
category: auth

### SCREEN OVERVIEW
Create a reset password page for "Crowd Builder" platform. The reset password page is accessed via email link. Users create a new password with strength requirements enforced.

Purpose:
- Allow users to create a new password
- Enforce password strength requirements
- Confirm password reset success

### LAYOUT INSTRUCTIONS

**LAYOUT:**
- Centered card on light gray background
- Card: White, max-width 440px, 48px padding

**CARD CONTENT:**
- Icon: Lock icon in circle (64px, emerald-100 bg, emerald icon)
- Title: "Create New Password" (24px, bold, centered)
- Description: "Your new password must be different from your previous password."
- New Password Input: Lock icon, eye toggle, password strength bar
- Requirements Checklist: 8+ characters, 1 uppercase, 1 number, 1 special character
- Confirm Password Input: Lock icon, eye toggle, match indicator
- Submit Button: "Reset Password" (full-width, 48px, indigo)

**SUCCESS STATE:**
- Checkmark animation
- "Password Reset Successfully!"
- "Redirecting to login..." (auto-redirect 3s)
- "Go to Login" button

### KEY FEATURES
- Token validation from URL
- Expired link handling
- Real-time requirement checking
- Password match validation
- Auto-redirect on success

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Validate Token | On page load | Check reset token validity, show error if expired/invalid |
| Token Invalid | Invalid/expired token | Show error "This reset link has expired. Request a new one." |
| Submit New Password | Click "Reset Password" button | Validate requirements, update password |
| Password Reset Success | Password updated | Show success animation, auto-redirect to Login in 3s |
| Password Requirement Check | On password input | Update checklist items (green check when met) |
| Password Strength Update | On password input | Update strength bar (Weak/Fair/Good/Strong) |
| Password Match Check | On confirm password blur | Show match/mismatch indicator |
| Navigate to Login | Click "Go to Login" button | Route to Login Page immediately |
| Toggle Password Visibility | Click eye icons | Show/hide password text |

### BRANDING ELEMENTS
- Emerald/green accent for success states
- Password strength uses semantic colors
- Checklist uses brand colors
- Consistent card styling

---

## Page: 05-dashboard
name: User Dashboard
category: user

### SCREEN OVERVIEW
Create a user dashboard/home page for "Crowd Builder" platform. The dashboard is the logged-in user's home screen, showing a personalized overview of their activity, notifications, trending ideas, and quick actions.

Purpose:
- Welcome user with personalized greeting
- Show activity summary and stats
- Highlight notifications and updates
- Provide quick access to key actions
- Display trending content

### LAYOUT INSTRUCTIONS

**TOP NAVIGATION (Fixed, 64px):**
- Left: Logo "Crowd Builder"
- Center: Navigation tabs - Home (active), Browse Ideas, Submit Idea (highlighted), My Ideas, Saved
- Right: Notification bell with badge, User avatar dropdown

**MAIN CONTENT (with sidebar):**

**LEFT SIDEBAR (240px, collapsible):**
- User profile card (avatar, name, member since)
- Quick stats: Ideas Submitted, Ideas Approved, Total Votes Received
- Quick Actions: "Submit New Idea" button, "Browse Ideas" link
- Saved Ideas preview (3 items)

**MAIN CONTENT AREA:**

**WELCOME SECTION:**
- Greeting: "Welcome back, [First Name]!" (24px, bold)
- Subtitle: "Here's what's happening with your ideas"
- Date: Current date

**STATS CARDS ROW (4 cards):**
- Ideas Submitted, Pending Approval, Total Votes, Comments Received

**RECENT UPDATES SECTION:**
- Header: "Recent Activity" with "View All" link
- Timeline format activity feed

**TRENDING IDEAS SECTION:**
- Header: "Trending This Week" with "See All" link
- Horizontal card scroll (3 visible)

**YOUR RECENT ACTIVITY SECTION:**
- Tabs: "Voted On", "Commented", "Saved"
- List of 5 ideas per tab

### KEY FEATURES
- Real-time notification updates
- Collapsible sidebar for more content space
- Pull to refresh on mobile
- Activity feed updates via WebSocket
- Quick stats click-through to detailed views
- Responsive grid layout

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Navigate to Browse Ideas | Click "Browse Ideas" nav/link | Route to Browse Ideas Page |
| Navigate to Submit Idea | Click "Submit Idea" nav/button | Route to Submit Idea Page |
| Navigate to My Ideas | Click "My Ideas" nav | Route to My Ideas Page |
| Navigate to Saved | Click "Saved" nav | Route to Saved Ideas Page |
| View Notification Dropdown | Click bell icon | Show notification dropdown with latest items |
| Mark Notifications Read | Click "Mark All Read" | Clear unread badge, mark all as read |
| View All Notifications | Click "View All Notifications" link | Route to Notifications Page |
| Open User Menu | Click avatar | Show dropdown (Profile, Settings, Logout) |
| Logout | Click "Logout" in dropdown | Clear session, redirect to Landing Page |
| View Idea Detail | Click on any idea card | Route to Idea Detail Page |
| Toggle Sidebar | Click collapse button | Collapse/expand sidebar, save preference |
| View All Activity | Click "View All" link | Route to Notifications Page filtered to activity |
| Switch Activity Tab | Click tab (Voted On/Commented/Saved) | Show corresponding list of ideas |
| Stat Card Click | Click on stat card | Route to relevant filtered view |

### BRANDING ELEMENTS
- Consistent indigo accent color
- Card-based layout with soft shadows
- Status colors: Green (success), Yellow (pending), Red (rejected)
- Avatar with indigo ring for verified users
- Clean, professional dashboard aesthetic

---

## Page: 06-browse-ideas
name: Browse Ideas Page
category: user

### SCREEN OVERVIEW
Create a browse ideas page for "Crowd Builder" platform. The browse ideas page displays all public approved ideas in a filterable, searchable feed. Users can vote, save, and explore ideas from the community.

Purpose:
- Discover new startup ideas
- Filter and search ideas
- Vote on promising ideas
- Save ideas for later review

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Browse Ideas" (28px, bold)
- Subtitle: "Discover innovative startup ideas from our community"

**SEARCH & FILTER BAR (Sticky):**
- Search Input: "Search ideas, keywords, tags..."
- Filter Pills: "All Categories", "Tags", "AI Label", "Vote Range", "Date"
- Sort Dropdown: Most Voted, Newest, Oldest, Most Discussed
- "Clear All Filters" link

**RESULTS HEADER:**
- Left: "[N] Ideas Found"
- Right: View toggle - Grid (default) / List

**IDEAS GRID (Card Layout):**
- 3 columns desktop, 2 tablet, 1 mobile
- 24px gap between cards

**IDEA CARD DESIGN:**
- Thumbnail Image (16:9)
- Category Badge (top-left)
- AI Label Badge (top-right)
- Title, Description (truncated)
- Creator Row: Avatar, Name, Posted date
- Tags Row
- Actions Row: Vote Button, Comment count, Share, Save

### KEY FEATURES
- Real-time vote count updates
- Optimistic UI for voting
- Debounced search
- Filter state in URL (shareable)
- Infinite scroll with loading states
- Save for later functionality
- Share copies link to clipboard

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Search Ideas | Type in search input (debounced 300ms) | Filter results matching query, update URL |
| Apply Category Filter | Select from dropdown | Filter ideas by category, update results |
| Apply Tag Filter | Select tags (multi-select) | Filter ideas by tags, update results |
| Apply AI Label Filter | Select label type | Filter ideas by AI label (Original/Similar/Duplicate) |
| Apply Vote Range Filter | Adjust slider | Filter ideas within vote range |
| Apply Date Filter | Select date option | Filter ideas by date range |
| Clear All Filters | Click "Clear All Filters" | Reset all filters to default |
| Sort Ideas | Select sort option | Re-sort results (Most Voted/Newest/etc.) |
| Toggle View Mode | Click Grid/List toggle | Switch between grid and list layout |
| Vote on Idea | Click vote button | Toggle vote, update count (optimistic UI) |
| Save Idea | Click bookmark icon | Add to saved list, show confirmation toast |
| Unsave Idea | Click filled bookmark | Remove from saved, show undo toast |
| Share Idea | Click share icon | Copy idea URL to clipboard, show toast |
| View Idea Detail | Click on idea card/title | Route to Idea Detail Page |
| Load More Ideas | Scroll to bottom | Load next page of results (infinite scroll) |
| View Creator Profile | Click creator name/avatar | Route to Creator's public profile |

### BRANDING ELEMENTS
- Consistent card styling
- AI labels use semantic colors (green=Original, yellow=Similar, red=Duplicate)
- Vote animation (heart pulse)
- Category colors consistent throughout
- Clean, scannable layout

---

## Page: 07-idea-detail
name: Idea Detail Page
category: user

### SCREEN OVERVIEW
Create an idea detail page for "Crowd Builder" platform. The idea detail page shows the complete information about a submitted idea, including story, SWOT analysis, media, and allows voting, commenting, and sharing.

Purpose:
- Display full idea information
- Enable voting and engagement
- Facilitate discussion via comments
- Provide sharing options
- Allow reporting problematic content

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Breadcrumb: "Ideas > [Category] > [Idea Title]"
- Back button: "← Back to Ideas"

**MAIN CONTENT (2-column: 65% content, 35% sidebar):**

**LEFT COLUMN - IDEA CONTENT:**
- Header Section: Title, Meta row (badges), Creator row, Report button
- Media Gallery: Main image/video, thumbnail strip, lightbox
- Story Section: Full description (rich text)
- SWOT Analysis: 2x2 grid (Strengths/Weaknesses/Opportunities/Threats)
- Legal Ground Section
- Tags Section

**RIGHT COLUMN - SIDEBAR:**
- Vote Card (Sticky): Vote count, Vote button, Save button, Share button
- Creator Card: Avatar, name, stats, "View Profile" link
- AI Analysis Card: Label badge, explanation text

**COMMENTS SECTION (Below main, full width):**
- Header with sort dropdown
- Comment input (if logged in)
- Comments list with threaded replies
- Report modal, Share modal

### KEY FEATURES
- Image/video gallery with lightbox
- Real-time vote updates
- Threaded comments
- Rich text comment formatting
- Report functionality
- Social sharing
- Deep linking to comments

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Vote on Idea | Click vote button | Toggle vote, update count, animate heart |
| Save Idea | Click "Save for Later" button | Add to saved list, update button state |
| Share Idea | Click share button | Open share modal with link and social options |
| Copy Share Link | Click copy button in modal | Copy URL to clipboard, show toast |
| Social Share | Click Twitter/LinkedIn/Facebook | Open social share dialog with pre-filled content |
| View Media Gallery | Click thumbnail | Open lightbox with full-size media |
| Navigate Gallery | Click arrows in lightbox | Show previous/next media item |
| Close Lightbox | Click X or outside | Close lightbox, return to page |
| Play Video | Click play button | Start video playback |
| Expand Story | Click "Read more" | Expand truncated story content |
| View Creator Profile | Click creator name/avatar | Route to Creator's public profile |
| Post Comment | Click "Post Comment" button | Submit comment, add to list, clear input |
| Reply to Comment | Click "Reply" on comment | Show inline reply input |
| Submit Reply | Submit reply form | Add reply under parent comment |
| View Replies | Click "View [N] replies" | Expand nested replies |
| Hide Replies | Click "Hide replies" | Collapse nested replies |
| Report Idea | Click report flag icon | Open report modal |
| Submit Report | Submit report form | Send report to admin, show confirmation |
| Report Comment | Click report on comment | Open report modal for comment |
| Delete Own Comment | Click delete on own comment | Confirm and delete comment |
| Navigate to Tag | Click tag pill | Route to Browse Ideas filtered by tag |
| Back to Ideas | Click "← Back to Ideas" | Route to Browse Ideas Page |

### BRANDING ELEMENTS
- SWOT colors: Green (Strengths), Red (Weaknesses), Blue (Opportunities), Yellow (Threats)
- Vote button uses brand primary
- Consistent card styling
- Professional content presentation
- Clear visual hierarchy

---

## Page: 08-submit-idea
name: Submit New Idea Page
category: user

### SCREEN OVERVIEW
Create a submit new idea page for "Crowd Builder" platform. The idea submission page allows users to submit their startup/business ideas with detailed information including story, SWOT analysis, and supporting media.

Purpose:
- Collect complete idea information
- Guide users through structured submission
- Support media uploads
- Allow privacy selection
- Validate and submit for AI analysis

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Submit Your Idea" (28px, bold)
- Subtitle: "Share your entrepreneurship vision with our community"
- Progress indicator (optional)

**FORM LAYOUT:**
- Single column, max-width 720px, centered
- Sticky "Submit" bar at bottom

**SECTION 1: BASIC INFORMATION**
- Project Name: Input (required), 0/100 characters
- Category: Dropdown select (required)
- Tags: Tag input with autocomplete (required, min 3, max 10)

**SECTION 2: YOUR STORY**
- Story/Description: Rich text editor (required, min 200, max 5000)

**SECTION 3: SWOT ANALYSIS**
- 2x2 Grid: Strengths, Weaknesses, Opportunities, Threats (each required, min 50 chars)

**SECTION 4: LEGAL CONSIDERATIONS**
- Legal Ground: Textarea (required, min 50 chars)

**SECTION 5: MEDIA UPLOADS**
- Images: Drag & drop, max 10, reorderable
- Videos: Upload or YouTube URL, max 3

**SECTION 6: PRIVACY SETTING**
- Radio cards: Public (default), Private

**FORM ACTIONS (Sticky bottom):**
- "Save as Draft" (outlined), "Submit for Review" (primary), "Cancel" (text)

### KEY FEATURES
- Auto-save draft every 30 seconds
- Form validation with inline errors
- Rich text editor for story
- Drag-drop image upload with preview
- Tag autocomplete
- Character counters
- AI analysis on submission

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Enter Project Name | Type in input | Update character count, validate length |
| Select Category | Choose from dropdown | Set category value |
| Add Tag | Type and select from autocomplete | Add tag pill, update count (min 3, max 10) |
| Remove Tag | Click X on tag pill | Remove tag, update count |
| Enter Story | Type in rich text editor | Update character count, validate min length |
| Format Story Text | Use toolbar buttons | Apply formatting (bold, italic, lists, etc.) |
| Enter SWOT Field | Type in textarea | Update character count, validate min 50 |
| Enter Legal Ground | Type in textarea | Update character count, validate min 50 |
| Upload Images | Drag & drop or click upload | Upload files, show thumbnails |
| Remove Image | Click X on thumbnail | Remove image from list |
| Reorder Images | Drag thumbnail | Reorder images, first = main thumbnail |
| Upload Video | Drag & drop or click | Upload video file, show preview |
| Add YouTube URL | Paste URL | Validate and embed YouTube video |
| Remove Video | Click X on video | Remove video from list |
| Select Privacy | Click radio card | Set Public or Private visibility |
| Save Draft | Click "Save as Draft" | Save current state, show confirmation toast |
| Auto-save Draft | Every 30 seconds | Silent save, show "Saved" indicator |
| Submit Idea | Click "Submit for Review" | Validate all fields, show processing overlay |
| Validation Error | Submit with invalid fields | Scroll to first error, highlight fields |
| AI Processing | After submit | Show progress steps (Validating, AI Analysis, etc.) |
| Submission Success | Processing complete | Show success modal, redirect to My Ideas |
| Cancel Submission | Click "Cancel" | Confirm discard, route to previous page |

### BRANDING ELEMENTS
- SWOT quadrants use semantic colors
- Consistent form field styling
- Progress indicators use brand colors
- Clear section separation
- Professional form layout

---

## Page: 09-my-ideas
name: My Ideas Page
category: user

### SCREEN OVERVIEW
Create a my ideas management page for "Crowd Builder" platform. The My Ideas page shows all ideas submitted by the current user, organized by status. Users can manage their ideas, track approval status, edit submissions, and change privacy settings.

Purpose:
- View all user's submitted ideas
- Track idea status (pending, approved, rejected)
- Edit ideas and view edit history
- Manage privacy settings
- Monitor engagement metrics

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "My Ideas" (28px, bold)
- "Submit New Idea" button (primary, right)

**STATUS TABS:**
- All Ideas (count), Approved (green), Pending Approval (yellow), Rejected (red), Edits Pending (orange)

**FILTER/SORT BAR:**
- Search, Sort dropdown, View toggle (Card/Table)

**IDEAS LIST (Card View):**
- Horizontal card: Thumbnail, Title, Status Badge, Privacy Badge, Description, Stats Row, Meta Row, Actions Dropdown

**IDEAS LIST (Table View):**
- Columns: Checkbox, Thumbnail, Title, Status, Privacy, Votes, Comments, Date, Actions

**STATUS-SPECIFIC CONTENT:**
- Rejected: Show rejection reason
- Approved: Show engagement stats, privacy toggle
- Pending Edits: Show edit indicator

**EMPTY STATES:** Per-status empty state messages

**MODALS:** Change Privacy, Edit History, Delete Confirmation

### KEY FEATURES
- Status-based filtering
- Real-time status updates
- Edit tracking
- Privacy toggle for approved ideas
- Bulk actions
- Export idea data

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Navigate to Submit Idea | Click "Submit New Idea" button | Route to Submit Idea Page |
| Filter by Status | Click status tab | Filter ideas by selected status |
| Search Ideas | Type in search input | Filter ideas matching query |
| Sort Ideas | Select sort option | Re-sort ideas list |
| Toggle View Mode | Click Card/Table toggle | Switch between card and table view |
| View Idea Details | Click idea title/row | Route to Idea Detail Page |
| Edit Idea | Click "Edit Idea" in dropdown | Route to Edit Idea Page |
| Change Privacy | Click "Change Privacy" in dropdown | Open Change Privacy Modal |
| Confirm Privacy Change | Submit privacy modal | Update privacy setting, show toast |
| View Edit History | Click "View Edit History" | Open Edit History Modal |
| Delete Idea | Click "Delete" in dropdown | Open Delete Confirmation Modal |
| Confirm Delete | Confirm in delete modal | Delete idea, remove from list, show toast |
| Select Ideas (Table) | Click checkboxes | Enable bulk actions |
| Bulk Delete | Click "Delete Selected" | Confirm and delete multiple ideas |
| Export Ideas | Click "Export" (if available) | Download CSV of user's ideas |

### BRANDING ELEMENTS
- Status colors consistent throughout (Green=Approved, Yellow=Pending, Red=Rejected, Orange=Edit Pending)
- Card styling matches browse page
- Clear action affordances
- Professional table design

---

## Page: 10-edit-idea
name: Edit Idea Page
category: user

### SCREEN OVERVIEW
Create an edit idea page for "Crowd Builder" platform. The edit idea page allows users to modify their submitted ideas. All edits require admin approval before going live. The form is pre-filled with current values and tracks changes.

Purpose:
- Edit existing idea submissions
- Track changes for admin review
- Submit edit requests for approval

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Breadcrumb: "My Ideas > [Idea Name] > Edit"
- Title: "Editing: [Project Name]" (28px, bold)
- Warning banner: "Changes require admin approval before going live."

**FORM:**
- Same structure as Submit Idea page
- All fields pre-filled with current values
- Changed fields highlighted with yellow border and "Modified" badge

**CHANGE TRACKING:**
- Original value preview on hover/click

**SIDEBAR (Desktop):**
- "Edit Summary" card: Fields modified count, Current status, Last edit attempt

**FORM ACTIONS:**
- "Discard Changes" (outlined), "Submit Changes" (primary)

### KEY FEATURES
- Pre-filled form values
- Change detection and highlighting
- Side-by-side comparison option
- Discard changes confirmation
- Edit history reference

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Load Idea Data | On page load | Pre-fill all form fields with current values |
| Modify Field | Change any input | Mark field as modified, update sidebar summary |
| View Original Value | Hover/click modified field | Show original value tooltip/preview |
| Discard Changes | Click "Discard Changes" | Confirm dialog, reset to original values |
| Submit Changes | Click "Submit Changes" | Open confirmation modal with change summary |
| Confirm Edit Submission | Confirm in modal | Submit edit request, show success message |
| Edit Submission Success | Edit submitted | Show toast, redirect to My Ideas |
| Cancel Edit | Click "Cancel" or navigate away | Confirm if unsaved changes, return to My Ideas |
| View Original Idea | Click "View Original" in sidebar | Open idea detail in new tab |

### BRANDING ELEMENTS
- Yellow highlight for modified fields
- Consistent form styling with submit page
- Warning banner uses amber/yellow
- Professional change tracking UI

---

## Page: 11-saved-ideas
name: Saved Ideas Page
category: user

### SCREEN OVERVIEW
Create a saved ideas page for "Crowd Builder" platform. The saved ideas page displays all ideas the user has bookmarked for later review.

Purpose:
- View bookmarked ideas
- Manage saved collection
- Quick access to interesting ideas

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Saved Ideas" (28px, bold)
- Subtitle: "Ideas you bookmarked for later"
- Count: "You have [N] saved ideas"

**FILTER/SORT:**
- Search, Sort (Recently Saved, Most Voted, Newest), Filter by category

**IDEAS GRID:**
- Same card design as Browse Ideas
- "Unsave" button replaces "Save" button

**EMPTY STATE:**
- Illustration, "No saved ideas yet", "Browse Ideas" button

### KEY FEATURES
- Unsave with undo option
- Filter within saved
- Sort options
- Bulk unsave

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Search Saved Ideas | Type in search input | Filter saved ideas matching query |
| Sort Saved Ideas | Select sort option | Re-sort by Recently Saved/Most Voted/Newest |
| Filter by Category | Select category | Filter saved ideas by category |
| View Idea Detail | Click on idea card | Route to Idea Detail Page |
| Unsave Idea | Click "Unsave" button | Remove from saved, show undo toast |
| Undo Unsave | Click "Undo" in toast | Restore idea to saved list |
| Share Idea | Click share icon | Copy idea URL to clipboard |
| Vote on Idea | Click vote button | Toggle vote on idea |
| Navigate to Browse Ideas | Click "Browse Ideas" button (empty state) | Route to Browse Ideas Page |
| Bulk Select | Click checkboxes | Enable bulk unsave action |
| Bulk Unsave | Click "Unsave Selected" | Remove multiple ideas from saved |

### BRANDING ELEMENTS
- Consistent card styling with browse page
- Bookmark icon prominent on cards
- Undo toast uses brand colors
- Clean, organized layout

---

## Page: 12-notifications
name: Notifications Page
category: user

### SCREEN OVERVIEW
Create a notifications page for "Crowd Builder" platform. The notifications page displays all user notifications organized by type and time.

Purpose:
- View all notifications
- Filter by notification type
- Manage notification preferences

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Notifications" (28px, bold)
- "Mark All as Read" button (right)
- Settings icon (notification preferences)

**FILTER TABS:**
- All, Idea Updates, Comments, Admin, Reports (each with unread count)

**NOTIFICATION LIST:**
- Grouped by date: Today, Yesterday, This Week, Earlier

**NOTIFICATION ITEM:**
- Icon (colored by type), Content (title, subtitle), Timestamp
- Unread: Light indigo background
- Click to navigate

**EMPTY STATE:** "No notifications yet"

**SETTINGS MODAL:** Email/push notification toggles

### KEY FEATURES
- Real-time updates
- Mark individual/all as read
- Filter by type
- Click to navigate
- Notification preferences

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Filter Notifications | Click filter tab | Show notifications of selected type |
| Mark All Read | Click "Mark All as Read" | Clear all unread states, update badges |
| Mark Single Read | Click on notification | Mark as read, navigate to related content |
| Navigate from Notification | Click notification | Route to related page (idea, comment, etc.) |
| Delete Notification | Swipe or click delete | Remove notification from list |
| Open Settings | Click settings icon | Open notification preferences modal |
| Toggle Email Notifications | Toggle switches in modal | Update email notification preferences |
| Toggle Push Notifications | Toggle switches in modal | Update push notification preferences |
| Save Preferences | Close settings modal | Save notification preference changes |

### BRANDING ELEMENTS
- Notification type colors (Green=Approved, Blue=Comment, Indigo=Admin, Red=Report)
- Unread state uses light indigo background
- Clean timeline layout
- Consistent with dashboard styling

---

## Page: 13-profile-settings
name: Profile & Settings Page
category: user

### SCREEN OVERVIEW
Create a profile and settings page for "Crowd Builder" platform. The profile/settings page allows users to manage their account information, preferences, security settings, and view account statistics.

Purpose:
- Manage personal profile
- Update account security
- Configure email preferences
- Control privacy settings
- Account deletion option

### LAYOUT INSTRUCTIONS

**LAYOUT:**
- Sidebar navigation (left, 240px)
- Content area (right)

**SIDEBAR MENU:**
- Profile, Account Settings, Email Preferences, Privacy, Language, Danger Zone

**PROFILE SECTION:**
- Avatar (96px, editable), Name, Bio, Email (display only), Member since
- Statistics card: Ideas submitted, approved, votes received/given, comments

**ACCOUNT SETTINGS SECTION:**
- Change Password: Current, New, Confirm
- Linked Accounts: Google, Apple (connect/disconnect)

**EMAIL PREFERENCES SECTION:**
- Toggle switches for notification types

**PRIVACY SECTION:**
- Profile visibility, Show statistics, Show saved ideas

**LANGUAGE SECTION:**
- Language dropdown

**DANGER ZONE:**
- Delete Account button (red)

### KEY FEATURES
- Avatar upload with crop
- Real-time save indication
- Password strength validation
- OAuth account linking
- Granular notification control
- Account deletion flow

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Switch Settings Section | Click sidebar menu item | Show corresponding settings panel |
| Upload Avatar | Click avatar / "Change Photo" | Open file picker, then crop modal |
| Crop Avatar | Adjust crop area | Preview cropped image |
| Save Avatar | Confirm crop | Upload and update avatar |
| Update Name | Edit name field | Enable "Save Changes" button |
| Update Bio | Edit bio textarea | Enable "Save Changes" button |
| Save Profile Changes | Click "Save Changes" | Save updates, show confirmation toast |
| Change Password | Fill password fields | Validate strength, enable update button |
| Update Password | Click "Update Password" | Validate current password, update, show toast |
| Connect Google | Click "Connect" on Google row | Redirect to Google OAuth, link on return |
| Connect Apple | Click "Connect" on Apple row | Redirect to Apple OAuth, link on return |
| Disconnect Account | Click "Disconnect" on linked account | Confirm (if has password), unlink account |
| Toggle Email Preference | Click toggle switch | Update preference, auto-save |
| Toggle Privacy Setting | Click toggle switch | Update privacy setting, auto-save |
| Change Language | Select from dropdown | Apply language change, refresh page |
| Delete Account | Click "Delete My Account" | Open confirmation modal with password |
| Confirm Account Deletion | Enter password, confirm | Delete account, logout, redirect to landing |

### BRANDING ELEMENTS
- Consistent sidebar navigation
- Form styling matches other pages
- Danger Zone uses red accent
- Clean, organized settings layout
- Profile statistics use brand colors

---

## Page: 14-admin-dashboard
name: Admin Dashboard Home
category: admin

### SCREEN OVERVIEW
Create an admin dashboard home page for "Crowd Builder" platform. The admin dashboard provides a comprehensive overview of platform activity, pending tasks, and quick access to management functions.

Purpose:
- Overview of platform metrics
- Quick access to pending tasks
- Activity monitoring
- Key performance indicators

### LAYOUT INSTRUCTIONS

**ADMIN NAVIGATION (Sidebar, 260px, Dark):**
- Logo: "Crowd Builder Admin"
- Menu sections: Overview, Review (Pending Ideas, Pending Edits), Management (All Ideas, Users, Comments), Reports, Content (CMS, Categories/Tags), Analytics, Settings
- Badge counts on pending items
- Collapse button

**MAIN CONTENT:**

**TOP BAR:**
- Search, Channel Talk button, Admin avatar dropdown

**WELCOME HEADER:**
- "Welcome back, [Admin Name]", Date

**OVERVIEW CARDS (4 columns):**
- Pending Ideas (yellow), Pending Edits (orange), Unresolved Reports (red), Active Users (green)
- Each with number, label, trend, action link

**CHARTS ROW:**
- Ideas Over Time (line chart, 60% width)
- Category Distribution (pie chart, 40% width)

**BOTTOM ROW:**
- Recent Activity feed (60%)
- Top Ideas This Week (40%)

### KEY FEATURES
- Real-time metric updates
- Interactive charts
- Quick action links
- Activity feed
- Responsive sidebar
- Badge counts for pending items

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Navigate to Pending Ideas | Click "Pending Ideas" menu or card | Route to Pending Ideas Queue |
| Navigate to Pending Edits | Click "Pending Edits" menu or card | Route to Edit Approvals Queue |
| Navigate to Reports | Click "Reports" menu or card | Route to Reports Center |
| Navigate to User Management | Click "Users" menu | Route to User Management Page |
| Navigate to Analytics | Click "Analytics" menu | Route to Analytics Dashboard |
| Navigate to CMS | Click "CMS Pages" menu | Route to CMS Management Page |
| Toggle Sidebar | Click collapse button | Collapse/expand sidebar |
| View Activity Item | Click activity feed item | Route to related content |
| View All Activity | Click "View All" on activity | Route to full activity log |
| Review Trending Idea | Click "Review" on trending idea | Route to Idea Detail (admin view) |
| Change Chart Date Range | Select date filter | Update chart data |
| Admin Search | Type in search bar | Search ideas, users across platform |
| Open Channel Talk | Click Channel Talk button | Open support chat widget |
| Logout | Click Logout in dropdown | Clear admin session, redirect to login |

### BRANDING ELEMENTS
- Dark sidebar with light text
- Overview cards use semantic colors
- Clean chart styling
- Professional admin aesthetic
- Badge counts use alert colors

---

## Page: 15-admin-pending-ideas
name: Pending Ideas Queue
category: admin

### SCREEN OVERVIEW
Create a pending ideas review page for "Crowd Builder" admin dashboard. The pending ideas queue shows all ideas awaiting admin approval, with AI analysis results and quick action capabilities.

Purpose:
- Review submitted ideas
- View AI analysis and labels
- Approve or reject ideas
- Manage idea queue efficiently

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Pending Ideas" (24px, bold)
- Count badge: "[N] awaiting review"

**FILTER BAR:**
- Date range, Category filter, AI Label filter, Privacy filter, Sort options

**BULK ACTIONS (when selected):**
- Select all, "Approve Selected", "Reject Selected", "Delete Selected"

**IDEAS TABLE:**
- Columns: Checkbox, Thumbnail, Idea Info (title, creator, date), Category, AI Labels, Privacy, Votes, Reports, Actions dropdown

**IDEA DETAIL MODAL/SLIDE-OVER:**
- Header: Title, Status, Close
- AI Analysis Panel: Summary, Labels, Risk Flags
- Tabs: Summary View, Full Details, Creator Info
- Admin Actions Panel: Accept, Reject (with reason), Request More Info, Change Privacy, Delete
- Admin Notes Section

### KEY FEATURES
- AI-powered summaries
- Bulk actions
- Side-by-side comparison for duplicates
- Quick action buttons
- Admin notes
- Report indicators

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Filter Ideas | Apply filter options | Update table with filtered results |
| Sort Ideas | Select sort option | Re-sort table |
| Select Idea | Click checkbox | Enable bulk actions |
| Select All | Click "Select All" checkbox | Select all visible ideas |
| View Idea Summary | Click "View Summary" in dropdown | Open modal with AI summary tab |
| View Full Details | Click "View Details" or idea title | Open modal with full details tab |
| Approve Idea | Click "Accept" button | Confirm, approve idea, send notification to creator |
| Bulk Approve | Click "Approve Selected" | Confirm, approve all selected ideas |
| Reject Idea | Click "Reject" button | Open rejection form with reason dropdown |
| Submit Rejection | Select reason, add notes, submit | Reject idea, send notification with reason |
| Bulk Reject | Click "Reject Selected" | Select common reason, reject all selected |
| Request More Info | Click "Request More Info" | Open Channel Talk composer with creator |
| Change Privacy | Click "Change Privacy" | Toggle Public/Private setting |
| Delete Idea | Click "Delete" | Confirm deletion, remove from queue |
| Add Admin Note | Type in notes section | Save internal note (admin-only visible) |
| View Similar Ideas | Click link in AI Analysis | Open comparison view with similar ideas |
| Contact Creator | Click "Contact Creator" | Open Channel Talk with creator |

### BRANDING ELEMENTS
- AI labels use semantic colors (Green=Original, Yellow=Similar, Red=Duplicate)
- Report indicators use red accent
- Professional table styling
- Modal uses consistent admin styling

---

## Page: 16-admin-edit-approvals
name: Edit Approvals Queue
category: admin

### SCREEN OVERVIEW
Create an edit approvals page for "Crowd Builder" admin dashboard. The edit approvals page shows all pending edit requests with side-by-side comparison of original and edited versions.

Purpose:
- Review edit requests
- Compare original vs edited content
- Approve or reject edits
- Maintain content quality

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Edit Approvals"
- Count: "[N] pending"

**EDITS TABLE:**
- Columns: Idea Name, Submitter, Fields Changed, Edit Date, Original Status, Actions

**EDIT REVIEW INTERFACE:**
- Header: "Edit Request: [Idea Name]", Submitter info, Edit date, Status
- Comparison View: Split screen (Original left, Edited right), Changed fields highlighted
- Field-by-Field Review: Expandable list with individual approve/reject toggles
- Admin Actions: Approve All, Approve Partial, Reject All, Request Clarification

### KEY FEATURES
- Side-by-side diff view
- Field-level approval
- Change highlighting
- Reason required for rejection

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| View Edit Request | Click on table row | Open edit review interface |
| Toggle Comparison View | Click view toggle | Switch between side-by-side and unified view |
| Expand Field Details | Click field row | Show original and new values |
| Approve Single Field | Toggle field approval | Mark field for approval |
| Reject Single Field | Toggle field rejection | Mark field for rejection |
| Approve All Changes | Click "Approve All Changes" | Approve entire edit, update idea |
| Approve Partial | Click "Approve Partial" | Approve selected fields only |
| Reject All Changes | Click "Reject All" | Open rejection reason form |
| Submit Rejection | Enter reason, submit | Reject edit, notify user with reason |
| Request Clarification | Click "Request Clarification" | Open Channel Talk with user |
| Add Admin Note | Type in notes field | Save internal note about edit |

### BRANDING ELEMENTS
- Yellow highlight for changed fields
- Green/red for approved/rejected fields
- Professional diff view styling
- Consistent admin panel design

---

## Page: 17-admin-reports
name: Reports Center
category: admin

### SCREEN OVERVIEW
Create a reports center page for "Crowd Builder" admin dashboard. The reports center manages all reported content (ideas, comments, users) with filtering, review, and action capabilities.

Purpose:
- Manage reported content
- Review report details
- Take moderation actions
- Maintain community safety

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Reports Center"
- Total unresolved count

**TABS:**
- Idea Reports ([N]), Comment Reports ([N]), User Reports ([N])

**FILTER BAR:**
- Date range, Report category, Status (New, Under Review, Resolved, Dismissed), Sort

**REPORTS TABLE (per tab):**
- Idea Reports: Thumbnail, Title, Report Count, Categories, First Reported, Status, Actions
- Comment Reports: Comment Preview, Commenter, Idea, Report Count, Categories, Status, Actions
- User Reports: Avatar+Name, Report Count, Categories, Account Status, Status, Actions

**REPORT DETAIL VIEW:**
- Reported Item preview
- All Reports list (grouped by category)
- Statistics: Total reports, Unique reporters, Category breakdown
- Admin Actions (varies by type)
- Decision Log

### KEY FEATURES
- Tabbed report types
- Bulk dismiss
- Action logging
- User history view
- Report statistics

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Switch Report Type | Click tab | Show reports of selected type |
| Filter Reports | Apply filters | Update table with filtered results |
| View Report Detail | Click on report row | Open report detail view |
| View Reported Content | Click "View in Context" | Open idea/comment in new tab |
| View Reporter Profile | Click reporter name | Open user profile |
| Delete Reported Idea | Click "Delete Idea" | Confirm, delete idea, resolve report |
| Make Idea Private | Click "Change to Private" | Update visibility, resolve report |
| Warn Creator | Click "Warn Creator" | Open warning composer, send warning |
| Delete Comment | Click "Delete Comment" | Confirm, delete comment, resolve report |
| Warn User | Click "Warn User" | Open warning composer, send warning |
| Ban User (Temporary) | Click "Temporary Ban" | Set ban duration, apply ban |
| Ban User (Permanent) | Click "Permanent Ban" | Confirm, apply permanent ban |
| Dismiss Report | Click "Dismiss" | Mark report as dismissed, no action |
| Bulk Dismiss | Select multiple, click "Dismiss Selected" | Dismiss all selected reports |
| Add Decision Notes | Type in decision log | Record action taken and reasoning |
| View User History | Click "View History" | Show user's past reports and warnings |

### BRANDING ELEMENTS
- Report severity indicated by color
- Warning/ban actions use red accent
- Professional moderation interface
- Clear action logging display

---

## Page: 18-admin-users
name: User Management
category: admin

### SCREEN OVERVIEW
Create a user management page for "Crowd Builder" admin dashboard. The user management page allows admins to view, search, filter, and manage all platform users including banning and account administration.

Purpose:
- View all platform users
- Search and filter users
- Manage user accounts
- Handle bans and warnings

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "User Management"
- Export CSV button

**FILTER BAR:**
- Search by name/email, Status filter (All, Active, Banned, Suspended), Date range, Sort

**USERS TABLE:**
- Columns: Checkbox, Avatar+Name+Email, Status badge, Ideas Submitted, Reports Received, Warnings, Joined Date, Last Active, Actions dropdown

**USER DETAIL MODAL:**
- Profile Section: Avatar, Name, Email, Status, Member since, Last active
- Statistics: Ideas, Votes, Comments, Reports, Warnings
- Tabs: Ideas, Comments, Activity, Reports & Warnings
- Admin Actions: Edit Profile, Ban User, Send Warning, Reset Password, Delete Account, Contact
- Admin Notes section

### KEY FEATURES
- Bulk actions
- User search
- Activity history
- Warning/ban management
- Admin notes
- Action audit log

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Search Users | Type in search input | Filter users by name or email |
| Filter by Status | Select status option | Show users with selected status |
| Sort Users | Select sort option | Re-sort users table |
| View User Detail | Click on user row | Open user detail modal |
| View User Ideas | Click "Ideas" tab in modal | Show user's submitted ideas |
| View User Comments | Click "Comments" tab | Show user's comments |
| View User Activity | Click "Activity" tab | Show user's activity log |
| View User Reports | Click "Reports & Warnings" tab | Show reports and warnings |
| Send Warning | Click "Send Warning" | Open warning composer, send to user |
| Temporary Ban | Click "Ban User" > "Temporary" | Set duration, apply ban, notify user |
| Permanent Ban | Click "Ban User" > "Permanent" | Confirm, apply permanent ban |
| Unban User | Click "Unban User" | Remove ban, restore account access |
| Reset Password | Click "Reset Password" | Send password reset email to user |
| Delete Account | Click "Delete Account" | Confirm, delete user and content |
| Contact User | Click "Contact User" | Open Channel Talk with user |
| Export Users | Click "Export CSV" | Download CSV of filtered users |
| Bulk Select | Click checkboxes | Enable bulk actions |
| Bulk Ban | Click "Ban Selected" | Apply ban to all selected users |
| Add Admin Note | Type in notes section | Save internal note about user |

### BRANDING ELEMENTS
- Status badges use semantic colors
- Ban/warning actions use red accent
- Professional table and modal design
- Clean user profile display

---

## Page: 19-admin-cms
name: CMS Content Management
category: admin

### SCREEN OVERVIEW
Create a CMS content management page for "Crowd Builder" admin dashboard. The CMS page allows admins to edit platform content pages like Landing Page, Terms, Privacy Policy, and FAQ.

Purpose:
- Manage platform content pages
- Edit and publish content
- Maintain version history
- Control SEO settings

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Content Management"

**PAGES LIST:**
- Card for each page: Name, Last updated, Status (Published/Draft), Actions (Edit, Preview, Publish)

**EDITABLE PAGES:**
- Landing Page, How It Works, About Us, Terms of Service, Privacy Policy, Community Guidelines, FAQ, Contact Us

**PAGE EDITOR:**
- Header: Page title, Status badge, Last saved
- Toolbar: Save Draft, Preview, Publish, Version History
- Editor: Rich text WYSIWYG with HTML toggle
- Image Library: Upload and manage images
- Preview Panel: Live preview (collapsible)
- Version History: List with restore option
- SEO Settings: Meta title, description, OG image

### KEY FEATURES
- Rich text editing
- Version history
- Preview before publish
- SEO settings
- Image management
- Draft/publish workflow

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Select Page to Edit | Click "Edit" on page card | Open page editor |
| Edit Content | Type in WYSIWYG editor | Update content, enable Save button |
| Format Text | Use toolbar buttons | Apply formatting (headings, bold, lists, etc.) |
| Toggle HTML View | Click HTML toggle | Switch between visual and HTML editing |
| Insert Image | Click image button | Open image library picker |
| Upload Image | Drag/drop or click upload | Upload to image library |
| Save Draft | Click "Save Draft" | Save current state as draft |
| Auto-save | Every 60 seconds while editing | Silent save, show "Saved" indicator |
| Preview Page | Click "Preview" | Open preview in split pane or new tab |
| Publish Page | Click "Publish" | Make current version live |
| Unpublish Page | Click "Unpublish" | Revert to draft, remove from live site |
| View Version History | Click "Version History" | Show list of previous versions |
| Restore Version | Click "Restore" on version | Replace current with selected version |
| Compare Versions | Select two versions | Show side-by-side comparison |
| Update SEO Settings | Edit meta fields | Update SEO metadata |
| Upload OG Image | Click OG image upload | Set social sharing image |

### BRANDING ELEMENTS
- Clean editor interface
- Draft/Published status badges
- Professional version history UI
- Consistent admin styling

---

## Page: 20-admin-analytics
name: Analytics Dashboard
category: admin

### SCREEN OVERVIEW
Create an analytics dashboard page for "Crowd Builder" admin dashboard. The analytics dashboard provides comprehensive platform metrics, trends, and insights for monitoring platform health and growth.

Purpose:
- Monitor platform metrics
- Track growth trends
- Analyze user engagement
- Generate reports

### LAYOUT INSTRUCTIONS

**PAGE HEADER:**
- Title: "Platform Analytics"
- Date range picker: Last 7 days, 30 days, 3 months, Custom

**KEY METRICS ROW:**
- Total Users (trend), Total Ideas (trend), Total Votes Cast (trend), Active Users (today), Avg Votes per Idea

**CHARTS SECTION:**
- User Growth Chart: Line chart, new registrations, cumulative users
- Idea Submission Chart: Bar chart, submissions per period, status breakdown
- Engagement Chart: Line chart, votes and comments over time
- Category Distribution: Pie chart
- AI Label Distribution: Bar chart (Original/Similar/Duplicate)

**LISTS SECTION:**
- Top Voted Ideas: Rank, Title, Votes, Creator (Top 10)
- Most Active Users: Rank, User, Activity score (Top 10)
- Reports Summary: Total, by status, by type, avg resolution time

**EXPORT OPTIONS:**
- Export to CSV, Generate PDF Report, Schedule email reports

### KEY FEATURES
- Interactive charts
- Date range filtering
- Export capabilities
- Trend indicators
- Comparative analysis

### MAIN ACTIONS
| Action | Trigger | Behavior |
|--------|---------|----------|
| Change Date Range | Select from date picker | Update all metrics and charts |
| Select Custom Date Range | Click "Custom", pick dates | Apply custom date filter |
| Hover Chart Data Point | Mouse over chart | Show tooltip with detailed data |
| Click Chart Segment | Click pie/bar segment | Filter related data, show details |
| View Idea Detail | Click idea in top list | Route to Idea Detail Page |
| View User Detail | Click user in top list | Route to User Management detail |
| Export to CSV | Click "Export to CSV" | Download current data as CSV |
| Generate PDF Report | Click "Generate PDF Report" | Create and download PDF summary |
| Schedule Email Report | Click "Schedule email reports" | Open scheduling modal |
| Configure Report Schedule | Set frequency, recipients | Save automated report settings |
| Refresh Data | Click refresh icon | Reload all analytics data |
| Compare Periods | Enable comparison mode | Show current vs previous period |

### BRANDING ELEMENTS
- Clean chart styling with brand colors
- Trend indicators (green up, red down)
- Professional analytics layout
- Consistent with admin dashboard theme

---
