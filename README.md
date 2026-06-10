# Bank Loan Risk & Performance Analysis

---

## 1. Project Overview
This project delivers a comprehensive data analytics solution designed to monitor, evaluate, and optimize a commercial bank's lending portfolio. By tracking key performance indicators across loan applications, funding allocations, and repayment collections, the dashboard provides critical visibility into portfolio health. The analytical architecture distinguishes between high-performing assets ("Good Loans") and non-performing vulnerabilities ("Bad Loans") to mitigate credit risk and improve cash flow forecasting.

---

## 2. Tools & Technologies
* **Business Intelligence:** Power BI (Data modeling, interactive dashboard design, and native filter controls)
* **Analytical Calculations:** Advanced DAX programming for dynamic Month-to-Month (**MoM**) and Month-to-Date (**MTD**) lending metrics
* **Data Categorization:** Risk segmentation matrices based on applicant employment history, debt-to-income (**DTI**) ratios, loan grades, and utilization purposes

---

## 3. Key Business Insights
* **Lending Volume & Scale:** Accumulated **38.6K** total loan applications, culminating in **$435.8M** in total funded capital and **$473.1M** in total collected revenue.
* **Portfolio Health Split:** **86.2%** of applications qualify as Good Loans (generating **$435.8M** in cash collections), while **13.8%** are flagged as Bad Loans, stalling **$65.5M** in funded capital.
* **Default Exposure:** A total of **5,333** applications have been completely **Charged Off**, directly accounting for a **$37.3M** recovery deficit relative to their funded totals.
* **Core Risk Profile:** Capital is heavily distributed at an average interest rate of **12.0%** and an average Debt-to-Income (**DTI**) ratio of **13.3%**.
* **Primary Demand Drivers:** **Debt consolidation** stands as the overwhelming primary driver for credit applications (**16K** applications), with **Renters** (**16K**) and **Mortgage holders** (**15K**) making up the vast majority of borrowers.
* **Temporal & Demographic Trends:** Credit demand displays steady month-over-month growth throughout the year, peaking in December at **3,665** applications, with the most stable borrower demographic being professionals with **10+ years** of employment history (**7.5K** applications).

---

## 4. Strategic Recommendations

* **High Debt Consolidation Concentration ➔ Portfolio Diversification** The heavy concentration of credit in debt consolidation increases structural risk. Introduce targeted marketing for lower-risk loan products (e.g., home improvement) to diversify asset distribution.

* **Charged Off Loss Metric ($37.3M Received vs $65.5M Funded) ➔ Credit Policy Tightening** Tighten underwriting requirements for applicants mirroring the profiles of high-risk "Charged Off" segments, specifically focusing on lower-grade loan tiers (Grades D through E) exhibiting elevated DTI ratios.

* **13.8% Bad Loan Ratio ➔ Automated Risk Flags** Deploy early-warning automated alerts within the CRM when an applicant's DTI tracks above the **13.3%** average, especially for shorter employment brackets (under 1 year) where default probabilities elevate.

* **Short-Term Term Structure Strategy ➔ Capital Velocity Optimization** With **75.85%** of applicants choosing shorter **36-month terms**, capitalize on this high turnover rate by offering loyalty interest incentives to repeatable, "Fully Paid" borrowers to maximize safe capital velocity.
