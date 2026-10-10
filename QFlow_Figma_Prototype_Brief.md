# Q-Flow — Figma Prototype Brief

This document covers every screen, component, and interaction needed to produce a high-fidelity clickable prototype in Figma. It is based on the architecture decisions already locked for the project. Use this as the single source of truth when laying out screens.

---

## Brand & Design Tokens

### Colors

| Token | Hex | Usage |
|-------|-----|-------|
| Primary Navy | `#060164` | Top bar backgrounds, table headers, primary text, section icons |
| Deep Orange | `#ed4f07` | Primary action buttons, accents, active indicators, section underlines |
| Light Orange | `#ff7a3d` | Hover states on orange buttons, P1 priority badges |
| Background White | `#ffffff` | Page backgrounds, card surfaces |
| Surface Light | `#f8f8ff` | Card backgrounds, subtle row hovers, tech badge backgrounds |
| Border Light | `#f0f0f0` | Section dividers, card borders |
| Border Medium | `#e0e0e0` | Table row dividers, input borders |
| Text Primary | `#1a1a1a` | Headings, important labels |
| Text Secondary | `#444444` | Body copy, descriptions |
| Text Muted | `#888888` | Timestamps, secondary info, footers |
| Status Waiting | `#f59e0b` | Yellow pill — ticket is in queue |
| Status Called | `#3b82f6` | Blue pill — ticket has been called |
| Status In Service | `#22c55e` | Green pill — being served |
| Status Skipped | `#9ca3af` | Grey pill — no-show |
| Status Served | `#1e293b` | Dark pill — completed |
| Success Green | `#2e7d32` | "Correct" examples, Existing component badges |
| Info Blue | `#1565c0` | New component badges |
| Purple | `#7b1fa2` | Shared component badges |
| Error Red | `#c62828` | "Avoid" examples, danger actions |

### Typography

| Element | Font | Size | Weight | Line Height |
|---------|------|------|--------|-------------|
| Cover Title | System | 52px | 800 | 1.1 |
| Cover Subtitle | System | 20px | 400 | 1.4 |
| Section Title (h2) | System | 21px | 700 | 1.3 |
| Subsection (h3) | System | 14px | 700 | 1.4 |
| Body Text | System | 12.5px | 400 | 1.6 |
| Table Header | System | 9.5px | 600 | 1.2 |
| Table Body | System | 11px | 400 | 1.5 |
| Badge Text | System | 9.5px | 600 | 1.0 |
| Code Inline | Mono | 10.5px | 400 | 1.4 |
| Section Label | System | 10px | 700 | 1.2 |

### Spacing

| Element | Value |
|---------|-------|
| Page padding (mobile) | 20px all sides |
| Page padding (desktop) | 48px top/bottom, 56px left/right |
| Card padding | 16px |
| Table cell padding | 9px 12px |
| Gap between cards | 10px |
| Gap between sections | 24px |
| Section bottom margin | 14px |

### Border Radius

| Element | Radius |
|---------|--------|
| Cards | 8px |
| Buttons | 6px |
| Badges / Pills | 4px |
| Input fields | 6px |
| Cover icon | 16px |
| Page header icon | 8px |

---

## What Q-Flow Is

Q-Flow is a queue management system for retail branches. A customer scans a QR code at the store, joins a single store-wide FIFO queue, and receives live updates on their position and estimated wait time. Staff at counters pull from that same queue — calling the next customer, marking service complete, skipping no-shows, and reassigning tickets across counters. There is one queue per branch, not per service.

---

## Target Users

1. **Customers** — scan a QR, join the queue, track their position on a mobile screen, get notified when their turn is close, and can leave the queue if they change their mind.
2. **Staff (Counter Agents)** — sign in, select their counter for the shift, call the next customer, manage the queue in real time, view ticket details, and log out at shift end.
3. **Admin (Branch Manager)** — manage counters (create, toggle active/inactive), manage staff accounts, view and print the branch QR code, and review enterprise-wide ticket history.

---

## Screen Sizes

| Surface | Frame Size | Notes |
|---------|-----------|-------|
| Customer | 390 × 844 (iPhone 14) | Mobile-first, single column |
| Staff | 1440 × 900 | Desktop, sidebar optional, full-width content |
| Admin | 1440 × 900 | Desktop, same layout as staff |

---

## Screen Breakdown

### A. Customer Screens

#### A1. Join Queue (`/join/:code`)

