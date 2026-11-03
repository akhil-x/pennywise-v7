# Pennywise Personal Finance Manager — v7

Pennywise v7 is a frontend-only personal finance application built with React, Vite, custom CSS and Lucide icons and localStorage. No backend, authentication or bank connection is included.

## Run locally

```bash
npm install
npm run dev
```

## v7 highlights

### Financial ledger and migration
- Introduces versioned `pw_v7_*` localStorage keys and a one-time migration from v6 keys.
- Creates a pre-migration local backup before copying existing data.
- Keeps the existing transaction list as the central cash-movement ledger.
- Account balances are derived from opening balances plus ledger movements.
- Transfers and balance adjustments are represented as ledger entries.
- Savings goal allocations no longer create artificial account expenses.

### Investments
- Investment purchases reduce the selected cash account and increase tracked investment holdings.
- Market valuation edits do not change cash balances.
- Adds investment sale and dividend actions.
- Separates investment purchase/sale activity from ordinary income and expense analytics.

### Loans and EMI
- Loan disbursements increase cash and create a liability, without being counted as salary/income.
- EMI entry splits principal and interest.
- Principal repayment reduces the loan liability; interest is included in expenses.
- Loan-linked transactions remain visible in Transactions.

### Accounts and transaction management
- Account reconciliation compares the calculated balance with the actual bank/wallet balance and records a traceable adjustment.
- Account deletion requires reassignment of its existing transactions.
- Transactions can be filtered by account, type and month.
- CSV/XLSX bank statement import supports common date, description, debit, credit, amount and type columns, with duplicate checks and a confirmation summary.

### Planning and analysis
- Optional weekly, monthly and yearly recurring transaction rules. Due items are only posted when the user selects **Generate due**.
- Budget usage notices at 50%, 80% and 100%.
- Local net-worth snapshots and a history chart.
- Existing daily, weekly, monthly and yearly analytics, pie/bar charts, Excel and PDF exports are retained.
- Full JSON backup and restore now include accounts, loans, recurring rules, categories, settings and net-worth history.

## Data and migration notes

- v7 uses `pw_v7_ledger`, `pw_v7_accounts`, `pw_v7_budgets`, `pw_v7_goals`, `pw_v7_investments`, `pw_v7_loans`, `pw_v7_categories` and `pw_v7_settings`.
- A one-time migration copies existing v6 records and stores a raw pre-migration snapshot in `pw_v7_pre_migration_backup`.
- Existing v6 savings contribution auto-expense entries are omitted from the new ledger migration because goal allocations are not cash expenses. Existing investment purchase entries remain cash outflows.
- Historical EMI records from v6 remain as legacy cash outflows because their principal/interest split cannot be reconstructed automatically. New EMI entries are split correctly.
- Export a JSON backup before testing or clearing browser storage.

## Frontend-only limitations

All data remains in the browser's localStorage. Clearing browser data can remove records; JSON backups are strongly recommended. Bank statement import reads files locally in the browser and does not connect to a bank. There is no cloud sync, multi-device sync, automatic bank feed, or real-time market price feed. Investment valuations are entered by the user. PDF export uses the browser print dialog; choose **Save as PDF**.
