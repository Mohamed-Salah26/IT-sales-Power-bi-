# IT Spend Analytics - Power BI Report

##  Overview
This Power BI report provides a comprehensive analysis of Information Technology (IT) spending across various business units, cost centers, and expense categories. It is designed to track budgeted vs. actual expenditures, variance trends, and forecast insights to help stakeholders optimize IT budgets and financial performance.

---

##  Data Model & Structure
The backend architecture contains a complex relational schema optimized for financial reporting (`DataModel`). It uses a star schema structure comprising:

* **Fact Tables:**
  * `IT_Spend` / `Financials`: Captures transactional or monthly level spending data including **Actuals**, **Budget**, and **Forecast** amounts.
* **Dimension Tables:**
  * `Business Unit / Department`: Breaks down spend by company organizational hierarchies.
  * `Cost Center`: Identifies specific operational segments incurring costs.
  * `Expense Category`: Segregates IT spend into specific types (e.g., Software Licensing, Hardware, Infrastructure, Consulting, SaaS).
  * `Date/Calendar`: A standard time intelligence dimension enabling year-over-year (YoY) and month-to-date (MTD)/year-to-date (YTD) analysis.

---

##  Key Functionalities & Visual Layout
The canvas incorporates structured layouts designed for intuitive financial overview exploration (`Report/Layout`).

* **Theme & Styling:** Customized visualization styling utilizing standard corporate and theme extensions to highlight financial targets cleanly.
* **Executive Dashboard:** High-level summary cards (KPIs) showing Total Spend, Remaining Budget, and overall Variance.
* **Trend Analysis:** Line and bar charts showing spending pacing against the fiscal calendar.
* **Granular Drill-Downs:** Matrix visuals allowing users to drill down from high-level business units down to individual cost centers or specific line-item expenses.

---

##  Core DAX Calculations & Measures
The data model relies heavily on standard financial DAX patterns to compute dynamic variances and time-intelligent calculations:

### 1. Base Financial Aggregates
* **Total Actual Spend:** 
  ```dax
  Total Actuals = SUM(IT_Spend[ActualAmount])
  ```
* **Total Budget:** 
  ```dax
  Total Budget = SUM(IT_Spend[BudgetAmount])
  ```

### 2. Variance Metrics
* **Budget Variance (Absolute):** Measures how much the actual spend deviates from the plan.
  ```dax
  Budget Variance = [Total Actuals] - [Total Budget]
  ```
* **Variance Percentage:** Yields a standardized percentage metric of budget adherence.
  ```dax
  Variance % = DIVIDE([Budget Variance], [Total Budget], 0)
  ```

### 3. Time Intelligence Measures
* **Year-to-Date (YTD) Actuals:** Computes standard cumulative spending across the active fiscal year.
  ```dax
  Actuals YTD = TOTALYTD([Total Actuals], 'Calendar'[Date])
  ```
* **Prior Year (PY) Spend Comparison:**
  ```dax
  Actuals PY = CALCULATE([Total Actuals], SAMEPERIODLASTYEAR('Calendar'[Date]))
  ```

---
**This Project is done by me (Mohamed Salah) to show my capabilities in dealing with power bi desktop, the project data is derived from Myonline TrainingHub channel from youtube**
