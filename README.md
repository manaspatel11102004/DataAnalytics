# Sales Insights Data Analysis Dashboard

A multi-page interactive Business Intelligence dashboard built using Microsoft Power BI
to analyse business sales data across customers, products, markets, and time periods.

## 🛠️ Tools & Technologies
- Microsoft Power BI Desktop
- Power Query (M Language) — ETL & Data Transformation
- DAX (Data Analysis Expressions) — KPI Calculations
- SQL Server / MySQL — Data Source
- Microsoft Excel — Supporting Data Source

## 📊 Dashboard Pages
1. Executive Summary
2. Sales & Revenue Deep Dive
3. Customer Performance
4. Product Portfolio
5. Market & Regional Performances
6. Strategic Insights
7. Profit Breakdown
8. Q&A (Natural Language Queries)

## ⚙️ Key Features
- Star schema data model (1 fact table + 4 dimension tables)
- 22 custom DAX measures (Revenue, Profit Margin %, YOY Growth %, AOV, and more)
- ETL pipeline using Power Query for data cleaning and transformation
- Interactive slicers, drill-through, and bookmark navigation
- Cross-page synchronized filters (Customer Type, Year, Month)

## 🗄️ Database Setup

1. Install MySQL on your local computer:
   https://www.youtube.com/watch?v=WuBcTJnIuzo

2. Download `db_dump.sql` from this repository and import it as per the instructions in the video above.

## 🔍 Data Analysis Using SQL

```sql
-- Show all customer records
SELECT * FROM customers;

-- Show total number of customers
SELECT count(*) FROM customers;

-- Show transactions for Chennai market (market code: Mark001)
SELECT * FROM transactions WHERE market_code='Mark001';

-- Show distinct product codes sold in Chennai
SELECT DISTINCT product_code FROM transactions WHERE market_code='Mark001';

-- Show transactions in USD
SELECT * FROM transactions WHERE currency='USD';

-- Show transactions in 2020 joined with date table
SELECT transactions.*, date.*
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020;

-- Show total revenue in 2020
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020
AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');

-- Show total revenue in January 2020
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020
AND date.month_name = 'January'
AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');

-- Show total revenue in 2020 for Chennai
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020
AND transactions.market_code = 'Mark001';
```

## ⚡ Data Transformation — Power Query

Currency normalization formula (USD to INR conversion):

```
= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" 
or [currency] = "USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)
```

## 📸 Screenshots
<!-- Add your dashboard screenshots here -->

## 🚀 How to Use
1. Clone or download the repository
2. Set up MySQL and import `db_dump.sql`
3. Open the `.pbix` file in Power BI Desktop
4. Update the database connection to your local instance
5. Refresh data and explore the dashboard

## 📁 Project Structure
```
├── dashboard/
│   └── SalesInsightsDashboard.pbix
├── screenshots/
│   └── (dashboard page images)
├── data/
│   └── db_dump.sql
└── README.md
```

## 🏢 Developed During
GTU Internship 2026 — PS Infotech, Pune