**Frame:** Mobile — 390 × 844

**Layout (top to bottom):**
1. **Status bar area** — 44px safe area at top.
2. **App Logo** — centered, 40×40px, 20px below the status bar.
3. **Page Title** — "Join Queue", centered, 21px, weight 700, color `#060164`, 24px below logo.
4. **Branch Name** — centered, 13px, color `#888`, 6px below title. Example: "AmaliTech Branch — East Legon".
5. **Form Card** — white background, 16px padding, 8px border radius, 1px solid `#e0e0e0` border, 24px below branch name, full width minus 40px (20px margin each side).
   - **Full Name Input** — label "Full Name" (11px, weight 600, color `#444`), text input below (height 44px, border 1px solid `#e0e0e0`, border radius 6px, placeholder "Enter your full name", font size 13px).
   - **12px spacing** between inputs.
   - **Phone Number Input** — label "Phone Number", same styling, placeholder "e.g. 024 123 4567", includes a small country code prefix (+233) inside the input on the left.
   - **16px spacing** below phone input.
   - **Notification Channel** — label "How should we notify you?" (11px, weight 600). Three option cards in a row, each 33% width minus gap:
     - **WhatsApp** — icon + label, border 2px solid `#ed4f07` when selected (default), `#e0e0e0` otherwise. Background white.
     - **SMS** — same styling, unselected by default.
     - **None** — same styling, unselected by default.
   - **20px spacing** below channel selector.
   - **Join Queue Button** — full width, height 48px, background `#ed4f07`, text "Join Queue" (15px, weight 600, color white, centered), border radius 6px.
6. **Footer text** — centered, 11px, color `#aaa`, 24px below button: "By joining, you agree to receive queue updates."

**States to design:**
- Default (empty form)
- Filled form (all fields populated)
- Submitting (button shows a small spinner, disabled state — opacity 0.7)

---

#### A2. Ticket Confirmation (`/ticket/:ticketId` — first visit)

**Frame:** Mobile — 390 × 844

**Layout (top to bottom):**
1. **Status bar area** — 44px.
2. **App Logo** — centered, 40×40px.
3. **Success Icon** — a green checkmark circle, 56×56px, centered, 16px below logo.
4. **Title** — "You're in the queue!", centered, 18px, weight 700, color `#060164`.
5. **Ticket Card** — white card, 16px padding, 8px radius, full width minus 40px, centered, 20px below title.
   - **Ticket Number** — "Q-047" or similar, 32px, weight 800, color `#060164`, centered.
   - **Join Time** — "Joined at 10:32 AM", 12px, color `#888`, centered, 4px below ticket number.
   - **Divider** — 1px line, color `#f0f0f0`, 12px margin top and bottom.
   - **Status Message** — "You're in the queue — we'll notify you when it's almost your turn.", 13px, color `#444`, centered.
6. **Stat Cards Row** — two cards side by side, full width minus 40px, centered, 20px below ticket card.
   - **Position Card** — white background, 1px solid `#e0e0e0`, 12px padding, 8px radius. Label "Position" at top (11px, weight 600, color `#888`). Large number below (28px, weight 800, color `#060164`). Example: "7".
   - **Estimated Wait Card** — same styling. Label "Est. Wait". Value "25 min" (28px, weight 800, color `#ed4f07`).
   - Gap between cards: 10px.
7. **Leave Queue Button** — full width minus 40px, centered, 24px below stat cards, height 44px, background white, border 1px solid `#e0e0e0`, text "Leave Queue" (13px, weight 600, color `#c62828`), border radius 6px.

**States to design:**
- Waiting (position visible, wait visible)
- Position 1 / "Almost up" (status message changes to "You're next! Please head to the counter.")
- Called (status message: "It's your turn! Please proceed to the counter now." — hide stat cards, hide Leave Queue button)

---

#### A3. Confirmation Dialog (Modal — overlays A2/A3)

**Frame:** Same mobile frame, semi-transparent black overlay (`rgba(0,0,0,0.5)`), dialog centered.

**Dialog:**
- Width: 320px, auto height.
- White background, 16px padding, 12px border radius.
- Title: "Leave Queue?" (16px, weight 700, color `#060164`, centered).
- Body: "You'll lose your spot in the queue. You can rejoin by scanning the QR again." (13px, color `#444`, centered, 8px below title).
- Two buttons, full width, stacked:
  - "Stay in Queue" — full width, height 44px, background `#060164`, text white, 13px weight 600, radius 6px.
  - "Yes, Leave" — full width, height 44px, background white, border 1px solid `#e0e0e0`, text `#c62828`, 13px weight 600, radius 6px.
