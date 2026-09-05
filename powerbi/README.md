# Power BI Report

This folder contains the exported Power BI report:

`Vietnam_Retail_Sales_Inventory_Analytics.pbix`

The report was created in Power BI Service and downloaded as a PBIX copy.

## Semantic model relationships

Use active, single-direction, one-to-many relationships from dimensions to facts:

- DimProduct[product_key] -> FactSales[product_key]
- DimProduct[product_key] -> FactInventory[product_key]
- DimCustomer[customer_key] -> FactSales[customer_key]
- DimSite[site_key] -> FactSales[site_key]
- DimWeek[week_key] -> FactSales[week_key]
- DimDate[date_key] -> FactInventory[date_key]
- DimPlant[plant_key] -> FactInventory[plant_key]

## Interaction design

- Brand filters both Sales and Inventory through DimProduct.
- Channel filters Sales only.
- Sales Year filters Sales only.
- Sales visual selections are intentionally prevented from filtering Inventory where the relationship would be misleading.
- Weekly trend uses the valid week-start date from DimWeek, so source week `202153` remains in KPI totals but is not plotted on the weekly date axis.
