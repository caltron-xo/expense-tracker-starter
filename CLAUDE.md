# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # Install dependencies
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

No test suite is configured.

## Architecture

This is a single-file React app — all logic lives in `src/App.jsx` with styles in `src/App.css`. There are no separate components, hooks, or utilities yet.

**State in App.jsx:**
- `transactions` — array of `{ id, description, amount, type, category, date }`. Note: `amount` is stored as a string (not a number), which causes a known bug in the income/expense/balance calculations — `reduce` concatenates strings instead of summing.
- Form state: `description`, `amount`, `type`, `category`
- Filter state: `filterType`, `filterCategory`

**Data flow:** All filtering and summary calculations (totalIncome, totalExpenses, balance) are derived inline from `transactions` on each render — no memoization. Transactions are not persisted; they reset on page reload.

**Known intentional issues (part of the course):**
- `amount` stored as string → broken totals in summary cards
- "Freelance Work" seed transaction is typed as `expense` instead of `income`
- UI and code organization are intentionally rough