- 10px gap between buttons.

---

### B. Staff Screens

#### B1. Staff Login (`/staff/login`)

**Frame:** Desktop — 1440 × 900

**Layout:**
- Background: `#f8f8ff` (full frame).
- Center: Login card, width 400px, auto height, white background, 32px padding, 12px border radius, box-shadow `0 4px 24px rgba(0,0,0,0.08)`.
- Inside card (top to bottom):
  1. **App Logo** — centered, 48×48px, 0px margin top.
  2. **Title** — "Q-Flow", centered, 24px, weight 800, color `#060164`, 12px below logo.
  3. **Subtitle** — "Staff Sign In", centered, 13px, color `#888`, 4px below title.
  4. **24px spacing**.
  5. **Employee ID Input** — label "Employee ID" (11px, weight 600, color `#444`), input (height 44px, full width, border 1px solid `#e0e0e0`, radius 6px, placeholder "e.g. EMP-0042").
  6. **12px spacing**.
  7. **Password Input** — label "Password", same input styling, placeholder "Enter your password", right side has an eye icon to toggle visibility.
  8. **20px spacing**.
  9. **Sign In Button** — full width, height 48px, background `#ed4f07`, text "Sign In" (15px, weight 600, white), radius 6px.

**States to design:**
- Default (empty form)
- Filled form
- Error state: red text below the form — "Invalid employee ID or password" (12px, color `#c62828`)

---

#### B2. Counter Selection (`/staff/counter-select`)

**Frame:** Desktop — 1440 × 900

**Layout:**
- Background: `#f8f8ff`.
- Top bar: full width, height 56px, background `#060164`. Left: "Q-Flow" logo text (16px, weight 700, white). Right: staff name and role (12px, white).
- Center content area (below top bar, centered):
  1. **Title** — "Select Your Counter" (21px, weight 700, color `#060164`), centered, 40px below top bar.
  2. **Subtitle** — "Choose the register you'll be working at today" (13px, color `#888`), centered, 8px below title.
  3. **Counter Cards** — grid, 2 columns, gap 12px, max-width 480px, centered, 24px below subtitle.
     - Each card: white background, 16px padding, 8px radius, 1px solid `#e0e0e0`. On hover: border color changes to `#ed4f07`.
     - Inside: counter name (15px, weight 600, color `#060164`), status indicator dot (green for active, grey for inactive), and counter number label (11px, color `#888`).
     - Example cards: "Counter 1" (active), "Counter 2" (active), "Counter 3" (inactive — greyed out).

---

#### B3. Operations Overview (`/staff`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Top Bar** — full width, height 56px, background `#060164`.
   - Left side (24px padding): Q-Flow logo text (16px, weight 700, white) | Branch name divider line (1px, rgba white 0.3) | Branch name "AmaliTech — East Legon" (13px, white, weight 400).
   - Right side (24px padding): Staff name "Kwame Asante" (13px, white) | Role badge "Counter Staff" (10px, weight 600, background rgba white 0.15, radius 4px, padding 2px 8px) | Avatar circle (32×32px, background `#ed4f07`, initials "KA" in white 12px) | Sign-out icon (20×20px, white, on far right).
