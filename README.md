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

The project follows a structured data analytics workflow, starting from raw retail data and progressing through data preparation, modeling, analysis, visualization, and business recommendations.

```text
Raw Data
   ↓
Power Query
   ↓
Data Cleaning & Transformation
   ↓
Data Model
   ↓
Relationships & Validation
   ↓
DAX
   ↓
KPIs & Measures
   ↓
Power BI
   ↓
Interactive Dashboards
   ↓
Business Insights
   ↓
Business Recommendations```


## Business Recommendations

Based on the verified findings from the analysis, the following recommendations can be considered:

### 1. Investigate Cancellation Drivers in North

North has the highest cancellation rate at **31.98%**.

Further analysis should focus on identifying cancellation patterns by:

- Product ID
- Date
- Geography

This can help identify specific areas associated with higher cancellation levels.

### 2. Review Cancellation Patterns by Product, Date and Geography

Cancellation performance should be reviewed across Product ID, time period, city, and zone to identify patterns that may require further investigation.

### 3. Plan Inventory and Operations Around Weekend Demand

Saturday has the highest day-of-week revenue at approximately **9.55M**.

Inventory and operational coverage can take stronger weekend demand patterns into consideration.

### 4. Perform Deeper Analysis of South

South has the highest reported revenue at approximately **18.31M**.

Further analysis at the city and Product ID levels can help understand the performance within this zone.

### 5. Improve Product Taxonomy

The Product Mapping dataset contains only one Product Group:

`Tshirts_Men`

Therefore, Product Group comparison is limited. A more detailed product classification structure would enable more meaningful product-group analysis.

### 6. Correct Geographic Lookup Issues

Unresolved and malformed geographic lookup values should be corrected before relying fully on city-tier analysis.

---

# Data Preparation

The raw retail datasets were prepared using **Power Query** before building the analytical model.

## Data Cleaning & Transformation

The main data preparation activities included:

- Correcting data types
- Checking missing values
- Checking duplicate records
- Connecting sales data with Product Mapping
- Connecting sales data with geographic lookup data
- Checking key matching between Sales `ProductId` and Product Mapping
- Checking PinCode and City relationships
- Reviewing CityTier mappings
- Creating month fields for time-based analysis
- Creating day-of-week fields for demand analysis
- Creating Net Units

### Net Units

Net Units were derived using:

`Net Units = Units - Cancelled_Units`

This measure represents the units remaining after cancelled units are deducted from total units.

## Data Validation

The following key mappings were reviewed during data preparation:

- Sales `ProductId` against Product Mapping `ProductId`
- Sales `PinCode` against PinCode-Geo `PinCode`
- PinCode-Geo `City` against CityTier `City`
- Missing CityTier values
- Unresolved geographic values

Unresolved geographic values were kept visible rather than assigning guessed values.

---

# Data Model

The cleaned datasets were connected into a **star-schema-style analytical structure**.

## Main Fact Table

### Sales Transactions

The Sales Transactions table acts as the main fact table and contains transaction-level information such as:

- `OrderDate`
- `UserId`
- `ProductId`
- `PinCode`
- `Revenue`
- `Units`
- `Cancelled_Units`

## Lookup / Dimension-Style Tables

### Product Mapping

Contains:

- `ProductId`
- `ProductGroup`

### PinCode-Geo

Contains:

- `PinCode`
- `City`
- `Zone`

### CityTier

Contains:

- `City`
- `CityTier`

---

# Main Relationships

The main relationships in the analytical model are:

### Product Relationship

`Sales Transactions[ProductId]` → `Product Mapping[ProductId]`

This relationship allows transaction data to be analyzed by product and product group.

### Geographic Relationship

`Sales Transactions[PinCode]` → `PinCode-Geo[PinCode]`

This relationship connects transaction-level data with city and zone information.

### City Tier Relationship

`PinCode-Geo[City]` → `CityTier[City]`

This relationship allows geographic performance to be analyzed by City Tier.

### Model Structure

```text
                    Product Mapping
                         |
                      ProductId
                         |
                         ↓
                Sales Transactions
                    (Fact Table)
                         |
                      PinCode
                         |
                         ↓
                    PinCode-Geo
                         |
                        City
                         |
                         ↓
                     CityTier
