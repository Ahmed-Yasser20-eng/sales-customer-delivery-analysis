# Sales, Customer & Delivery Analysis

I built this Power BI report to look at sales, product concentration, customer segments and shipping status in one place. I wanted to move from a headline number to the products, customers or regions that explain it.

**Tools:** Power BI, Power Query and DAX.

![Executive overview](https://github.com/Ahmed-Yasser20-eng/sales-customer-delivery-analysis/releases/download/v1.0.0/4-power-bi.png)

## What I worked on

I used Power Query to select, rename and type the source columns, then organized the model around order items. Customer, order and product dimensions filter the fact table. Category filters product, which makes this part of the model a snowflake rather than a pure star.

I wrote 21 DAX measures for sales before and after discount, profit, order counts, average order sales and shipping-status analysis. The report has four analytical pages: Executive Overview, Product & Category Performance, Customers & Market, and Delivery & Operations. A cover and a saved Insights & Recommendations image bring the total to six pages.

The project ZIP includes the exact extracted DAX at `analysis/measures.dax` and original Power Query at `analysis/power-query.m`.

## Model and architecture

![Actual model structure](https://github.com/Ahmed-Yasser20-eng/sales-customer-delivery-analysis/releases/download/v1.0.0/3-architecture.png)

The four active many-to-one relationships in the file are:

- FactOrderItems[Customer_Id] to DimCustomer[Customer_Id]
- FactOrderItems[Order_Id] to DimOrder[Order_Id]
- FactOrderItems[Product_Id] to DimProduct[Product_Id]
- DimProduct[Category_Id] to DimCategory[Category_Id]

Each uses single-direction filtering from the dimension side. The custom Date table is disconnected in the supplied file. The diagram shows that gap rather than implying a working date relationship.

## What the saved model supports

I checked these overall figures from the embedded tables, using the sales and profit formulas in the report:

| Metric | Checked value |
|---|---:|
| Order-item rows | 180,519 |
| Distinct orders | 65,752 |
| Sales after discount | 33,044,315.20 |
| Profit | 3,972,078.34 |
| Profit margin | 12.02% |
| Consumer share of net sales | 51.93% |
| Top three products' share of net sales | 42.05% |
| Orders with a late-delivery status | 36,048 (54.82%) |

The data covers January 2015 to January 2018. These figures describe the supplied dataset at its overall scope. I have not assigned a currency that the source has not established here.

The sales concentration is a reason to look at product mix and stock exposure, not evidence that the biggest products should automatically receive more investment. I would compare their margin and availability first. The late-status share points to a shipping investigation by region and mode. It does not prove a cause or a measured delivery improvement.

## How I would use the report

I would start with the overview, choose a product, market or customer segment to investigate, then compare its contribution with margin and shipping status. The Insights & Recommendations page records possible next steps. It is a static image, not a filter-aware calculation, and its recommendations have not been tested in a live business.

![Delivery and operations](https://github.com/Ahmed-Yasser20-eng/sales-customer-delivery-analysis/releases/download/v1.0.0/5-operations.png)

![Saved insights and recommendations](https://github.com/Ahmed-Yasser20-eng/sales-customer-delivery-analysis/releases/download/v1.0.0/6-insights.jpg)

## Known limits and next checks

- The custom Date table is disconnected. Curr_YTD, Pre_YTD and related year comparisons need a correct relationship and native Power BI testing before use.
- The measure named Sales_Margin divides sales after discount by sales before discount. It is not the profit margin. Profit Margin % is a separate measure.
- Days_Delivery is an order-to-shipping interval in this model. It should not be described as a confirmed arrival time.
- Original refresh inputs were not supplied separately. The queries refer to a local DataCoSupplyChainDataset1.csv path, so a new user cannot reproduce refresh from the PBIX alone.
- Overall totals were checked from embedded tables. Native report interactions, refresh and every filter state have not been fully tested.
- I have preserved the original PBIX and extracted code. The issues above are documented, not silently repaired.

## Open the project

1. Download `originals/Sales_Customer_Delivery.pbix` and open it in Power BI Desktop.
2. Inspect the model, measures and source settings before refreshing.
3. Supply an authorized copy of the original CSV and update the source paths in Power Query.
4. Fix and test the Date relationship in a separate working copy. Compare overall and filtered results with known subsets.
5. Keep the supplied original for reference when saving corrections.

## Download the project

[Download the complete project ZIP](https://github.com/Ahmed-Yasser20-eng/sales-customer-delivery-analysis/releases/download/v1.0.0/Sales_Customer_Delivery_Project.zip) | [View release](https://github.com/Ahmed-Yasser20-eng/sales-customer-delivery-analysis/releases/tag/v1.0.0)

Repository file uploads did not complete. The complete folder structure and unchanged original PBIX are delivered in the verified release ZIP instead. Download and extract it to browse these files. The package README uses local links within the extracted folders.

## Files

```text
originals/     Original PBIX, unchanged
analysis/      Extracted DAX and Power Query
docs/          Model diagram, relationship inventory and file hashes
images/        Authentic saved report views
```

## Data and scope

This is portfolio work, not a claim of paid client delivery or measured commercial impact. The PBIX contains embedded customer names and geographic/order fields. I confirmed that this is training data and approved public redistribution of this project. This README does not grant a license over third-party data or images.