2. **Content Area** — padding: 32px top, 24px left/right (inside the 1440 frame).
   - **Stats Row** — three cards in a row, equal width, gap 12px.
     - Each card: white background, 16px padding, 8px radius, 1px solid `#e0e0e0`.
     - Label at top (11px, weight 600, color `#888`, uppercase, letter-spacing 1px).
     - Large number below (32px, weight 800).
       - "WAITING" → number color `#f59e0b` (amber). Example: "12".
       - "SERVING" → number color `#22c55e` (green). Example: "3".
       - "SERVED TODAY" → number color `#060164` (navy). Example: "47".
     - Subtle background tint matching the status color at 5% opacity (optional).
   - **16px spacing** below stats.
   - **Call Next Button** — full width of content area, height 52px, background `#ed4f07`, text "Call Next Customer" (15px, weight 700, white, centered), radius 6px. On hover: background `#ff7a3d`.
   - **20px spacing** below button.
   - **Section Title** — "Current Queue" (14px, weight 700, color `#060164`), inline with "View Full Queue →" link (12px, color `#ed4f07`, weight 600) on the right.
   - **8px spacing**.
   - **Queue Table** (compact, showing first 5 rows):
     - Header row: background `#060164`, text white, 9.5px, weight 600, uppercase. Columns: Ticket # | Customer | Position | Status | Time.
     - Data rows: white background, 1px bottom border `#f0f0f0`. Font 11px, color `#444`.
     - Status column: pill badges — small rounded rectangles (padding 2px 8px, radius 4px, font 9.5px, weight 600):
       - Waiting: background `#fef3c7`, text `#92400e`
       - Called: background `#dbeafe`, text `#1e40af`
       - In Service: background `#dcfce7`, text `#166534`
     - Example rows:
       - Q-047 | Ama Mensah | 7 | Waiting | 10:32 AM
       - Q-046 | Kofi Darko | 6 | Called | 10:28 AM
       - Q-045 | Abena Osei | 5 | In Service | 10:25 AM

---

#### B4. Queue List (`/staff/queue`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Top Bar** — identical to B3.
2. **Content Area** — 32px top, 24px left/right.
   - **Page Title** — "Queue" (21px, weight 700, color `#060164`), 0px below top bar content padding.
   - **16px spacing**.
   - **Search Bar** — full width, height 44px, background white, border 1px solid `#e0e0e0`, radius 6px. Left padding with search icon (20×20px, color `#888`). Placeholder: "Search by name or ticket number..." (13px, color `#aaa`).
   - **12px spacing** below search.
   - **Filter Row** (optional) — pill buttons for status filter: "All" (selected, background `#060164`, text white), "Waiting" (unselected, background white, border `#e0e0e0`), "Called", "In Service", "Skipped", "Served". Each pill: padding 6px 14px, radius 20px, font 11px, weight 600.
   - **12px spacing**.
   - **Queue Table** (full width, showing 8 rows):
     - Header: same styling as B3 but full columns: Ticket # (15% width) | Customer Name (25%) | Position (15%) | Status (20%) | Time Joined (15%) | Actions (10%).
     - Rows: alternating white and `#fafafa` backgrounds (or all white with bottom borders). Row height ~44px.
     - Actions column: eye icon button (view detail), 32×32px, radius 6px, background transparent, on hover background `#f0f0f0`.
     - Example data rows:
       - Q-047 | Ama Mensah | 7 | [Waiting pill] | 10:32 AM | [eye]
       - Q-046 | Kofi Darko | 6 | [Called pill] | 10:28 AM | [eye]
       - Q-045 | Abena Osei | 5 | [In Service pill] | 10:25 AM | [eye]
       - Q-044 | Yaw Boateng | 4 | [Skipped pill] | 10:20 AM | [eye]
       - Q-043 | Efua Mensah | 3 | [Served pill] | 10:15 AM | [eye]
       - Q-042 | Kojo Appiah | 2 | [Served pill] | 10:10 AM | [eye]
       - Q-041 | Adwoa Amoah | 1 | [Served pill] | 10:05 AM | [eye]
       - Q-040 | Nana Agyei | — | [Served pill] | 10:00 AM | [eye]
   - **Pagination** — below table, right-aligned: "← Previous" | "1 2 3 ... 6" | "Next →" (12px, color `#060164`, active page bold with `#ed4f07` underline).

---

