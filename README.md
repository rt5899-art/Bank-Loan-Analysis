# Bank Loan Analysis

## Project Overview

This project performs a comprehensive analysis of a bank's loan portfolio to uncover patterns in loan applications, funding, repayment, and risk classification — supporting data-driven decision-making in credit operations. The same analysis has been implemented across three platforms to serve different audiences and use cases:

- **SQL** — for data extraction, transformation, and KPI computation directly against the database
- **Power BI** — for interactive dashboards and executive-level reporting
- **Python (Jupyter Notebook)** — for exploratory data analysis, statistical computation, and custom visualizations

Together, the three implementations form a complete end-to-end analytics pipeline: SQL handles the data layer, Python handles deep analysis, and Power BI handles presentation and stakeholder reporting.

---

## Dataset

The source dataset is `financial_loan_data_excel.xlsx`, an Excel file containing individual loan records with the following key fields:

- `id` — unique loan identifier
- `issue_date` — date the loan was issued
- `loan_amount` — principal amount funded
- `total_payment` — total amount received from the borrower
- `int_rate` — interest rate on the loan
- `dti` — debt-to-income ratio
- `loan_status` — current status (Fully Paid, Current, Charged Off)
- `address_state` — borrower's state
- `term` — loan repayment term (36 or 60 months)
- `emp_length` — borrower's employment length
- `purpose` — stated purpose of the loan
- `home_ownership` — borrower's housing status (Own, Rent, Mortgage, etc.)

---

## Requirements

### SQL
- Any standard relational database — MySQL, PostgreSQL, or MS SQL Server
- Access to import the source Excel/CSV data into a table
- A SQL client (DBeaver, pgAdmin, SSMS, or equivalent)

### Power BI
- Power BI Desktop (free) or Power BI Service (Pro for sharing)
- The source Excel file or a connected SQL database as the data source
- Basic knowledge of DAX for custom measures (MTD, percentage calculations)

### Python
- Python 3.8 or above
- Jupyter Notebook or JupyterLab

The following Python libraries are required:

- `pandas` — data loading, cleaning, and aggregation
- `numpy` — numerical operations
- `matplotlib` — static chart rendering
- `seaborn` — statistical visualization support
- `plotly` — interactive treemap visualizations
- `openpyxl` — reading `.xlsx` files via pandas

Install all Python dependencies using:

```bash
pip install pandas numpy matplotlib seaborn plotly openpyxl
```

---

## Tools and Technologies

| Tool / Technology | Implementation | Purpose |
|---|---|---|
| SQL | SQL layer | KPI queries, filtering, aggregations, MTD calculations |
| Power BI Desktop | Power BI layer | Dashboard design, DAX measures, interactive reporting |
| DAX | Power BI layer | Custom calculated measures and time intelligence |
| Python 3.8+ | Python layer | Exploratory analysis and custom visualizations |
| Pandas | Python layer | Data manipulation and KPI computation |
| NumPy | Python layer | Numerical aggregations |
| Matplotlib | Python layer | Time-series, bar, and pie charts |
| Plotly Express | Python layer | Interactive treemap visualizations |
| Jupyter Notebook | Python layer | Analysis environment and narrative presentation |
| Excel (.xlsx) | All layers | Primary source data format |

---

## Project Structure

### SQL
The SQL implementation covers:
- Total loan applications, funded amounts, and amounts received
- MTD and month-over-month KPI calculations
- Good loan vs. bad loan segmentation by status
- Breakdowns by state, term, employment length, purpose, and home ownership

### Power BI
The Power BI implementation covers:
- A summary KPI dashboard with cards for total applications, funded amount, amount received, average interest rate, and DTI
- Trend charts for monthly loan activity
- Regional map visual for state-level distribution
- Slicers for loan status, purpose, term, and home ownership filtering
- DAX measures for MTD metrics and percentage calculations

### Python (Jupyter Notebook)
The notebook is organized into the following sections:

