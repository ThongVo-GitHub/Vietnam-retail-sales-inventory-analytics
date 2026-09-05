# Phase 4 — CV, GitHub and Interview Pack

## Recommended project name

**Vietnam Retail Sales & Inventory Analytics | Python, Pandas, Power BI, DAX**

Do not list SQL Server for this project unless a SQL Server layer is actually implemented.

## CV version — compact

**Vietnam Retail Sales & Inventory Analytics | Python, Pandas, Power BI, DAX**
- Built an end-to-end BI pipeline from 37 Excel sales, inventory, and master-data files; cleaned and modeled 831K+ sales rows and 1.36M+ inventory fact rows into a surrogate-key star schema.
- Developed an interactive Power BI dashboard for sales, profit, returns, brand/channel performance, and latest-snapshot inventory; validated core DAX KPIs independently with Python and documented data-quality limitations.

## CV version — detailed

**Vietnam Retail Sales & Inventory Analytics | Python, Pandas, Power BI, DAX**
- Profiled and transformed multi-file Vietnamese retail data containing 831,966 sales rows and 1,367,080 inventory fact rows, preserving return/reversal activity and auditing duplicate-like records, missing keys, zero-value transactions, and an invalid source week.
- Designed a dimensional model with FactSales, FactInventory, and six business dimensions using surrogate keys and Unknown members; avoided row multiplication from effective-dated and multi-grain master data.
- Built a Power BI dashboard with sales, cost, profit, margin, quantity, return, brand/channel, and latest-inventory analysis; configured business-appropriate slicer and visual interactions.
- Reconciled dashboard KPIs against Python calculations with a dedicated validation notebook and documented source limitations, including inventory ending in Dec 2022 while sales continue through Jul 2023.

## GitHub repository description

`End-to-end retail BI project: Python data cleaning, star-schema modeling, Power BI/DAX dashboarding, and independent KPI validation on Vietnamese sales & inventory data.`

## Suggested GitHub topics

`power-bi`, `data-analytics`, `business-intelligence`, `python`, `pandas`, `dax`, `star-schema`, `dimensional-modeling`, `data-cleaning`, `retail-analytics`

## 30-second interview explanation

> I built this project to practice the full analytics workflow rather than only creating a dashboard. I started from 37 Excel files containing sales, inventory, and master data. I profiled and cleaned the data in Python, investigated returns, duplicate-looking rows, missing keys, and inconsistent time fields, then designed separate sales and inventory fact tables with shared dimensions. I exported the star schema to Power BI Service, created DAX KPIs and an interactive dashboard, and finally built a Python validation notebook to independently reconcile the dashboard metrics. One important limitation is that inventory ends in December 2022 while sales continues to July 2023, so I explicitly keep those time contexts separate.

## 2-minute interview explanation

> The source was not a clean single CSV. It contained monthly sales and inventory snapshots plus several master-data files. The first challenge was understanding the grain and deciding what should or should not be cleaned. For example, negative quantities and prices were not deleted because their sign pattern indicated returns or reversals. Duplicate-looking sales rows were also not blindly removed because there was no transaction ID proving that they were accidental duplicates.
>
> I then validated the master data. A direct merge with product classification caused row explosion because the classification table had multiple records per product style and season. COGS and retail price were effective-dated, so I excluded those tables from the MVP rather than using an incorrect static join.
>
> For the BI model, I created FactSales and FactInventory with surrogate-key dimensions for product, customer, site, week, date, and plant. In Power BI I used one-to-many, single-direction relationships. Brand can filter both facts through DimProduct, while Channel and Sales Year intentionally affect only Sales. This prevents misleading inventory filtering.
>
> Finally, I created a validation notebook that independently recalculates the dashboard KPIs. That gave me a way to verify that DAX and model relationships were producing the expected results rather than trusting the visual output alone.

## Questions you should be ready to answer

### Why did you use a star schema?
A star schema keeps measures in fact tables and descriptive attributes in dimensions. It reduces repeated descriptive data, makes filter paths easier to understand, and gives Power BI a clean one-to-many model.

### Why are there two fact tables?
Sales and inventory have different business grains. Sales represents sales activity over time, while inventory represents stock snapshots. Combining them into one table would mix grains and create incorrect aggregations.

### Why didn't you delete negative transactions?
The negative quantity, cost, and net-price patterns were consistent with returns/reversals. Removing them would overstate net sales and net quantity. I preserved them and derived return measures separately.

### Why didn't you drop duplicate-looking rows?
There is no reliable invoice/order/transaction identifier in the source. Identical business columns can therefore represent either duplicate data or legitimate repeated activity. I flagged them instead of making an unsupported destructive assumption.

### What is the purpose of the UNKNOWN dimension member?
It preserves fact rows that cannot be matched to a dimension. This avoids losing business measures while still making unmatched data auditable.

### Why is 202153 special?
The source includes year-week 202153, but that is not a valid ISO week for the weekly date mapping used by the model. I preserved those fact rows so totals remain complete, while their weekly date is blank and therefore they are not plotted on the weekly date axis.

### Why does Year not filter Inventory?
The sales data runs through Jul 2023, but the latest inventory snapshot is Dec 2022. A Sales Year selection should not imply that a 2023 inventory snapshot exists. Inventory is intentionally shown as latest available snapshot.

### Why does Brand filter both Sales and Inventory?
Brand belongs to the shared Product dimension. DimProduct has valid one-to-many relationships to both FactSales and FactInventory, so Brand is a meaningful shared analytical dimension.

### Why doesn't Channel filter Inventory?
Distribution channel belongs to sales activity and there is no validated inventory-channel relationship in the model. Allowing it to filter inventory would imply a business relationship that the data model does not support.

### Why did you exclude Inventory Value?
The source `total_amount` semantics were not sufficiently validated and produced questionable results. I chose not to publish a KPI whose business meaning I could not defend.

### Why didn't you merge COGS/Retail Price directly?
They are effective-dated tables. A correct join depends on both product and transaction date falling between valid-from and valid-to. A static product-only merge can duplicate rows or apply the wrong price/cost.

### How did you validate the dashboard?
I created a separate Python notebook that recalculates core Sales and Inventory KPIs from the exported fact/dimension tables and compares them with the Power BI baseline using PASS/FAIL checks.

## CV integrity checklist

Before submitting:
- Keep **Power BI, DAX, Python/Pandas, star schema, data cleaning, validation**.
- Do **not** claim SQL Server for this project yet.
- Do **not** call `total_amount` inventory value.
- Do **not** imply inventory covers Jul 2023; it ends on 31 Dec 2022.
- If Phase 2 produces a FAIL, fix/reconcile it before saying all KPIs were validated.

## Recommended portfolio order

For Data Analyst / BI roles:
1. Vietnam Retail Sales & Inventory Analytics
2. Odoo ERP / HRM Business Process project
3. HCMC House Price Predictor or Vietnamese Sentiment Analysis
4. AI projects as supporting technical depth

For AI roles, keep the AI projects first and use this project to demonstrate data engineering/BI breadth.
