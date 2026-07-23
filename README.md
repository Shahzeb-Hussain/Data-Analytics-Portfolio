# E-Commerce Dashboard

## Problem Statement

This dashboard helps e-commerce management and operational teams better understand their sales dynamics, revenue drivers, and margin profitability. By converting fragmented enterprise operational data into unified visual insights, business leadership can quickly identify top-performing product categories, key customer segments, and regional market trends.

Through dynamic cross-filtering and key metric tracking, stakeholders can pinpoint cost bottlenecks, evaluate promotional marketing impact, and optimize discount strategies to maximize overall profitability.

Since operational margins and campaign performance vary across geographic regions, this report provides the visibility required to isolate underperforming market zones and strategically allocate resources.

---

## Steps Followed

* **Step 1:** Load raw enterprise sales, product, customer, and regional datasets into Power BI Desktop (from CSV / SQL sources).
* **Step 2:** Open Power Query Editor to inspect data quality using the "Column distribution", "Column quality", and "Column profile" options under the View tab.
* **Step 3:** Enable "Column profiling based on entire dataset" to ensure data integrity across large tables.
* **Step 4:** Address missing values and duplicate rows across key dimension tables.
* **Step 5:** Establish a relational data model (Star Schema) in the Model View, linking the core central fact table (`Sales_Fact`) to lookup dimension tables (`Product_Dim`, `Customer_Dim`, `Geography_Dim`, and `Promotion_Dim`).
* **Step 6:** Configure relationships (1-to-many) between fact and dimension tables, ensuring appropriate cross-filtering behavior.
* **Step 7:** Apply a custom color theme in the Report View under the View tab for consistent styling and legibility.
* **Step 8:** Add interactive visual filters (Slicers) for core categorical attributes: Region, Product Category, Customer Segment, and Promotion Offer.
* **Step 9:** Add Executive KPI Card visuals to the canvas to summarize key business totals: Total Revenue, Total Profit Margin, Total Units Sold, and Average Order Value (AOV).
* **Step 10:** Create bar and column charts to display profit margins and revenue distribution across Product Category and Customer Segment.
* **Step 11:** Implement dynamic Map Visuals to project regional sales distribution.
* **Step 12:** Add custom DAX measures for dynamic business aggregations and logic:

  *Total Revenue Measure:*
  ```dax
  Total Revenue = SUM(Sales_Fact[SalesAmount])
  ```
 *Total Profit Measure:*
  ```dax
  Total Profit = SUM(Sales_Fact[Profit])
  ```
 *Profit Margin Percentage Measure:*
  ```dax
  Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)
  ```
* **Step 13:** Create a Calculated Column to segment inventory into distinct price tier brackets:

  ```dax
  Price Tier = 
  IF(Product_Dim[UnitPrice] <= 50, "Low-Tier (<= $50)",
  IF(Product_Dim[UnitPrice] <= 200, "Mid-Tier ($51-$200)",
  IF(Product_Dim[UnitPrice] <= 500, "High-Tier ($201-$500)",
  "Premium (> $500)")))
  ```
Insights
Key inferences derived from the analytics model include:



Key inferences derived from the analytics model include:
## Insights

### [1] Core Sales & Margin Metrics
* **Total Revenue Generated:** $1,803,191
* **Overall Profit Margin:** 23.3%
* **Total Orders Processed:** 3,510
* High-volume categories account for the largest share of gross sales, while specific mid-tier product groups yield higher net profit margins.

### [2] Customer Segment Performance
* **Consumer Segment:** Contributes the largest revenue volume
 (51.2% of total sales).
* **Corporate / Small Business Segment:** Generates higher average order values (AOV) and stronger profit margins per transaction.

### [3] Regional & Promotional Insights
* **Regional Distribution:** Spatial analysis indicates top performance in core urban regions, while specific outlying zones exhibit lower margins due to elevated discount rates.
* **Promotional Impact:** Campaign conversion analysis demonstrates that target promotions significantly boost short-term volume, though heavy discounting requires monitoring to prevent margin erosion.
