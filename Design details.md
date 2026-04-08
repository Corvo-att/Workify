# **Workify — Design Document & Product Requirements**

---

## **1\. Brand Identity & Design Philosophy**

**Core Feel:** Sharp edges meet soft comfort. Think of a well-lit co-working space — productive, warm, and trustworthy. The UI should feel like a premium tool that doesn't intimidate.

**Design Principles:**

* **Clarity over clutter** — every element earns its place  
* **Role-aware UI** — freelancers and clients should feel the interface "knows" them  
* **Progressive disclosure** — complex flows (like posting a job) are broken into digestible steps  
* **Motion with purpose** — subtle transitions, no gratuitous animation

---

## **2\. Visual Language**

### **Color Palette**

| Token | Hex | Usage |
| ----- | ----- | ----- |
| `--primary` | `#5B4FE9` | Buttons, active states, links |
| `--primary-light` | `#7B72F0` | Hover states, secondary CTAs |
| `--accent` | `#F97316` | Badges, "hot" tags, earnings highlights |
| `--bg-base` | `#0F0E17` | Dark base background |
| `--bg-surface` | `#1A1928` | Cards, sidebars, panels |
| `--bg-elevated` | `#232236` | Modals, dropdowns |
| `--text-primary` | `#F5F4FF` | Headlines, body |
| `--text-muted` | `#8B8AA8` | Labels, placeholders, meta |
| `--success` | `#22C55E` | Payment released, contract active |
| `--warning` | `#EAB308` | In review, pending |
| `--danger` | `#EF4444` | Disputes, declines |

**Gradient Definitions:**

* **Hero gradient:** `linear-gradient(135deg, #5B4FE9 0%, #A78BFA 50%, #F97316 100%)`  
* **Card shimmer:** `linear-gradient(135deg, #1A1928 0%, #232236 100%)`  
* **CTA button:** `linear-gradient(90deg, #5B4FE9, #7B72F0)` with a subtle glow on hover  
* **Earnings/finance accent:** `linear-gradient(135deg, #22C55E20, #22C55E05)` — soft green wash behind financial figures

### **Typography**

| Role | Font | Weight | Size |
| ----- | ----- | ----- | ----- |
| Display / Hero | **Sora** | 700–800 | 48–72px |
| Headings | **Sora** | 600 | 24–36px |
| Body | **Inter** | 400–500 | 14–16px |
| Mono (code, IDs) | **JetBrains Mono** | 400 | 13px |
| Labels / Caps | **Inter** | 600 | 11px, `letter-spacing: 0.08em` |

### **Spacing & Shape**

* **Border radius:** `12px` for cards, `8px` for inputs, `999px` for pills/badges, `16px` for modals  
* **Spacing scale:** 4px base unit (4, 8, 12, 16, 24, 32, 48, 64\)  
* **Card elevation:** `box-shadow: 0 4px 24px rgba(0,0,0,0.4)` — cards float subtly above the background  
* **Dividers:** `1px solid rgba(255,255,255,0.06)` — barely-there separators

### **Iconography**

* Library: **Lucide Icons** — consistent stroke weight, clean and modern  
* Size standard: `20px` inline, `24px` standalone, `16px` in dense tables

---

## **3\. Layout System**

* **Grid:** 12-column, `max-width: 1280px`, `gap: 24px`  
* **Sidebar (authenticated):** `260px` fixed left, collapsible to `64px` icon rail on smaller screens  
* **Content area:** fluid, right of sidebar  
*  **Topbar:** `64px` height, sticky, backdrop blur (`blur(12px)` with `bg-opacity: 80%`)

---

## **4\. Page-by-Page Requirements**

---

### **4.1 Public & Discovery Pages**

#### **Landing Page**

* **Hero Section:** Full-width, uses the hero gradient as an animated subtle mesh background. Large headline (`"Work. Without Limits."`), subheading, and two pill-shaped CTAs side by side — `"Hire Talent"` (primary gradient button) and `"Find Work"` (ghost/outline button).  
* **Trust Bar:** Scrolling marquee of logos or stats — `"$2.4M+ paid out"`, `"12,000+ freelancers"`, etc.  
* **Trending Categories:** Horizontal scroll of category cards with icon \+ label \+ job count badge. Cards use the card shimmer gradient.  
* **Testimonials:** 3-column grid of quote cards. Each card has an avatar, star rating, and a subtle left-border accent in `--primary`.  
* **Footer:** Dark, minimal. Three link columns, social icons, and the Workify wordmark with tagline.

#### **Browse Jobs**

* **Layout:** Left sidebar for filters (280px), main content is a responsive card grid (2-col on desktop).  
* **Filter Panel:** Budget type toggle (Fixed / Hourly), experience level chips (Entry / Mid / Expert), category multi-select, budget range slider with gradient fill.  
* **Job Card:** Company logo, job title, category tag, budget badge (orange accent), truncated description, posted date, and a quick "Save" heart icon.  
* **Search bar:** Full-width at top, with category dropdown baked in. Subtle inner glow on focus.

