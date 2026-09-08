# Retail Analytics Dashboard | Power BI

> An end-to-end Power BI project focused on retail sales, revenue, cancellations, customer activity, product performance, and geographic analysis.
---
## Overview

This project transforms fragmented retail transaction and lookup data into an interactive Power BI analytics solution.
The analysis focuses on:
- Revenue and sales performance
- Gross vs. net units
- Cancellation patterns
- Customer activity
- Product-level performance
- Geographic performance
- Demand patterns by day and month

The project covers the complete analytics workflow from raw data preparation and transformation to data modeling, DAX measures, interactive dashboards, business insights, and recommendations.

---
## Tech Stack

| Tool | Purpose |
|---|---|
| **Power BI** | Dashboard development and visualization |
| **Power Query** | Data cleaning and transformation |
| **DAX** | Measures and KPI calculations |
| **Excel / CSV** | Source data |

---
## Data Sources

The project combines four source files:
| Dataset | File | Description |
|---|---|---|
| Sales Transactions | `Mod3_Raw_Sales_v0.1.xlsx` | Transaction-level sales data |
| Product Mapping | `Mod3_Raw_ProductMap_v0.1.csv` | Product ID and Product Group mapping |
| City Tier | `Mod3_Raw_CityTier_v0.1.csv` | City-level segmentation |
| PinCode Geography | `Mod3_Raw_PinCodeGeo_v0.1.xlsx` | PinCode, City, and Zone mapping |

### Sales Data
The main transaction dataset contains **83,374 transactions** covering **01 November 2017 to 20 January 2018**.

Key fields include:

`OrderDate` · `UserId` · `ProductId` · `PinCode` · `Revenue` · `Units` · `Cancelled_Units`

---
## Project Workflow

```text
Raw Data
    ↓
Power Query
(Data Cleaning & Transformation)
    ↓
Data Model
(Relationships & Validation)
    ↓
DAX
(KPIs & Measures)
    ↓
Power BI
(Interactive Dashboards)
    ↓
Business Insights
    ↓
Recommendations

Data Preparation

Power Query was used to prepare and validate the datasets before analysis.

Key Steps
Corrected data types
Cleaned and transformed source data
Connected sales data with product and geographic lookup tables
Created month and day-of-week fields
Checked missing values and duplicates
Validated Product ID key matching
Validated PinCode relationships
Reviewed city and CityTier mappings
Kept unresolved geographic values visible rather than assigning assumptions
Net Units

Net Units were calculated to account for cancelled units:
   Net Units = Units − Cancelled Units