1. Library imports and data loading
2. Metadata exploration — shape, data types, descriptive statistics
3. KPI computation — total applications, funded amounts, amounts received, interest rates, DTI
4. Month-to-date (MTD) KPI calculations
5. Loan quality segmentation — good loans (Fully Paid / Current) vs. bad loans (Charged Off)
6. Visual analysis across six dimensions:
   - Monthly trends (funded amount, received amount, application volume)
   - Regional analysis by US state
   - Loan term breakdown
   - Borrower employment length
   - Loan purpose
   - Home ownership

---

## Key Insights

- The portfolio is dominated by good loans (Fully Paid + Current), which account for the large majority of applications, indicating a reasonably healthy credit book overall.
- Charged-off (bad) loans represent a meaningful share of total funded capital that was not recovered, highlighting real credit risk exposure.
- Loan applications and funding amounts show a consistent upward trend month over month, suggesting growing demand for credit.
- A few states — likely larger population centers — account for a disproportionately large share of both funded amounts and repayments, pointing to geographic concentration risk.
- The 36-month term is more popular than the 60-month term by both application count and funded volume, which may reflect borrower preference for shorter commitments.
- Borrowers with longer employment histories (10+ years) receive the highest total funded amounts, suggesting employment stability is a key factor in loan sizing.
- Debt consolidation is by far the most common loan purpose, followed by credit card refinancing, indicating a borrower base actively managing existing debt loads.
- Mortgage holders and renters dominate the application pool, with outright homeowners representing a much smaller segment.
- The average DTI and interest rate serve as useful baseline benchmarks for assessing portfolio risk and pricing adequacy.

---

## Challenges Faced

- Keeping KPI results consistent across all three platforms required careful alignment of business logic — especially for MTD calculations, which each tool handles differently (SQL window functions, DAX time intelligence, and pandas date filtering).
- In Python, sorting monthly trends chronologically required explicit `sort_values` before groupby to prevent alphabetical month-name ordering, which would misrepresent the time series.
- The Python notebook contains inconsistent currency symbols across chart labels — some show `$` and others show `₹` — which is a copy-paste oversight that needs correction.
- Plotly treemaps render interactively in Jupyter but do not display correctly in static notebook exports (PDF, HTML snapshot), creating a documentation gap.
- Power BI's default date hierarchy can conflict with custom MTD DAX measures if the date table is not properly marked as a date table in the model.
- The dataset lacks a loan grade or credit score column, which limits risk segmentation depth across all three implementations.
- Importing the Excel source into SQL required handling date format inconsistencies, as Excel serial dates and string-formatted dates behave differently depending on the database engine used.

---

## Recommendations for Improvement

- Build a shared data model — ideally a cleaned, normalized SQL database — that all three tools (SQL queries, Power BI, and Python) connect to directly, rather than each reading from the raw Excel file independently. This eliminates inconsistency and makes the pipeline maintainable.
- Standardize currency symbols across all Python chart labels. The current mix of `$` and `₹` is misleading and should be corrected to match the actual currency of the dataset.
- Add a loan grade or risk tier breakdown (using a `grade` or `sub_grade` column if available) to enrich risk segmentation beyond the binary good/bad classification across all three platforms.
- In Python, replace static matplotlib charts with Plotly for all visualizations to achieve consistent interactivity and hover tooltips throughout the notebook, not just in the treemaps.
- In Power BI, add drill-through pages so users can click a state or purpose and navigate to a borrower-level detail view.
- In SQL, add views or stored procedures for the most frequently used KPI queries so they can be reused by both the Python layer and Power BI without rewriting logic.
- Introduce a correlation heatmap in the Python notebook between numeric variables (loan amount, DTI, interest rate, total payment) to surface multivariate relationships not visible in individual charts.
- Parameterize MTD calculations in Python so the reference month can be set manually rather than always defaulting to the maximum date in the dataset, making the notebook reusable across reporting periods.
- Add data validation checks at the top of the Python notebook (null counts, duplicate IDs, date range sanity) to make the pipeline more robust against data quality issues.
- Consider building a simple predictive model (logistic regression or decision tree) in Python to quantify which borrower features most strongly predict loan default, and surface the outputs back into Power BI as a risk score.