#### B5. Customer Detail (`/staff/queue/:ticketId`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Top Bar** — identical to B3.
2. **Content Area** — 32px top, 24px left/right.
   - **Back Link** — "← Back to Queue" (13px, color `#ed4f07`, weight 600), 0px top.
   - **12px spacing**.
   - **Ticket Header Row** — two items aligned:
     - Left: Ticket number "Q-047" (24px, weight 800, color `#060164`).
     - Right: Status pill (e.g., [Waiting] — padding 4px 12px, radius 4px, font 11px, weight 600).
   - **16px spacing**.
   - **Customer Info Card** — white card, 20px padding, 8px radius, 1px solid `#e0e0e0`, full width.
     - Title inside card: "Customer Information" (13px, weight 700, color `#060164`), 16px below card top.
     - Below title, grid of 2 columns:
       - **Name:** label "Full Name" (10px, weight 600, uppercase, color `#888`), value "Ama Mensah" (13px, weight 500, color `#1a1a1a`).
       - **Phone:** label "Phone", value "+233 24 123 4567".
       - **Channel:** label "Notification", value "WhatsApp" with a small green WhatsApp icon.
       - **Joined:** label "Time Joined", value "10:32 AM".
   - **16px spacing**.
   - **Control Panel Card** — white card, 20px padding, 8px radius, 1px solid `#e0e0e0`. Content changes by state:
     - **If Waiting:** Title "Queue Actions" (13px, weight 700). One primary button below: "Call Next" (full width, height 48px, background `#ed4f07`, text white, 14px weight 600).
     - **If Called:** Two buttons side by side. Left: "Start Service" (primary, `#ed4f07`, flex 1). Right: "Mark No-Show" (danger, white background, border 1px solid `#c62828`, text `#c62828`, flex 1).
     - **If In Service:** One primary button: "Complete Service" (`#ed4f07`, full width).
     - **If Skipped:** One primary button: "Reopen Ticket" (`#ed4f07`, full width).
   - **16px spacing**.
   - **Notes Section** — white card, 20px padding, 8px radius.
     - Title: "Notes & Alerts" (13px, weight 700, color `#060164`).
     - **Add Note Input** — full width, height 40px, border 1px solid `#e0e0e0`, radius 6px, placeholder "Add a note...", right side has a small "Add" button (background `#060164`, text white, height 32px, radius 4px, padding 0 12px).
     - **12px spacing**.
     - **Note List** — 1-2 example notes:
       - Each note: left border 3px solid `#ed4f07`, padding 10px 12px, background `#fafafa`, radius 0 6px 6px 0.
       - Note text: "Customer asked to be called urgently" (12px, color `#444`).
       - Timestamp: "10:35 AM — Kwame Asante" (10px, color `#888`).

---

#### B6. Staff History (`/staff/history`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Top Bar** — identical to B3.
2. **Content Area**:
   - **Page Title** — "History" (21px, weight 700, color `#060164`).
   - **16px spacing**.
   - **Filter Bar** — row, gap 12px:
     - Date picker input (width 200px, height 40px, border 1px solid `#e0e0e0`, radius 6px, placeholder "Select date", calendar icon on left).
     - Export button (optional — "Export CSV", white background, border 1px solid `#e0e0e0`, radius 6px, text 12px, icon on left).
   - **12px spacing**.
   - **History Table** — full width, columns: Ticket # | Customer | Status | Served At | Counter.
     - Same table styling as queue table.
     - Status column uses the same pill badges.
     - Read-only — no action buttons.
     - Example rows:
       - Q-039 | Akua Sarpong | Served | 9:55 AM | Counter 1
       - Q-038 | Kwesi Mensah | Served | 9:48 AM | Counter 2
       - Q-037 | Esi Ampofo | Skipped | 9:40 AM | Counter 1
   - **Pagination** — same as B4.

---

### C. Admin Screens

#### C1. Admin Login

Same layout as B1. The system determines the role from the login response and routes admin users to `/admin/counters`. Design one login screen; it works for both roles.

---

#### C2. Admin Top Bar

Present on all admin pages. Same height (56px) and background (`#060164`) as staff top bar, but the right side navigation is replaced with a horizontal tab bar:

- **Tabs:** Counters | Staff | QR Code | History
- Tab styling: text 12px, weight 500, white color, padding 0 16px. Active tab has a 2px bottom border in `#ed4f07`. Inactive tabs have no bottom border.
- Right side: avatar + staff name + role badge "Admin" (same styling as staff).

---

#### C3. Counter Management (`/admin/counters`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Admin Top Bar** — with "Counters" tab active.
2. **Content Area**:
   - **Page Title** — "Counter Management" (21px, weight 700).
   - **16px spacing**.
   - **Header Row** — "Manage your branch counters" subtitle (13px, color `#888`) on the left, "Add Counter" button on the right (background `#ed4f07`, text white, height 36px, radius 6px, padding 0 16px, font 12px weight 600, plus icon).
   - **12px spacing**.
   - **Counter Table** — columns: Counter Name (30%) | Status (20%) | Staff Assigned (25%) | Actions (25%).
     - Status column: green dot + "Active" or grey dot + "Inactive" (11px).
     - Actions column: "Edit" text button (color `#ed4f07`, 12px, weight 600) | Toggle switch (44×24px, green when on, grey when off).
     - Example rows:
       - Counter 1 | ● Active | Kwame Asante, Ama Owusu | Edit | [toggle on]
       - Counter 2 | ● Active | Kofi Darko | Edit | [toggle on]
       - Counter 3 | ○ Inactive | — | Edit | [toggle off]

