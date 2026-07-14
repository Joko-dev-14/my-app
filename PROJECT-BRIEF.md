# Financial App Store — Frontend Test

**Time:** 1–2 hours  
**Stack:** React (preferred) — style it however you like (Tailwind, CSS modules, styled-components, plain CSS)

---

## Overview

We'd like you to recreate the **Financial App Store** design included with this brief (`design-1.png`). Think of it as a mini marketplace where users can browse, filter, and favourite financial tools.

Try to match the design as closely as you can — layout, spacing, and component structure all matter. That said, we're not chasing pixel perfection; we also want to see how you approach clean, readable code.

---

## What to build

### Page layout

The page has three areas:

- A **header** across the top — logo/title on the left, search bar on the right
- A **sidebar** on the left for filters
- A **card grid** in the main area showing the apps

### Sidebar filters

- **Category** — All, Investment, Banking, Lending, Insurance, Crypto
- **Min Rating** — All, 4+, 3+, 2+
- **Liked** — toggle to show only favourited apps
- **Downloads** — All, High (1M+), Medium (100K+), Low
- A **Clear All Filters** button near the top of the sidebar

Only one option should be active at a time per group, and the active state should be clearly visible.

### App cards

Each card should show:
- A logo (SVG assets are in `/assets`, named `app-1.svg` through `app-48.svg`)
- App name
- Category badge
- Short description
- Star rating and numeric score
- Download count
- A **favourite (heart) button** that toggles on/off

Cards should have a subtle hover effect.

### Above the grid

Show a results count (e.g. *"Showing 11 of 48 apps"*) and a **Sort** button on the right.

---

## Data

All 48 apps are provided in `mockData.ts` — each has a name, description, category, rating, and download count. Import it directly into your components.

## Getting started

Scaffold a new React app however you prefer:

```bash
npx create-react-app my-app --template typescript
# or
npm create vite@latest my-app -- --template react-ts
```

Then copy `mockData.ts` and the `assets/` folder into your `src/` directory.

---

## Icons & assets

The reference design uses **Material Icons** for UI icons and the provided **SVG assets** for app logos — but feel free to use whatever icon library or approach you prefer. The SVG assets are in `/assets`, named `app-1.svg` through `app-48.svg`, and each app in `mockData.ts` has an `id` that maps to its file (e.g. id `1` → `app-1.svg`).

## What we're looking for

- How closely you've matched the provided design
- A layout that feels clean and easy to use
- Visible and intuitive filter interactions
- Readable, well-structured code
- Attention to small details — spacing, alignment, hover states

---

## Bonus (if you have time)

- Wire up the filters so they actually filter the data
- Add working search
- Mobile-friendly layout

---

Good luck — keep it simple and have fun with it!
