# Finlo — Finance Dashboard

A clean, interactive personal finance dashboard built as a single self-contained HTML file. No build step, no server, no dependencies to install.

---

## Quick Start

1. Open https://finance-dashboard-ui-eosin.vercel.app/ directly in any modern browser
2. That's it — no setup required

All data is persisted automatically via `localStorage`, so your transactions survive page refreshes.

---

## Features

### Dashboard Overview
- **4 summary cards** — Total Balance, Monthly Income, Monthly Expenses, Savings Rate — each with month-over-month change indicators
- **Balance trend chart** (Chart.js line chart) — income vs expenses across the last 6 months
- **Spending by category** (doughnut chart) — with a custom legend showing amounts and percentages
- **Recent activity list** — last 5 transactions at a glance

### Transactions
- Full sortable/filterable table of all transactions
- **Filters**: by type (income/expense), category, month, and a live global search
- **Sorting**: newest first, oldest first, highest/lowest amount
- Merchant icons using category emojis for fast scanning
- Empty state when no results match filters
- **Add / Edit / Delete** transactions (Admin role only)

### Role-Based UI
Switch roles via the sidebar dropdown:
- **Admin** — full CRUD access; can add, edit, and delete transactions; sees action buttons throughout
- **Viewer** — read-only; all mutation controls are hidden via CSS (`[data-role="viewer"] .admin-only { display: none }`)

### Insights
- **Top spending category** — highest cumulative expense category
- **Average transaction size** — mean expense amount
- **Net cashflow** — all-time income minus expenses
- **Monthly comparison bars** — proportional expense bars per month
- **Category breakdown** — progress bars with percentages per spending category
- **Observations panel** — auto-generated contextual insights (savings rate, MoM change, top category callout)

### Additional
- **Dark mode** — toggle via the moon icon in the topbar; preference saved to localStorage
- **CSV export** — downloads all transactions as a `.csv` file
- **Data persistence** — all transactions stored in localStorage; seed data included for demo

---

## Tech Stack

| Concern | Approach |
|---|---|
| Framework | Vanilla HTML/CSS/JS — no build toolchain |
| Charts | Chart.js 4.4.1 (CDN) |
| Fonts | DM Serif Display + DM Sans (Google Fonts) |
| Styling | Pure CSS with custom properties (CSS variables) for theming |
| State | Single in-memory JS object + localStorage persistence |
| Data | 28 mock transactions seeded across 6 months |

---

## State Management

State lives in three places:

- `transactions[]` — the master array of all transaction objects; mutated by add/edit/delete and synced to `localStorage` on every change
- Filter state (`typeFilter`, `catFilter`, `monthFilter`, `sortMode`, `searchQuery`) — plain JS variables; all render functions read from these before filtering
- `currentRole` — drives which elements the CSS `admin-only` class hides

All render functions (`renderDashboard`, `renderTransactions`, `renderInsights`) are pure in the sense that they always re-derive their output from the current state — there's no incremental patching.

---

## Project Structure

```
finance-dashboard.html   ← Everything: markup, styles, scripts, data
README.md
```

Single-file architecture was chosen deliberately — it means zero setup, easy sharing, and straightforward evaluation.

---

## Assumptions

- Currency is Indian Rupees (₹) — mock data reflects typical Indian salary and expense ranges
- "Current month" is determined from the most recent transaction date in the dataset, not today's wall-clock date (so the demo always looks meaningful regardless of when it's opened)
- Roles are frontend-only simulation — no authentication backend
