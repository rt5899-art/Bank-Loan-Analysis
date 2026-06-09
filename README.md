# Bank Loan Analysis

## Project Overview

This project presents a comprehensive Bank Loan Analysis built to monitor, evaluate, and report on lending activity across a financial institution. The primary objective is to enable data-driven decision-making by transforming raw loan application data into actionable business intelligence across three dedicated dashboard pages: Summary, Overview, and Details.

The problem it addresses is the lack of a consolidated, visual view of loan performance. Stakeholders previously had no quick way to distinguish healthy lending from risky exposure, understand borrower profiles, or track month-over-month portfolio growth. This project solves that by providing a structured, filterable reporting system covering 38,576 total loan applications, $435.8M in total funded amounts, and $473.1M in total amounts received.

![image alt](https://github.com/rt5899-art/Bank-Loan-Analysis/blob/main/ss-Bankloan_summary%20bi.png?raw=true)

---

## Requirements

### Software

- Microsoft Power BI Desktop (version 2.x or later recommended)
- Microsoft Excel 2016 or later (for data preparation and pivot analysis)
- Python 3.8 or later
- Jupyter Notebook or any compatible Python IDE (for EDA notebooks)

### Python Libraries

- pandas
- numpy
- matplotlib
- seaborn
- openpyxl (for Excel file I/O)

### Hardware

- Minimum 8 GB RAM recommended for Power BI with datasets of this size
- Windows 10 or later (Power BI Desktop is Windows-only natively)

### Prerequisites

- Basic familiarity with Power BI report navigation and slicer controls
- Access to the source loan dataset in CSV or Excel format
- A GitHub account to clone or fork the repository

---

## Tools and Technologies

- **Power BI Desktop** — Primary dashboard and visualization layer (Summary, Overview, and Details pages)
- **Microsoft Excel** — Data cleaning, preliminary analysis, and pivot table exploration
- **Python (pandas, matplotlib, seaborn)** — Exploratory data analysis (EDA) and statistical summaries via Jupyter notebooks
- **DAX (Data Analysis Expressions)** — Custom measures and KPIs within Power BI (MTD, MoM calculations, Good vs Bad Loan segmentation)
- **Power Query (M Language)** — Data transformation and shaping within Power BI
- **GitHub** — Version control and portfolio hosting

---

## Dashboard Analysis

### Page 1: Summary

![image alt](https://github.com/rt5899-art/Bank-Loan-Analysis/blob/main/ss-Bankloan_summary%20bi.png?raw=true)

The Summary page provides a high-level portfolio health snapshot. Total loan applications stand at 38,576, with a Month-to-Date (MTD) count of 4,300 and a Month-over-Month (MoM) growth of 6.9%. The total funded amount is $435.8M against a total amount received of $473.1M, indicating that repayments are exceeding disbursements — a positive cash flow signal.

The average interest rate across the portfolio is 12.0% (MTD: 12.4%, MoM growth: 3.5%), and the average Debt-to-Income (DTI) ratio is 13.3% (MTD: 13.7%, MoM growth: 2.7%).

Good loans account for 86.2% of the portfolio — 33,000 applications — with a funded amount of $370.2M and a received amount of $435.8M. Bad loans represent 13.8%, comprising 5,300 applications, $65.5M in funded amount, and $37.3M received. The gap between funded and received amounts in bad loans flags a significant recovery deficit.

The Loan Status breakdown table reveals:

- Current loans: 1,098 applications, $188.7M funded, $242.0M received, Avg Interest Rate 15.10%, Avg DTI 14.72%
- Charged Off loans: 5,333 applications, $65.5M funded, $37.3M received — these represent the at-risk segment
- Fully Paid loans: 32,145 applications, $351.4M funded, $411.6M received — the dominant healthy segment

---

### Page 2: Overview

![image alt](https://github.com/rt5899-art/Bank-Loan-Analysis/blob/main/ss-Bankloan%20overview.png?raw=true)

The Overview page breaks down loan applications across multiple dimensions to reveal behavioral and geographic trends. The KPI cards on this page reflect a filtered view (Good Loans only): 33,200 total applications, $370.2M funded, $435.8M received, 11.8% average interest rate, and 13.2% average DTI.

**Monthly Trend:** Loan applications grow consistently from 2,023 in January to 3,665 in December, demonstrating strong year-end demand. This 81% growth from January to December signals a clear seasonal pattern in loan intake.

**Geographic Distribution:** California is the dominant state by loan volume, highlighted prominently on the US map. This suggests a geographically concentrated risk and opportunity profile.

**Loan Term Split:** 75.85% (25,000) of loans are on 60-month terms, while 24.15% (8,000) are on 36-month terms. The heavy preference for longer terms increases the duration of portfolio exposure.

**Loan Purpose:** Debt consolidation is overwhelmingly the top purpose at 16,000 applications, followed by credit card (4,000), other (3,000), and home improvement (3,000). Major purchase, car, small business, and wedding loans each account for approximately 1,000–2,000 applications.

**Employment Length:** Borrowers with 10+ years of employment history are the largest group at 7,500 applications, followed by those with less than 1 year (3,900) and 2 years (3,800). Lending is broadly distributed across employment tenures.

**Home Ownership:** Renters (RENT) and mortgage holders (MORTGAGE) are the two dominant groups, each accounting for approximately 15,000–16,000 applications. Outright homeowners represent a smaller segment.

---

### Page 3: Details

![image alt](https://github.com/rt5899-art/Bank-Loan-Analysis/blob/main/ss-%20bank%20loan%20details.png?raw=true)

The Details page presents a granular, row-level loan register displaying individual records filtered to Good Loans. Each row includes Loan ID, Purpose, Home Ownership, Grade, Sub Grade, Issue Date, Funded Amount, Interest Rate, Installment, and Amount Received.

Sample records from January 2021 show funded amounts ranging from $3,000 to $20,000 with interest rates between 6% and 19%, installment values between $92 and $687, and amounts received between $3,335 and $24,741. Grade distribution spans A through E, with Sub Grades providing further risk granularity (e.g., A1, B3, E4).

This page serves as an audit and drill-down tool, allowing stakeholders to verify individual loan performance, cross-reference with portfolio-level metrics, and support compliance or investigation workflows.

---

## Challenges Faced

**1. Defining Good vs Bad Loan Segmentation**
Mapping loan status categories (Current, Fully Paid, Charged Off) into a binary Good/Bad classification required careful business logic design in DAX. Charged Off loans were classified as Bad; Current and Fully Paid as Good. This rule was validated against the Summary page figures to ensure the 86.2% / 13.8% split was consistent.

**2. MTD and MoM Calculation Accuracy**
Building time-intelligence measures (MTD funded amount, MoM growth rates) in DAX required a well-structured date table and careful use of CALCULATE and DATESINPERIOD functions. Inconsistent date formats in the source data caused initial errors that were resolved during Power Query transformation.

**3. Cross-Page Filter Consistency**
Ensuring that slicer selections (State, Grade, Good vs Bad Loan, Purpose) propagated correctly across all three pages required explicit filter context management and careful use of report-level vs page-level filters in Power BI.

**4. Data Volume and Performance**
With 38,576 records and multiple calculated columns, report rendering speed was a challenge. This was partially addressed by reducing unnecessary visual complexity and pre-aggregating measures where possible.

**5. Python EDA to Power BI Alignment**
Insights derived from Python EDA (distribution of loan grades, interest rate histograms) needed to align with DAX measures in Power BI. Discrepancies caused by differing aggregation methods required reconciliation between the two environments.

---

## Key Insights

**1. The portfolio is predominantly healthy but carries meaningful tail risk.**
With 86.2% good loans and 13.8% bad loans (5,333 charged-off applications representing $65.5M funded but only $37.3M recovered), the recovery gap on bad loans is approximately $28.2M — a material credit loss exposure.

**2. Debt consolidation dominates loan purpose.**
At 16,000 applications out of approximately 33,200 good loans reviewed on the Overview page, debt consolidation represents roughly 48% of all applications. This concentration makes the portfolio highly sensitive to consumer debt market conditions.

**3. Longer loan terms dominate.**
75.85% of loans are on 60-month terms. Longer durations increase exposure to borrower default risk over time and tie up capital longer. Only 24.15% are on the shorter, lower-risk 36-month term.

**4. Strong year-end demand acceleration.**
Monthly applications grew from 2,023 in January to 3,665 in December — an 81.3% increase within a single year. This trend is valuable for capacity planning and credit risk provisioning.

**5. Charged-off loans carry a higher average interest rate (13.88%) than fully paid loans (11.64%).**
This confirms a classic risk-return pattern: higher-rate loans carry higher default probability. The DTI for charged-off borrowers (14.00%) is also slightly elevated versus fully paid (13.17%).

**6. California is a geographic concentration risk.**
The US map on the Overview page shows California as a dominant state. Over-reliance on a single geography exposes the portfolio to regional economic downturns.


---

## Recommendations for Improvements

**1. Introduce a Predictive Default Scoring Layer**
Given that 5,333 loans (13.8%) are charged off with a $28.2M recovery gap, a machine learning model (logistic regression or gradient boosting) trained on Grade, Sub Grade, DTI, Employment Length, and Purpose could flag high-risk applications before funding. This would be built in Python and could integrate into the Power BI report via a Python visual or exported score table.

**2. Add a Geographic Concentration Risk Page**
Since California dominates application volume, a dedicated geographic page with state-level default rates, average DTI, and funded-to-received ratios would help management monitor and rebalance geographic exposure. State-level filters already exist in the slicer; a full page would surface this more prominently.

**3. Reduce 60-Month Term Concentration**
With 75.85% of loans on 60-month terms, the portfolio duration risk is high. A term-wise default rate comparison (36 vs 60 months) should be added to the Summary or Overview page to quantify this risk. If 60-month term loans show higher charge-off rates, lending policy should be reviewed.

**4. Add Vintage Analysis**
Cohort or vintage analysis (grouping loans by issue month and tracking their performance over time) would reveal whether loans issued in certain months — particularly the high-volume December cohort (3,665 applications) — perform differently. This would require expanding the Details page with a time-based cohort view.

**5. Automate Data Refresh**
The current dashboard appears to be based on a static dataset. Connecting Power BI to a live database or scheduled data pipeline (via Power BI Gateway or Python ETL scripts) would make the report operational rather than just analytical.

**6. Expand the Details Page with Search and Export**
The Details page currently displays raw loan records without search capability. Adding a loan ID search filter and an export-to-CSV button (via Power BI's built-in export feature or a Python-based data extract tool) would make it more useful for compliance and audit teams.

**7. Segment the Summary Page by Loan Grade**
The current Summary page aggregates all grades together. A Grade-level breakdown of Good vs Bad loan percentages, average interest rates, and DTI ratios would allow credit officers to evaluate whether lower-grade (D, E) loans justify their higher interest rates given their elevated default risk.

---

## Repository Structure

```
Bank-Loan-Analysis/
|-- assets/
|   |-- ss-Bankloan_summary_bi.png
|   |-- ss-Bankloan_overview.png
|   |-- ss-_bank_loan_details.png
|-- data/
|   |-- bank_loan_data.csv
|-- notebooks/
|   |-- bank_loan_eda.ipynb
|-- excel/
|   |-- bank_loan_analysis.xlsx
|-- powerbi/
|   |-- bank_loan_report.pbix
|-- README.md
|-- Image1
|-- Image2
|-- Image3
```

---

## Author

Rina Tiwari
GitHub: [github.com/rt5899-art](https://github.com/rt5899-art)
Kaggle: [kaggle.com/rinatiwari911](https://kaggle.com/rinatiwari911)
