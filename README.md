# Budget tracker (general)

Reads RBC Visa `.csv` and Amex `.xls` statements, sorts spending into categories, and writes a monthly Excel report.

**Setup:** Python 3, then `pip3 install -r requirements.txt` (needs `openpyxl` and `xlrd` for Amex files).

**Run:** Put your downloads in a folder (e.g. `credit_statements/`), then:

```bash
python3 budget_tracker_general.py credit_statements/
```

First run asks for income and savings settings and saves them to `budget_config.json`. Change those anytime with `python3 budget_tracker_general.py credit_statements/ --setup`. You can also pass a single `.csv` or `.xls` file instead of a folder. Output is `budget_YYYY_MM.xlsx` in this directory.