#### **Browse Talent**

* Same filter layout as Browse Jobs but filters are: skills, hourly rate range, availability toggle.  
* **Freelancer Card:** Avatar with online indicator dot, name, headline, skill chips (max 4 visible, `+N more`), star rating, hourly rate in accent color, and a `"View Profile"` button.

#### **How It Works**

* Two-tab toggle at top: **"I'm a Client"** / **"I'm a Freelancer"**  
* Numbered step flow for each — large step number in gradient text, icon, title, and description.  
* CTA at the bottom of each path leading to registration.

---

### **4.2 Authentication & Onboarding**

#### **Login / Register**

* Split-screen: left side is a decorative panel using the hero gradient with a floating testimonial card; right side is the form.  
* Form inputs: dark background (`--bg-elevated`), `1px` border that glows `--primary` on focus.  
* OAuth options: `"Continue with Google"` and `"Continue with GitHub"` — ghost buttons with logos.

#### **Role Selection**

* Two large, clickable cards centered on a clean background. Each card has an icon, role title, and a short description. Selected card gets a `--primary` border glow and a soft checkmark overlay. Unselected dims slightly.

#### **Freelancer Profile Setup (Multi-step)**

* Progress bar at top using gradient fill.  
* **Step 1:** Name, headline, professional bio (textarea with character count)  
* **Step 2:** Skills input (tag-based, typeahead search), hourly rate input  
* **Step 3:** Portfolio links (dynamic add/remove rows), profile photo upload with crop  
* Each step has a "Back" ghost button and a "Continue" primary button.

#### **Client Company Profile**

* Single-page form (not multi-step — clients want to get to posting fast).  
* Fields: Company name, industry dropdown, website URL, team size selector (pill buttons), payment method verification (Stripe-embedded flow).

---

### **4.3 Freelancer Workspace**

#### **Freelancer Dashboard**

* **Greeting header:** `"Good morning, [Name]"` with current date.  
* **Stat cards (row of 4):** Active Proposals, Interview Invites, Active Contracts, Total Earned — each with a mini trend sparkline and the earnings card using the green wash gradient.  
* **Quick actions:** `"Browse New Jobs"` and `"Edit Profile"` — outline buttons.  
* **Activity Feed:** Right column showing recent events (proposal viewed, message received, payment released) with timestamps and color-coded left-border indicators.

#### **Job Details Page**

* Full-width header with job title, company name, posted date, and "Save Job" toggle.  
* **Two-column layout:** Left (70%) has the full description, required skills list, and project scope. Right (30%) is a sticky card showing budget, duration, client stats (rating, total spent, hire rate, member since), and the `"Apply Now"` gradient CTA button.  
* Client's recent reviews visible below in a collapsed accordion.

#### **Proposal Submission Page**

