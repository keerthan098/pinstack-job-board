# Pinstack — Job Board for Early-Career Software Engineers

Pinstack is a self-contained, single-page job board built for early-career software engineers in India's tech market — spanning backend, frontend, full-stack, data, QA, and DevOps roles. It runs entirely client-side (HTML, CSS, and vanilla JavaScript, no backend or build step required) and is deployed as a static site.

**Live demo:** https://pinstack-job-board.vercel.app
**Repository:** https://github.com/keerthan098/pinstack-job-board

---

## Design concept

The interface is built around a literal "board" metaphor: job listings are rendered as index cards pinned to a corkboard, with a subtle paper-grain background, slightly rotated cards, and a hand-set typewriter display font (Courier Prime) paired with a clean UI sans-serif (IBM Plex Sans) and a monospace face for data/labels (IBM Plex Mono).

The signature interaction is the **pin color**, which is not purely decorative — it encodes real information about each listing:

| Pin color |           Meaning                    |
|-----------|------------------------------------- |
| 🔴 Red   | Company is hiring urgently            |
| 🟠 Amber | Posted within the last 3 days ("new") |
| ⚪ Gray  | Standard listing                      |

Cards sit slightly rotated at rest and straighten out on hover/keyboard focus, giving a tactile "picking it up off the board" feel without relying on heavy imagery or external assets.

---

## Features

### 1. Search
A single search bar in the hero section filters listings in real time (on input, no page reload) by matching against job title, company name, and skill tags. Search is case-insensitive and substring-based, so partial terms like "spring" or "kafka" surface relevant roles immediately.

### 2. Filtering
A dedicated filter sidebar (collapsible into a toggle panel on mobile) lets users narrow results across four independent, combinable dimensions:

- **Category** — Backend, Frontend, Full Stack, Data, QA, DevOps
- **Work setting** — Remote, Hybrid, Onsite
- **Experience level** — Intern, Fresher, 1–3 yrs, 3–5 yrs
- **Job type** — Full-time, Internship, Contract

Each filter checkbox displays a live count of how many current listings match, so users can see the impact of a filter before applying it — no dead-end filter combinations that silently return zero results without warning.

A **minimum salary slider** (0–15+ LPA) lets users set a compensation floor, filtering out roles below that threshold based on each listing's upper salary band.

An active filter count badge and a **"Clear all"** link appear whenever any filter is applied, so users always have a fast way back to the full board.

### 3. Sorting
A sort dropdown reorders the currently filtered results by:
- Newest first (default)
- Salary: high to low
- Salary: low to high
- Company name (A–Z)

Sorting and filtering compose together — sort order is reapplied automatically whenever the filtered set changes.

### 4. Save for later (bookmarking)
Every card has a bookmark toggle in its top-right corner. Saved jobs are tracked in-session and surfaced through a dedicated **"Saved"** tab in the top navigation, with a live count badge. This lets a user browse broadly, mark roles of interest, and return to a focused shortlist without losing their place. The save state is reflected consistently between the card view and the detail modal.

### 5. Job detail view
Clicking (or pressing Enter on) a card opens a detail modal with the full listing:
- Role title, company, location, and metadata chips (work setting, experience level, job type, posting age)
- Full role description
- "What you'll do" — responsibilities list
- "What we're looking for" — requirements list
- Full skill tag list
- Compensation, save toggle, and an **Apply now** action

The modal is dismissible via a close button, clicking outside it, or the **Escape** key.

### 6. Apply flow
Clicking "Apply now" opens a lightweight confirmation step showing the role and company before submission. Confirming triggers a toast notification ("Pinned! Your application to [Company] was sent.") and returns the user to the board — giving clear, immediate feedback that the action succeeded without requiring a full page navigation.

### 7. Empty states
Two distinct empty states, each with a clear next action rather than a dead end:
- **No results from filters**: "No jobs match these filters" with a one-click "Clear filters" button.
- **No saved jobs yet**: "Nothing pinned yet" with a one-click "Browse all jobs" button back to the main tab.

### 8. Responsive design
- Below 860px, the filter sidebar collapses behind a "Filters" toggle button showing the active filter count, and the card grid reduces to a single column.
- Below 480px, spacing, font sizes, and modal layout adjust further for small-screen comfort, including stacking the apply/save/salary row in the detail modal vertically.
- All interactive elements (cards, buttons, checkboxes, the salary slider) are touch-friendly with adequate tap targets.

### 9. Accessibility
- Cards are keyboard-focusable (`tabindex`) and operable via Enter, with visible focus outlines.
- The search input, filters, and buttons all use native, screen-reader-friendly HTML elements (`input`, `label`, `button`, `select`) rather than non-semantic custom widgets.
- Save/bookmark buttons include descriptive `aria-label`s that update based on state ("Save job" vs. "Remove from saved").
- `prefers-reduced-motion` is respected — animations and transitions are effectively disabled for users who request reduced motion at the OS level.

### 10. At-a-glance stats
The hero section surfaces three live counters computed from the current listing set: total roles pinned, roles posted in the last week, and roles marked as urgently hiring — giving users an immediate sense of board activity before they start filtering.

---

## Tech stack

- **HTML/CSS/vanilla JavaScript** — no frameworks or build tooling; the entire application is a single static file
- **Google Fonts** (Courier Prime, IBM Plex Sans, IBM Plex Mono) loaded via CDN
- **In-memory state** — search, filters, sort order, and saved jobs are held in JavaScript state for the session (no backend, no persistent storage)
- **Deployment** — static hosting on Vercel, built and deployed via a GitHub Actions CI/CD workflow (`.github/workflows/deploy.yml`) that runs on every push to `main`

---

## Data

All 14 job listings are seeded mock data representing realistic roles at recognizable Indian tech employers and startups, spanning fresher, internship, and 1–3 year experience levels. There is no backend or live data source — this is a front-end feature and UX demonstration, not a production job aggregation service.

---

*This documentation was generated with AI assistance (Claude) as part of the project's assessment deliverables.*
