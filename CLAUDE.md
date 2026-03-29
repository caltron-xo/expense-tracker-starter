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

The app is composed of four components with styles in `src/App.css`. Transactions are not persisted; they reset on page reload.

**Component tree:**

```
App
├── Summary
├── TransactionForm
└── TransactionList
```

**State ownership:**

- `App` — owns `transactions` (array of `{ id, description, amount, type, category, date }`) and passes it down. `amount` is a number.
- `Summary` — receives `transactions`, derives `totalIncome`, `totalExpenses`, and `balance` internally.
- `TransactionForm` — owns its own form state (`description`, `amount`, `type`, `category`); calls `onAdd(transaction)` prop on submit.
- `TransactionList` — receives `transactions`; owns `filterType` and `filterCategory` state internally.

**Known intentional issue (part of the course):**

- "Freelance Work" seed transaction is typed as `expense` instead of `income`
