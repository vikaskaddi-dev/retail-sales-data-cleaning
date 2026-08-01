# Retail Sales Data Cleaning & Exploration

Cleaned and analyzed a messy, realistic retail sales dataset using Python and Pandas — fixing duplicate records, inconsistent formatting, missing values, and invalid entries — then produced summary statistics and visual insights.

## The Problem

The raw dataset (`messy_sales_data.csv`, 515 rows) simulated common real-world data quality issues:

- **Duplicate rows** — ~15 exact duplicate transactions
- **Inconsistent date formats** — mixed `DD-MM-YYYY`, `MM/DD/YYYY`, `YYYY.MM.DD`, and `DD/MM/YYYY` in the same column
- **Inconsistent text formatting** — product/category/city names entered with mixed casing and extra whitespace (e.g. `"T-Shirt"`, `"tshirt"`, `"T Shirt"`, `" Jeans"`)
- **Messy numeric data** — the `Revenue` column mixed plain numbers, currency-symbol strings (`₹37,828.90`), and the literal text `"N/A"`
- **Invalid values** — a few negative quantities (data-entry sign errors)
- **Missing values** — scattered across Product, City, Quantity, UnitPrice, and PaymentMode

## What I Did

1. **Removed duplicates** — deduplicated on business columns rather than the row ID
2. **Standardized text fields** — stripped whitespace, normalized casing, and mapped product name variants to one canonical label per product
3. **Parsed inconsistent dates** — tried multiple known date formats per value to get a single clean `datetime` column
4. **Cleaned the Revenue column** — stripped currency symbols/commas, coerced to numeric, and recomputed revenue where possible instead of dropping rows
5. **Fixed invalid values** — converted negative quantities to absolute values
6. **Handled missing values with a documented strategy** (not a blanket `dropna()`):
   - Dropped rows missing Product/City/Category (unsafe to guess identity fields)
   - Imputed Quantity/UnitPrice with the column median
   - Filled missing PaymentMode with `"Unknown"`
7. **Generated summary statistics** — total revenue, average order value, revenue by product/city, monthly revenue trend
8. **Visualized results** — revenue by product and monthly revenue trend charts

## Tools

Python · Pandas · NumPy · Matplotlib · Jupyter Notebook

## Files

| File | Description |
|---|---|
| `sales_data_cleaning.ipynb` | Full cleaning + analysis notebook, with explanations for each step |
| `messy_sales_data.csv` | Raw input data (515 rows, intentionally messy) |
| `cleaned_sales_data.csv` | Final cleaned output (470 rows, zero missing values) |
| `revenue_charts.png` | Revenue by product and monthly revenue trend charts |

## How to Run

1. Clone or download this repo
2. Install dependencies:
   ```
   pip install pandas numpy matplotlib jupyter nbformat
   ```
3. Open `sales_data_cleaning.ipynb` in Jupyter Notebook, JupyterLab, VS Code (with the Jupyter extension), or Google Colab
4. Run all cells

## Key Cleaning Summary

| Issue | Rows Affected | Action Taken |
|---|---|---|
| Duplicate rows | ~15 | Dropped |
| Inconsistent text formatting | All rows | Standardized casing/whitespace, mapped name variants |
| Inconsistent date formats | All rows | Parsed against 4 known formats |
| Currency symbols / "N/A" in Revenue | ~20% | Cleaned and coerced to numeric |
| Negative quantities | ~2% | Converted to absolute value |
| Missing Product/City/Category | ~3% | Dropped |
| Missing Quantity/UnitPrice | ~3% | Imputed with median |
| Missing PaymentMode | Some rows | Filled with "Unknown" |
