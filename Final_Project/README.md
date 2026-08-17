# Final Project — Bank Loan Analytics Dashboard

An end-to-end Excel analytics project that turns a raw loan-transactions dataset into an interactive, Power Pivot–driven dashboard. Built as the capstone deliverable for the Excel track, it demonstrates data cleaning with Power Query, a proper star-schema data model, DAX-based aggregation via PivotTables, and dashboard design.

## What's in this folder

| File | Description |
|---|---|
| `My_project.xlsx` | The full workbook — Power Query queries, Power Pivot data model, PivotTables, and the final dashboard |
| `Screenshot (61).png` | Final dashboard view (KPI cards, sales-by-branch, product mix, monthly case volume) |
| `Screenshot (63).png` | "Analytics Engine" sheet — the PivotTable cards and charts feeding the dashboard |
| `Screenshot (64).png` | Power Pivot table view of `LoanDetails` |
| `Screenshot (65).png` | Data model diagram showing table relationships |
| `Screenshot (66).png` | Power Query editor showing the cleaning steps applied to `LoanDetails` |

## Data model

The workbook uses a star-schema data model built in Power Pivot, with `LoanDetails` as the fact table and three supporting dimension tables:

```
        Branch (1) ──── (*) LoanDetails (*) ──── (1) Products
                              │
                            (*)
                              │
                             (1) Calendar
```

- **Branch** — Branch ID, Branch Name
- **LoanDetails** (fact table, 999 rows) — Transaction ID, Customer ID, Product ID, Branch ID, Officer ID, Application Date, Disbursement Date, Requested Amount, Loan Amount, Tenor (Months), Approval Status, Installment Amount, TAT, SLA
- **Products** — Product ID, Product Name
- **Calendar** — Date, Year, Month Number, Month, Day Of Week Number, Day Of Week, plus a Year → Month date hierarchy for time-intelligence and drill-down

## Data preparation (Power Query)

Each source table is cleaned through Power Query before being loaded into the data model. The applied steps on `LoanDetails` include:

- Changed column data types
- Renamed columns for consistency
- Removed unnecessary columns
- Removed blank rows
- Removed duplicate records (deduplicated on Transaction ID)

## Dashboard

The **Dashboard** sheet presents four KPI cards and three charts, all driven by PivotTables/PivotCharts connected to the data model:

**KPI cards**
- Total Sales
- Total Requested (amount)
- Count of Cases
- Total Approved

**Charts**
- Total Sales per Branch (bar chart)
- Product Sales mix (pie chart — Personal, Auto, Business, Education, Home Loan)
- Total Cases per Month (line chart, 2024)

The **Analytics Engine** sheet is the supporting layer: it holds the underlying PivotTable cards and chart data (Branch Sales, Top 5 Officers by sales, Product Sales, monthly transaction counts) that the Dashboard sheet references.

## Sample findings from the dataset

> Note: this is a synthetic/practice dataset (placeholder city and product names), used here to demonstrate the modeling and dashboarding workflow rather than to represent real bank data.

- 999 loan cases, ~38.5M total approved sales against ~345M total requested
- Loan products are fairly evenly split, each in the 17–21% range of total sales
- Case volume by month ranges roughly from the low 30s to mid 50s, with December the highest

## Skills demonstrated

- Power Query: data cleaning, type correction, deduplication
- Power Pivot: relational data modeling (star schema) across four tables
- PivotTables/PivotCharts sourced from the data model
- Dashboard design: KPI cards, chart layout, and visual hierarchy

## How to use

1. Open `My_project.xlsx` in Excel (Power Pivot / Data Model support required — available in Excel 2016+ and Microsoft 365).
2. Go to **Data → Queries & Connections** to inspect or refresh the Power Query steps.
3. Use **Power Pivot → Manage** to view the data model and relationships.
4. View the finished result on the **Dashboard** sheet; the supporting PivotTables are on the **Analytics Engine** sheet.
