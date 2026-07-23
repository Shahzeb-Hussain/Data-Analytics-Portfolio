# Sales & Promotion Competitive Intelligence Dashboard

## Problem Statement

This dashboard helps the business understand how sales, profit, and discounting are performing across customers, products, and promotions. It brings together order-level transactions with customer, product, and promotion details so that the team can quickly see which products and promotions are driving (or dragging down) revenue and profit, where customers are located, and how sales trends move over time.

By comparing Top 5 vs Bottom 5 products on sales, quantity, and profit side by side, the business can identify which items to double down on and which to re-price, bundle, or discontinue. The Comparison and Edit Interactions pages also make it possible to slice Total Sales, Total Profit, and Total Quantity Sold by date, customer, product, and promotion, so cross-filtering behavior can be controlled per visual.

## Data Model

The report is built on a star-schema style model with one fact table and several supporting dimension/date tables:

- **Fact Table** — the core transaction table: `Order ID`, `CustomerID`, `Product ID`, `PromotionID`, `Date (dd/mm/yyyy)`, `Year`, `Net Sales`, `Total Sales`, `Profit`, `Discount Percentage`, `Discount Value`, `Price Per Unit (INR)`, `Units Sold`
- **Dim Customers** — `CustomerID`, `Customer Name`, `City`
- **Dim Product** — `Product ID`, `Product Name`
- **Dim Promotion** — `PromotionID`, `Promotion Name`
- **Date Table 2** / **Data Table 1** — supporting date dimensions used to drive the slicers and the Sales Trend line chart
- **Measures Table** — a dedicated table holding key DAX measures (e.g. `Quantity sold`, `Total Measure`) so they're kept separate from the raw data tables

### Steps followed

- **Step 1**: Loaded the order/transaction data into Power BI Desktop and built out the star schema — Fact Table connected to Dim Customers, Dim Product, and Dim Promotion via their respective keys (`CustomerID`, `Product ID`, `PromotionID`), plus a date table for time intelligence.
- **Step 2**: Created a dedicated **Measures Table** to hold the report's core DAX measures separately from the data tables, keeping the field list clean.
- **Step 3**: Built key measures such as `Total Sales`, `Sum of Net Sales`, `Total Profit`, and `Quantity sold` (aggregations of `Sales`, `Net Sales`, `Profit`, and `Units Sold` from the Fact Table).
- **Step 4**: Selected a report theme (theme pack: `CY26SU05`) under the View tab for consistent styling across all pages.
- **Step 5**: Built the **Overview** page with:
  - A line chart — *Sales Trends by Period* (Net Sales by Year)
  - A scatter chart — *Profit V/S Net Sales*
  - A bar chart — *Average Discount by Promotion Categories*
  - A map visual plotting customers by `City`
  - A card visual summarizing order activity
- **Step 6**: Built the **Top/Bottom 5 Analysis** page with three matched pairs of bar charts:
  - Top 5 / Bottom 5 Products by Sales
  - Top 5 / Bottom 5 Products by Quantity
  - Top 5 / Bottom 5 Products by Profit
- **Step 7**: Built the **Comparison Sales/Profit/Quantity** page with two slicers plus clustered column charts for Total Sales, Total Profit, and Total Quantity Sold, so the business can compare all three metrics side by side under the same filter context.
- **Step 8**: Built an **Edit Interactions** page with two sets of slicers and matching bar charts (Total Sales, Total Profit, Total Quantity Sold) to demonstrate/control how one visual's selection filters — or doesn't filter — the others (Format > Edit Interactions).
- **Step 9**: Built a detailed **Table Visual** page combining `CustomerID`, `Date`, `Order ID`, `Product ID`, `PromotionID`, `Discount Percentage`, `Discount Value`, `Net Sales`, `Price Per Unit (INR)`, `Profit`, and `Units Sold` into a single drillable table, filterable by Date, Customer Name, Product Name, and Promotion Name slicers.
- **Step 10**: Published the report to Power BI Service.

## Insights

*(Numbers below are placeholders — pull the current values straight from your published dashboard, since they'll shift as filters/slicers are applied.)*

### Sales & Profit

- Total Sales: `[₹12,20,00,000]`
- Total Profit: `[₹1,22,00,000]`
- Total Quantity Sold: `[₹7,100]`

### Products

- Top 5 products by Sales: `[Apple iPhone 14, Apple MacBook air, Sony Bravia 55" TV, Samsung Galaxy S21 and HP Pavillion Laptop]`
- Bottom 5 products by Sales: `[TupperWare Lunch Box, L'Oreal Shampoo, Nivea Body Lotion, Dove Soap Pack and Colgate Toothpaste]`
- Top 5 products by Profit: `Apple iPhone 14, Apple MacBook air, Sony Bravia 55" TV, Samsung Galaxy S21 and HP Pavillion Laptop]`
- Bottom 5 products by Profit: `[Nivea Bodylotion, Tuppware Lunch Box, Milton Thermas Flask, FabIndia Kurta and Borosil Glass Set]`

### Promotions

- Average discount by promotion category highlights which promotions are eroding margin the most vs. driving volume without heavy discounting — see the *Average Discount by Promotion Categories* chart on the Overview page.

### Customers & Geography

- Customer locations are plotted on the map visual (by `City`), making it easy to spot regional concentration of orders.

### Trend

- The *Sales Trends by Period* line chart (Net Sales by Year) shows the overall trajectory of sales — use this to flag any year-over-year decline or growth to investigate further.

## Tech Stack

- Power BI Desktop / Power BI Service
- DAX (measures for Total Sales, Total Profit, Quantity Sold)
- Star-schema data modeling (Fact + Dimension tables)
