Here is your complete, production-quality v0.app meta prompt. Paste this directly into v0 and it will build the full app for you.

text
Build a professional web application called "EngageIQ" — an AI-powered evidence reusability assistant for CPA firms managing recurring client engagements.

---

## APPLICATION PURPOSE

CPAs managing recurring clients (audit, tax, advisory) waste significant time re-requesting evidence that already exists from prior engagements. This app helps teams surface reusable evidence from prior-year files before opening a new client engagement, reducing duplicate document requests and speeding up engagement prep.

---

## LAYOUT: APP SHELL

Use a two-panel layout with a persistent left sidebar and a main content area.

### Left Sidebar (240px wide, fixed)
- App logo at top: "EngageIQ" with a small document + checkmark icon
- Primary nav sections:
  - Dashboard (home/overview)
  - Clients (list of all clients)
  - Engagements (all active and past engagements)
  - Settings
- Below nav: a prominent "New Engagement" button (teal, full-width)
- Client list below the button: show 5-8 mock clients each with:
  - Client name
  - Client ID (e.g. CLT-0042)
  - A small badge showing engagement type (Audit / Tax / Advisory)
  - Clicking a client expands to show their engagements listed underneath with fiscal year labels
- Bottom of sidebar: user avatar, name, and firm name

### Main Content Area
- Sticky top header bar with: page title (left), light/dark mode toggle (right), notification bell, user avatar
- Content renders based on sidebar selection

---

## CORE USER FLOWS

### Flow 1: Dashboard (default view)
Show a clean overview with:
- Summary cards: Total Active Clients, Open Engagements, Evidence Reused This Quarter, Time Saved (hrs)
- Recent Engagements table: client name, engagement type, fiscal year, status badge (In Progress / Evidence Review / Complete), last updated
- Quick action: "Start New Engagement" button

### Flow 2: New Engagement (triggered from sidebar button or dashboard)
Open a right-side slide-over panel (not a full page navigation) with a clean 4-field form:

**Form fields:**
1. Client Name — searchable dropdown (show existing clients or type new name)
2. Client ID — auto-fills if existing client selected, manual entry if new
3. Fiscal Year — dropdown: FY2025, FY2024, FY2023, or custom text input
4. Engagement Type — segmented control or radio group with three options:
   - Audit
   - Tax
   - Advisory
5. Client Status — toggle: "Existing Client" / "New Client"

**Form behavior:**
- If "New Client" is selected: disable the reusability check, show a note "No prior engagement history. A full evidence request will be generated."
- If "Existing Client" is selected: show a subtle "Prior engagements found" indicator once client name is selected
- Primary CTA: "Check Evidence Reusability" button (teal, disabled until all fields are filled)
- Secondary: "Cancel" ghost button

### Flow 3: Evidence Reusability Results (after form submission)
After the user submits the form, simulate a brief loading state (1.5 seconds with a skeleton loader and "Checking prior engagement records..." message), then display results in the main content area.

**Results layout — three-column evidence brief:**

**Column 1: Likely Reusable (green)**
Header: checkmark icon + "Likely Reusable"
Subtext: "Available from prior engagements. Confirm no material changes."
List of evidence items, each as a card showing:
- Evidence name (e.g. "Organizational Chart — FY2024")
- Source engagement label
- A "Mark for Reuse" checkbox (pre-checked)

**Column 2: Validate Before Reuse (amber)**
Header: warning icon + "Validate Before Reuse"
Subtext: "Exists but requires confirmation before relying on it."
Same card format, with:
- A "Needs Confirmation" badge
- A short reason line (e.g. "System changes may affect relevance")
- "Mark for Reuse" checkbox (unchecked by default)

**Column 3: Collect Fresh (blue)**
Header: refresh icon + "Collect Fresh"
Subtext: "Period-specific or must be refreshed this cycle."
Same card format, with:
- A "Fresh Required" badge
- No checkbox — these are always collected fresh

**Below the three columns:**
- A summary line: "X items marked for reuse · Y items need validation · Z items require fresh collection"
- Two action buttons:
  - "Generate Evidence Request" (primary teal) — produces a downloadable brief of only the "Collect Fresh" items
  - "Save & Open Engagement" (secondary) — saves this configuration and opens the engagement record

