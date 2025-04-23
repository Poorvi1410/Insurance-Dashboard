# Spiral Insurance Dashboard



## Problem Statement

This dashboard provides Spiral Insurance Pvt. Ltd. with a comprehensive overview of their policy landscape, claim patterns, and customer feedback. It aims to help management understand key performance indicators like premium amounts, coverage totals, and claim payouts across different policy types, age groups, and time periods.

Furthermore, by integrating and analyzing customer feedback through sentiment analysis, the dashboard identifies areas of customer satisfaction and concern. This allows Spiral Insurance to pinpoint strengths, address weaknesses, and make data-driven decisions to improve customer retention and business performance.

## Steps followed

-   **Step 1 : Load Data:** Loaded data into Power BI Desktop from two Excel files: `Insurance data.xlsx` and `Customer feedback.xlsx`.
-   **Step 2 : Data Exploration (Power Query):** Opened Power Query Editor. Used view tab options ("column distribution", "column quality", "column profile") to check data integrity.
-   **Step 3 : Data Profiling Scope:** Ensured column profiling was based on the entire dataset.
-   **Step 4 : Data Cleaning:** Handled inconsistencies or missing values, particularly noted in `ClaimDate` and `ClaimAmount` for policies without claims. Ensured correct data types were set.
-   **Step 5 : Create Date Table:** Added a dedicated Date Table using DAX for time-based analysis and filtering. Established relationships between the Date Table and relevant date columns in the `Insurance data` table.
-   **Step 6 : Theme Selection:** Selected a dark theme for the report in the View tab.
-   **Step 7 : Add Calculated Columns (DAX):**
    *   Created an `Age Group` column in the `Insurance data` table to categorize customers based on `Age`.
    *   Created a `Policy Status` column (`Active`/`Inactive`) in the `Insurance data` table based on `PolicyEndDate` compared to the current date.
-   **Step 8 : Sentiment Analysis (Python):**
    *   Configured Power BI to use a local Python environment with `pandas` and `vaderSentiment`.
    *   Added a step in the `Customer feedback` query to run a Python script, calculating sentiment scores using VADER.
    *   Added a `Table.Buffer()` step before the Python script to mitigate potential Formula.Firewall errors.
    *   This generated a numeric `SentimentScore` column in the `Customer feedback` table.
-   **Step 9 : Add Feedback Rating Column (M Query):** Added a custom column in the `Customer feedback` query *after* the Python script step. This used conditional logic (M language `if-then-else`) to categorize the numeric `SentimentScore` into text ratings ("Excellent", "Good", "Average", "Bad").
-   **Step 10 : Data Modeling:** Reviewed and confirmed relationships between `Insurance data`, `Customer feedback`, and `DateTable` in the Model view.
-   **Step 11 : Add Slicers:** Added slicers to the main dashboard page for `Date`, `Gender`, `PolicyNumber`, and `ClaimNumber`.
-   **Step 12 : Create Main Dashboard Visuals:**
    *   Added KPI Cards for Sum of `PremiumAmount`, Sum of `CoverageAmount`, and Sum of `ClaimAmount`.
    *   Added a Bar Chart showing `PremiumAmount` by `PolicyType`.
    *   Added a Donut Chart showing the count breakdown of `Policy Status` (Active/Inactive).
    *   Added a Ribbon Chart showing the count of claims by `ClaimStatus`.
    *   Added an Area Chart showing `ClaimAmount` by `Age Group`.
    *   Added a Matrix visual detailing claim amounts/counts by `PolicyType` (rows) and `ClaimStatus` (columns).
-   **Step 13 : Create Feedback Dashboard Visuals:**
    *   Created a separate page for feedback analysis.
    *   Added a Word Cloud visual based on the `Feedback` text.
    *   Added a Table visual displaying `Customer Name` and `Feedback`.
    *   Added a Pie Chart showing the breakdown by `Feedback Rating`.
    *   Added a Histogram showing the distribution of the numeric `SentimentScore`.
-   **Step 14 : Implement Drill-through:** Configured a drill-through page, allowing users to right-click a `PolicyType` on the main dashboard and navigate to a detailed view filtered for that specific type.
-   **Step 15 : Add Titles:** Added text boxes for titles like "SPIRAL INSURANCE PVT. LTD." on the dashboard pages.


# Snapshot of Dashboard (Main Page)

![Image](https://github.com/user-attachments/assets/30231486-4bce-4a7d-91ea-fa7ea4d3a77a)


# Snapshot of Dashboard (Drillthrough Page)

![Image](https://github.com/user-attachments/assets/dba0d56c-3209-4e7e-a3f7-1eaa8226a04a)


# Snapshot of Dashboard (Feedback Analysis Page)

![Image](https://github.com/user-attachments/assets/00cbbc4a-1051-4f84-a395-b68c5fddad99)


# Insights

The multi-page report provides several key insights:

### [1] Key Financial Metrics (Selected Period)
-   Total Premium Amount: **5.98M**
-   Total Coverage Amount: **600.55M**
-   Total Claim Amount: **16.91M**

### [2] Policy & Claim Insights
-   **Premium by Policy:** 'Travel' policies contribute the most premium (2.5M), followed by 'Health' (1.2M).
-   **Policy Status:** 58.13% of policies are 'Active'.
-   **Claim Status (Count):** Claims are most frequently 'Rejected' (4.4K), followed by 'Settled' (3.4K) and 'Pending' (2.3K).
-   **Claims by Age:** The 'Adult' age group has the highest total claim amount (8.8M).

### [3] Customer Feedback Sentiment
-   **Overall Sentiment:** Feedback is largely positive, with 'Good' (35.05%) and 'Excellent' (32.99%) being the most common ratings. 'Average' (23.71%) and 'Bad' (8.25%) represent smaller segments.
-   **Sentiment Distribution:** While scores skew positive, a distinct group of negative scores exists, highlighting specific areas of dissatisfaction.
-   **Key Themes:** The word cloud suggests common topics include "service", "policy", "claims", "easy", "good", alongside potentially negative terms like "long", "issue".

### [4] Interactivity Benefits
-   **Filtering:** Slicers allow users to focus on specific time periods, policy numbers, or customer segments.
-   **Drill-through:** Enables detailed analysis of specific policy types by navigating from the main page summary to a dedicated detail view.
-   **Cross-filtering:** Interactions between visuals (e.g., clicking 'Bad' sentiment filters the feedback table) provide context to the metrics.

These insights help Spiral Insurance identify high-performing policy types, understand claim patterns, monitor customer satisfaction, and pinpoint specific areas for operational or service improvements.
