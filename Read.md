# Sales-Dashboard (Tableau)

## Problem Statement

This dashboard helps the business understand where sales and profit are coming from, and where they're leaking. By breaking Profit down by Region and Customer Segment, the business can see which regions are actually profitable and which are dragging performance down. The Sales-by-Region breakdown shows how revenue is distributed geographically, the Order Quantity trend over time reveals seasonality and growth/decline patterns, and the Profit-vs-Sales scatter plot (by customer) helps flag customers who generate high sales but low (or negative) profit — a sign of over-discounting or high-cost servicing.

Since all four views are linked through cross-filter actions on the dashboard, selecting a Region or Customer Segment in one chart instantly filters the other three, making it easy to drill into any specific slice of the business (e.g. "West region, Corporate segment") across sales, profit, and quantity all at once.

### Steps followed

- Step 1 : Loaded the dataset (Sample Superstore Sales) into Tableau Desktop as a live/extract connection, containing fields such as `Order ID`, `Order Date`, `Ship Date`, `Sales`, `Profit`, `Discount`, `Unit Price`, `Order Quantity`, `Shipping Cost`, `Customer Name`, `Customer Segment`, `Region`, `State`, `City`, `Product Category`, `Product Sub-Category`, and `Product Name`.
- Step 2 : Created a calculated field named **"Grouping based on Unit Price"** to bucket products by price tier:

        Grouping based on Unit Price =
        IF [Unit Price] <= 2500 THEN 'A'
        ELSEIF [Unit Price] <= 5000 THEN 'B'
        ELSE 'C'
        END

- Step 3 : Built a **Bar Chart** worksheet — `SUM(Profit)` by `Region` on the Rows/Columns shelves, with `Customer Segment` used for color and label, so profit contribution by segment is visible within each region.
- Step 4 : Built a **Line Chart** worksheet — `Order Date` (by month) on Columns against `SUM(Order Quantity)` on Rows, to track order volume trends over time.
- Step 5 : Built a **Pie Chart** worksheet — wedge size driven by `SUM(Sales)`, colored and labeled by `Region`, with a percent-of-total label added so each region's share of overall sales is visible at a glance.
- Step 6 : Built a **Scatter Plot** worksheet — `SUM(Sales)` on Columns against `SUM(Profit)` on Rows, labeled by `Customer Name`, to spot customers with a poor sales-to-profit ratio.
- Step 7 : Assembled all four worksheets into a single **Dashboard 1**.
- Step 8 : Added **filter actions** so that selecting a mark in the Bar Chart, Line Chart, Pie Chart, or Scatter Plot cross-filters the other worksheets on the dashboard by `Region` and/or `Customer Segment` (on-select, auto-clear).
- Step 9 : Published the workbook (recommended: publish to **Tableau Public** to generate a shareable, no-login link).

## Insights

*(Fill in the current figures from your dashboard below — they'll shift depending on which cross-filter selections are active.)*

### Profit by Region

- Highest-profit region: `[West ( ₹.108,418)]`
- Lowest-profit / underperforming region: `[Central ( ₹.51,992)]`
- Profit split by Customer Segment within each region: `[West: Corporate (~ ₹.37,000), Consumer ( ~₹.$32,000), Home Office ( ₹.21,000), Small Business (~ ₹.18,000),
   East: Corporate (~ ₹.30,000), Consumer (~ ₹.25,000), Home Office (~ ₹.18,000), Small Business (~ ₹.18,000),
   South: Corporate (~ ₹.22,000), Consumer (~ ₹.20,000), Home Office (~ ₹.13,000), Small Business (~ ₹.12,000)
    Central: Corporate (~$18,000), Consumer (~ ₹.15,000), Home Office (~ ₹.10,000), Small Business (~ ₹.9,000)]`

### Sales by Region (Pie Chart)

- Region with the largest share of total sales: `[Central ] (32% of total)`
- Region with the smallest share of total sales: `[South ] (19.46% of total)`

### Order Quantity Trend

- Overall trend direction (growing / declining / seasonal): `[seasonal]`
- Peak order period: `[October]`

### Sales vs. Profit (Scatter Plot)

- Customers with high sales but low/negative profit (worth reviewing pricing/discounting for): `[Grant Carroll]`
- Customers with the strongest sales-to-profit ratio: `[Sanjit Chand]`

### Unit Price Grouping

- Distribution of products/orders across price tiers A (≤2500), B (2500–5000), and C (>5000): `[Total:8399]`

## Tech Stack

- Tableau Desktop / Tableau Public
- Calculated fields
- Dashboard filter actions (cross-filtering between worksheets)