---

#### C4. Staff Directory (`/admin/staff`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Admin Top Bar** — "Staff" tab active.
2. **Content Area**:
   - **Page Title** — "Staff Directory".
   - **Header Row** — subtitle "All staff accounts for this branch" | "Create Account" button (same styling as Add Counter).
   - **Staff Table** — columns: Employee ID (15%) | Name (25%) | Role (20%) | Assigned Counter (25%) | Actions (15%).
     - Role column: badge — "Counter Staff" (background `#e3f2fd`, text `#1565c0`) or "Admin" (background `#f3e5f5`, text `#7b1fa2`).
     - Actions: "Edit" text button.
     - Example rows:
       - EMP-0042 | Kwame Asante | [Counter Staff] | Counter 1 | Edit
       - EMP-0043 | Ama Owusu | [Counter Staff] | Counter 1 | Edit
       - EMP-0001 | Kofi Darko | [Admin] | — | Edit

---

#### C5. Create Staff Form (Modal — overlays C4)

**Dialog:** width 480px, white background, 24px padding, 12px radius.

- Title: "Create Staff Account" (18px, weight 700, color `#060164`).
- Fields (vertical stack, 14px gap):
  - Employee ID — label + input (same input styling).
  - Full Name — label + input.
  - Password — label + input (with visibility toggle).
  - Role — label + dropdown select (options: "Counter Staff", "Admin").
  - Assigned Counter — label + dropdown (options: "Counter 1", "Counter 2", "Counter 3", "None").
- **20px spacing**.
- Two buttons, right-aligned, gap 10px:
  - "Cancel" — white background, border `#e0e0e0`, text `#444`, height 40px, radius 6px.
  - "Create Account" — background `#ed4f07`, text white, height 40px, radius 6px.

---

#### C6. QR Code (`/admin/qr-code`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Admin Top Bar** — "QR Code" tab active.
2. **Content Area** — centered column, max-width 400px.
   - **Page Title** — "Branch QR Code", centered.
   - **16px spacing**.
   - **QR Card** — white background, 24px padding, 12px radius, centered, box-shadow `0 2px 12px rgba(0,0,0,0.06)`.
     - QR Code Image — 280×280px placeholder (a black and white QR pattern), centered.
     - **16px spacing**.
     - Branch Name — "AmaliTech — East Legon", centered, 16px, weight 600, color `#060164`.
     - Branch Address — "14 Independence Ave, Accra", centered, 12px, color `#888`, 4px below name.
   - **20px spacing**.
   - **Print Button** — centered, width 200px, height 44px, background `#060164`, text "Print QR Code" (13px, weight 600, white), radius 6px, printer icon on left.

---

#### C7. Admin History (`/admin/history`)

**Frame:** Desktop — 1440 × 900

**Layout:**
1. **Admin Top Bar** — "History" tab active.
2. **Content Area**:
   - **Page Title** — "Ticket History".
   - **Filter Bar** — row, gap 12px:
     - Status dropdown (width 160px, height 40px, options: All, Waiting, Called, In Service, Served, Skipped).
     - Date picker (width 200px).
     - Date-to picker (width 200px).
     - Search input (flex 1, height 40px).
   - **12px spacing**.
   - **History Table** — columns: Ticket # | Customer | Status | Counter | Date | Time.
     - Same styling as staff history but with extra Counter column.
     - Pagination at bottom.

---

## Components Reference

Design each component once as a Figma component (with variants where noted). These are reused across screens.

### Customer Components

| Component | Variants | Description |
|-----------|----------|-------------|
| `JoinDetailsForm` | Default, Filled, Submitting | Full form card with name, phone, channel selector |
| `ContactChannelInput` | WhatsApp (selected), SMS (selected), None (selected) | Three-option toggle row |
| `TicketHeader` | Waiting, Almost Up, Called | Ticket number + time + status message |
| `TicketStatCard` | Position, Wait Time | Label + large number, used in pairs |
| `LeaveQueueButton` | Default, Hover | Red text on white background |
| `ConfirmDialog` | Default | Modal with title, body, two action buttons |

### Staff Components