### Flow 4: Engagement Detail View (accessible from sidebar or recent engagements table)
Show a full engagement record for a selected client:
- Header: client name, client ID, engagement type badge, fiscal year, status badge
- Tabs: Overview / Evidence / Documents / Notes
- Evidence tab shows the same three-column reusability brief from Flow 3
- Documents tab shows a simple file list (mock data)
- Notes tab shows a text area for engagement notes

---

## MOCK DATA

Populate with realistic CPA firm mock data:

**Clients:**
- Meridian Healthcare Group (CLT-0041) — Audit
- Stonegate Capital Partners (CLT-0042) — Tax + Advisory
- Riverdale Manufacturing (CLT-0043) — Audit
- Crestwood Hospitality LLC (CLT-0044) — Tax
- Apex Logistics Inc. (CLT-0045) — Advisory

**Evidence items (use these across the three columns for Meridian Healthcare — FY2025 Audit):**

Likely Reusable:
- Organizational Chart (FY2024)
- Entity Governing Documents
- IT General Controls Walkthrough
- Related Party Listing
- Prior Year Financial Statements

Validate Before Reuse:
- Internal Control Narratives ("Confirm no process changes since FY2024")
- System Access Listings ("IT system upgrade in Q2 may affect relevance")
- Risk Assessment Documentation ("Review for updated risk factors")

Collect Fresh:
- Bank Statements — FY2025
- Management Representation Letter
- Period-End Account Balances
- Accounts Receivable Confirmations
- Engagement Letter — FY2025

---

## DESIGN DIRECTION

Professional, trustworthy, and precise. This is a tool for senior CPA professionals — it must feel like enterprise software built with care, not a startup demo.

**Palette:**
- Background: warm off-white (#f7f6f2 light / #171614 dark)
- Surface: layered neutral cards
- Primary accent: deep teal (#01696f) for buttons, active states, badges
- Success / Reusable: muted green
- Warning / Validate: muted amber
- Info / Fresh: muted blue
- No purple gradients, no glowing effects, no decorative blobs

**Typography:**
- Load Satoshi from Fontshare for body (api.fontshare.com)
- Load Instrument Serif from Google Fonts for display headings
- Body: 16px, weight 400. Headings: bold Satoshi. Page titles: Instrument Serif.

**Components:**
- Cards: subtle shadow, neutral border (alpha-blended), radius-md
- Badges: pill shape, muted background tones per category
- Buttons: solid teal primary, ghost secondary, no gradients
- Sidebar active state: teal left accent bar + teal text + lightly tinted background
- Form inputs: clean, generous padding, visible focus ring in teal
- Skeleton loaders: shimmer animation during loading states

**Both light and dark mode required.** Include a toggle in the top right header. Default to system preference.

---

## INTERACTION DETAILS

- Sidebar client items: clicking expands inline to show that client's engagements. Clicking an engagement navigates to the detail view.
- "New Engagement" slide-over: smooth slide-in from the right, overlay dims the main content, click outside or Cancel to dismiss.
- Evidence results: animate in with a subtle fade and slight upward translate per column, staggered 100ms each.
- "Mark for Reuse" checkboxes: update the summary count live as checked/unchecked.
- "Generate Evidence Request": show a brief success state ("Evidence request ready") with a simulated download trigger.
- All state is in-memory. No backend required. Simulate loading with setTimeout.

---

## TECH STACK

- React with TypeScript
- Tailwind CSS v4
- Lucide React for icons
- Framer Motion for slide-over and result animations
- No external backend — all state managed in React with useState/useReducer
- Fonts: Fontshare (Satoshi) + Google Fonts (Instrument Serif)

---

## QUALITY BAR

- Fully responsive: works at 375px mobile (sidebar collapses to hamburger) and 1280px+ desktop
- WCAG AA contrast on all text
- Keyboard navigable: all interactive elements reachable by Tab
- Every state designed: loading skeleton, empty states with helpful messages, error states with retry
- No placeholder text left in final output
- Light and dark mode both polished and verified