* Clean, focused single-column form (no sidebar distraction).  
* Fields: Cover letter (rich textarea), Bid Amount (with a note showing the client's stated budget), Proposed Timeline (date picker), Milestones (dynamic add/remove rows with amount \+ description per milestone).  
* Live preview pane on the right showing how the proposal will appear to the client.

#### **My Proposals**

* Tab bar: `Submitted` / `Active` / `Archived`  
* Table layout with columns: Job Title, Client, Bid Amount, Date Submitted, Status badge.  
* Status badges are color-coded pills: yellow \= Pending, green \= Active, gray \= Archived, red \= Declined.  
* Row click expands an inline detail panel showing the cover letter and client response.

#### **Active Contracts**

* Card per contract showing project name, client, current milestone, and deadline.  
* Inside each contract: milestone tracker (a visual stepper), a `"Submit for Review"` button per milestone, and a link to the chat room.

---

### **4.4 Client Workspace**

#### **Client Dashboard**

* **Stat cards:** Active Postings, New Applicants, In Progress Contracts, Total Spent.  
* **Quick action:** Large `"Post a New Job"` gradient button — prominent, always visible.  
* **Jobs Overview table:** Listing of active jobs with applicant count, status, and a `"Review Applicants"` CTA inline.

#### **Post a Job Wizard**

* Step 1 — **Title & Category:** Job title input, category dropdown, sub-category. Simple and fast.  
* Step 2 — **Description & Skills:** Rich text editor for description, required skills tag input, experience level selector (3 pill options).  
* Step 3 — **Budget & Duration:** Toggle between Fixed Price / Hourly Rate. Budget input. Project duration dropdown. Visibility toggle (public / invite-only).  
* Sticky right panel throughout showing a live "job preview card" so the client sees exactly what freelancers will see.  
* Final review screen before publishing — summary of all inputs with an `"Edit"` link per section.

#### **Review Proposals**

* Split layout: left column lists all applicants (avatar, name, bid, rating, top skills), right panel shows the selected applicant's full proposal.  
* Action buttons per applicant: `"Shortlist"` (adds a star), `"Message"`, `"Decline"` (soft — just removes from main view, doesn't notify).  
* Shortlisted tab at top for fast comparison.

#### **Hire / Offer Page**

* Clear contract summary: Freelancer name \+ avatar, role, agreed rate, start date.  
* Milestone table: define up to 10 milestones with amount \+ due date per row. Total auto-calculates.  
* Escrow info box — explains that funds are held safely until milestone approval. Uses a soft blue-tinted info card.  
* `"Confirm & Deposit"` primary CTA at bottom. Stripe integration here.

---

### **4.5 Collaboration & Finance**

#### **Messages / Chat Room**

* **Layout:** Left rail is conversation list (compact, shows avatar, name, last message snippet, unread badge). Right is the active chat.  
* Chat bubbles: sent messages use `--primary` gradient background, received use `--bg-elevated`.  
* Support for file attachments and inline image previews.  
* The top of chat shows a context bar: project name, contract status, and a quick link to the contract page.  
* Real-time via WebSocket (Socket.io or Supabase Realtime).

#### **Contract Management Page**

* Central "source of truth" card at top: both parties' names/avatars, project title, total contract value, start date.  
* **Milestone Tracker:** Vertical stepper. Each milestone shows: amount, description, status badge (Funded / Submitted / In Review / Released), and action button (context-aware — `"Release Payment"` for client, `"Submit Work"` for freelancer).  
* Funded amounts show a subtle green left-bar; in-review shows yellow.  
* Full message thread embedded at the bottom.

#### **Wallet / Transaction History**

* **Balance card:** Large display of available balance using the green gradient wash. `"Withdraw"` and `"Add Funds"` buttons.  
* **Transaction table:** Date, description, type (Credit/Debit), amount, status. Credits in green, debits in muted red.  
* Filterable by date range and type.  
* CSV export button (ghost, top-right of table).

#### **Dispute Center**

* Flag form with: reason category (dropdown), description textarea, evidence upload (up to 5 files).  
* Severity indicator (Low / Medium / High) displayed as colored pills — client selects one.  
* After submission, a case number is assigned, and a status tracker is shown (`Filed → Under Review → Resolved`).

---

### **4.6 Admin Panel**

* **Separate visual theme:** Same dark base but uses a red-tinted `--admin-accent: #E11D48` instead of purple for admin-specific UI elements. This reinforces "this is a power tool."  
* **User Management table:** Search, filter by role/status, inline `Ban`, `Verify`, `Impersonate` actions per row.  
* **Job Moderation queue:** Flagged jobs listed with reason, reporter, and `Approve / Remove / Escalate` actions.  
* **Financial Overview:** KPI cards — Total Escrow Held, Fees Collected (MTD), Pending Withdrawals. Line chart for fee revenue over time.

---

## **5\. Component Library Highlights**

| Component | Notes |
| ----- | ----- |
| `<GradientButton>` | Primary CTA, `linear-gradient` fill, lifts on hover with box-shadow glow |
| `<StatCard>` | Icon \+ label \+ value \+ sparkline, supports color variants |
| `<ProposalCard>` | Freelancer summary card used in Review Proposals |
| `<MilestoneTracker>` | Vertical stepper, status-aware |
| `<SkillChip>` | Pill tag, removable in edit mode |
| `<StatusBadge>` | Color-coded status pill, predefined variants |
| `<AvatarWithIndicator>` | Online/offline dot, ring variant for profile pages |
| `<FileUploadZone>` | Drag-and-drop area with dashed gradient border |

---

## **6\. Responsive Behavior**

* **Desktop (1280px+):** Full sidebar \+ multi-column layouts as described.  
* **Tablet (768–1279px):** Sidebar collapses to icon rail. Two-column grids drop to one.  
* **Mobile (\< 768px):** Sidebar becomes a bottom navigation tab bar (5 icons max). All tables become card stacks. Wizard steps go full-screen per step.

---

## **7\. Key UX Rules**

1. **Never show a blank state without a CTA.** Empty dashboards should guide users toward their first action.  
2. **Role context is always visible.** A small role badge in the nav (`Freelancer` or `Client`) prevents confusion. Users can switch roles if enabled.  
3. **Financial numbers are always formatted clearly** — currency symbol, proper commas, and green coloring for positive values.  
4. **Destructive actions require confirmation.** Declining a proposal, closing a contract, or banning a user all require a modal confirmation step.  
5. **Loading states use skeleton screens**, not spinners — maintains layout stability and feels faster.

