# Budget Tracker

A command-line tool that reads RBC Visa (`.csv`) and Amex (`.xls`) credit card statements, categorizes expenses, tracks savings progress, and generates a formatted Excel summary ready for Google Sheets.

There are two versions:

- **`budget_tracker.py`** — personal version with hardcoded income and savings config
- **`budget_tracker_general.py`** — general version that prompts for your financial details

## Setup

Requires **Python 3**.

Install dependencies:

```bash
pip3 install -r requirements.txt
```

## Usage

### Personal version

Place your credit card statement files in the `credit_statements/` folder, then run:

```bash
python3 budget_tracker.py credit_statements/
```

### General version

On first run, the script will walk you through setup (income, savings rate, savings goal, etc.) and save your answers to `budget_config.json`:

```bash
python3 budget_tracker_general.py credit_statements/
```

To update your settings later:

```bash
python3 budget_tracker_general.py credit_statements/ --setup
```

You can also point either version at a single file:

```bash
python3 budget_tracker_general.py credit_statements/march-2026.csv
```

### What happens when you run it

1. Load all `.csv` (RBC) and `.xls` (Amex) files from the folder
2. Let you pick a month if multiple are present
3. Auto-categorize transactions using keyword matching
4. Prompt you to manually categorize anything it can't match
5. Print a budget summary to the terminal
6. Save a styled `.xlsx` spreadsheet (e.g. `budget_2026_03.xlsx`)

## Categories

| Category          | Examples                                  |
|-------------------|-------------------------------------------|
| Transportation    | BC Ferries, gas stations, Uber, transit   |
| Fixed Costs       | Rent, insurance, internet, mortgage       |
| Food              | Groceries, restaurants, cafes, liquor     |
| Other Necessary   | Parking, medical, car repair, bookstore   |
| Discretionary/Fun | Everything else you choose to spend       |

## Custom Keywords

When you manually categorize a transaction, the script offers to save a keyword so it auto-matches next time. These are stored in `custom_categories.json`.

## Configuration

### General version (`budget_tracker_general.py`)

Everything is entered interactively on first run and saved to `budget_config.json`:

| Setting           | Description                              |
|-------------------|------------------------------------------|
| Monthly income    | Your total monthly income                |
| Savings rate      | Percentage of income to save (e.g. 20%)  |
| Savings goal      | Total savings target                     |
| Savings balance   | Current savings balance                  |
| Savings deadline  | Target date to reach your goal (YYYY-MM) |

### Personal version (`budget_tracker.py`)

Edit the constants at the top of the file:

| Variable           | Description                          |
|--------------------|--------------------------------------|
| `STIPEND`          | Monthly stipend amount               |
| `SAVINGS_RATE`     | Fraction of income to save (0.20 = 20%) |
| `SAVINGS_GOAL`     | Total savings target                 |
| `SAVINGS_BALANCE`  | Current TFSA balance (update monthly)|
| `SAVINGS_DEADLINE` | Target date to reach savings goal    |

## Output

- **Terminal** — a summary showing income, savings progress, expenses by category, and remaining fun money.
- **Excel file** — two sheets:
  - *Summary* — the same budget overview, formatted for Google Sheets
  - *Transactions* — every categorized transaction with date, description, amount, category, and source
