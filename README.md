# Superstore Sales & Revenue Performance Dashboard (2015-2018)

An interactive **Power BI** dashboard that analyzes four years of US retail sales: revenue trends, product and category performance, regional and state-level results, customer segments and shipping behavior.

## Project Overview

The goal of this project is to turn raw order-level data into a clear, decision-ready dashboard for a retail business. It answers questions such as:

- How is revenue changing year over year?
- Which categories, products, cities and states drive the most revenue?
- Which customer segments and individual customers are the most valuable?
- How do customers prefer to receive their orders?

## Dataset

- **Source:** Superstore Sales Dataset (Kaggle)
- **Size:** 9,800 order lines, 18 columns
- **Period:** January 2015 to December 2018
- **Key fields:** Order ID, Order Date, Ship Date, Ship Mode, Customer ID, Customer Name, Segment, Region, State, City, Category, Sub-Category, Product Name, Sales

The dataset has no Profit or Quantity column, so the analysis focuses on revenue, orders and customers.

## Dashboard Pages

### Page 1: Sales & Revenue Performance
- Slicers for Year, Region and Category
- KPI cards: Total Revenue, Total Orders, Average Order Value, Total Customers (with year-over-year change)
- Revenue Trend by month (area chart)
- Sales by Sub-Category (bar chart)
- Revenue by Region (donut chart)
- Top 5 Cities by Revenue (column chart)
- Top 5 Products by Revenue with growth (table)

### Page 2: Customers & Shipping
- Revenue by State (filled map)
- Revenue by Customer Segment (donut chart)
- Orders by Ship Mode (clustered bar chart)
- Revenue by Category and Region (matrix with color scale)
- Top 10 Customers by Revenue (table)

## Data Preparation (Power Query)

- Converted `Order Date` and `Ship Date` from text (dd/mm/yyyy) to the Date type using the `en-GB` locale
- Renamed `Row ID` to `ID` and set correct data types for all columns
- Built a dedicated **Date table** (Year, Month, Month No) and related it to `Order Date` with a many-to-one, single-direction relationship

## Key DAX Measures

```DAX
Total Revenue = SUM(train[Sales])

Total Orders = DISTINCTCOUNT(train[Order ID])

Average Order Value = DIVIDE([Total Revenue], [Total Orders])

Total Customers = DISTINCTCOUNT(train[Customer ID])

Revenue PY = CALCULATE([Total Revenue], SAMEPERIODLASTYEAR('Date'[Date]))

Revenue YoY % =
IF(
    HASONEVALUE('Date'[Year]),
    DIVIDE([Total Revenue] - [Revenue PY], [Revenue PY])
)
```

Similar previous-year and growth measures exist for orders, average order value and customers. All measures are stored in a dedicated `KeyMeasures` table.

## Key Insights

- **Revenue growth:** 2018 revenue reached about **$722K**, up **20.3%** on 2017 (about $600K). 2017 grew 30.6% after a 4.3% dip in 2016.
- **Segments:** Consumer customers generate about **51%** of revenue, Corporate about 30% and Home Office about 19%.
- **Regions:** West (about 31%) and East (about 30%) lead, while South is the smallest region (about 17%).
- **Top cities:** New York City (about $252K), Los Angeles (about $173K) and Seattle (about $116K).
- **Shipping:** Standard Class is by far the most used ship mode, with 2,945 of 4,922 orders.
- **Category and region:** Technology in the East is the strongest category-region combination (about $263K).
- **Average order value** declined from about $507 in 2015 to about $435 in 2018, while order volume grew, which suggests more but smaller orders.

## Tools & Skills

- **Power BI Desktop** for modeling, visuals and report design
- **Power Query (M)** for data cleaning and type conversion
- **DAX** for measures, time intelligence and Top N analysis
- Data modeling with a star-style schema and a custom Date table
- Dashboard design: custom theme (JSON), KPI cards, conditional formatting, synced slicers

## How to Use

1. Download `Superstore_Sales_Dashboard.pbix` from this repository.
2. Open it in Power BI Desktop.
3. If prompted, point the `train` query to your local copy of `train.csv`.
4. Select a single year in the Year slicer to see year-over-year growth figures.



**Your Name**
LinkedIn: your-link-here | GitHub: your-username