| Component | Variants | Description |
|-----------|----------|-------------|
| `StaffTopbar` | Default | Branch name, staff info, avatar, sign-out |
| `OverviewStatCard` | Waiting (amber), Serving (green), Served Today (navy) | Label + large number |
| `CallNextButton` | Default, Hover, Disabled | Full-width primary orange button |
| `QueueTable` | Default, Empty | Full table with header and rows |
| `QueueTableRow` | Default, Hover | Single row with all columns |
| `QueueStatusPill` | Waiting, Called, In Service, Skipped, Served | Color-coded badge |
| `QueueSearchBar` | Default, Focused | Input with search icon |
| `TicketDetailHeader` | All statuses | Ticket number + status pill |
| `QueueControlPanel` | Waiting, Called, In Service, Skipped | State-driven button layout |
| `CustomerInfoCard` | Default | Name, phone, channel, join time |
| `NoteItem` | Default | Orange left border, text, timestamp |
| `HistoryFilterBar` | Default | Date picker input |
| `HistoryTable` | Default | Read-only served-ticket log |
| `CounterSelectCard` | Active, Inactive | Counter name + status dot |
| `StaffLoginForm` | Default, Error | Centered card with inputs |

### Admin Components

| Component | Variants | Description |
|-----------|----------|-------------|
| `AdminTopbar` | Counters active, Staff active, QR active, History active | Tabbed navigation bar |
| `CounterListRow` | Active, Inactive | Counter name, toggle, staff count |
| `CounterForm` | Create, Edit | Modal form for counter management |
| `StaffDirectoryRow` | Counter Staff, Admin | Employee info with role badge |
| `CreateStaffForm` | Default | Modal form for account creation |
| `QrCodeCard` | Default | QR image + branch info + print button |
| `AdminHistoryTable` | Default | Extended history table with filters |

### Shared Components

| Component | Variants | Description |
|-----------|----------|-------------|
| `AppLogo` | Default, Large | Brand mark icon |
| `ToastNotification` | Success, Error, Info | Slide-in notification bar |
| `ConfirmDialog` | Default | Reusable yes/no modal |
| `AuthErrorMessage` | Default | Inline red error text |

---

## Interaction Flows to Prototype

### Flow 1: Customer Join
1. Open `/join/abc123` → see join form (A1).
2. Fill name and phone, select WhatsApp → tap "Join Queue".
3. Transition to ticket confirmation (A2) — show position "7", wait "25 min".
4. Tap "Leave Queue" → confirmation dialog appears.
5. Tap "Stay in Queue" → dialog closes.

### Flow 2: Staff Full Session
1. Open `/staff/login` → login form (B1).
2. Enter credentials → sign in → counter selection (B2).
3. Select "Counter 1" → operations overview (B3).
4. See stats (Waiting: 12, Serving: 3, Served Today: 47).
5. Tap "Call Next Customer" → button briefly shows loading → toast "Customer Q-047 called".
6. Tap "View Full Queue →" → queue list (B4).
7. Search "Ama" → table filters to show matching rows.
8. Tap row for Q-047 → customer detail (B5).
9. See customer info, status is now "Called".
10. Tap "Start Service" → status changes to "In Service".
11. Tap "Complete Service" → toast "Service completed" → back to overview.

### Flow 3: Admin Counter Management
1. Login as admin → redirects to `/admin/counters` (C3).
2. See counter list with active/inactive toggles.
3. Tap toggle on Counter 3 → switches to active.
4. Tap "Add Counter" → counter form modal (C4).
5. Fill name, toggle active → save → new counter appears in list.
6. Navigate to QR Code tab → see QR (C6) → tap "Print QR Code".

### Flow 4: Admin Staff Management
1. Navigate to Staff tab (C4).
2. See staff directory table.
3. Tap "Create Account" → modal form (C4 modal).
4. Fill fields, select role "Counter Staff", assign Counter 2 → "Create Account".
5. New row appears in the table.

---

## What's NOT in This Prototype

These are design gaps flagged for a later phase. Do not include them in this prototype pass:
- Loading skeletons or fetch-in-progress states (except the button submitting state in A1)
- Error states (network failure, ticket not found, etc.) — except login error in B1
- Empty state variants beyond a simple message
- Queue-closed or ticket-expired screens
- Staff logout confirmation
- History date range beyond "Today"
- Responsive breakpoints (mobile admin/staff)
- Toast notification auto-dismiss animation
