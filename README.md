# 🚗 BMW Global Sales Dashboard — Power BI

An end-to-end **Power BI dashboard** analysing BMW-style sales, inventory, discounts, and order fulfilment across **10 countries and 28 dealerships** during 2023–2024.

The project transforms transactional sales and inventory data into an interactive business intelligence report designed to help identify **sales trends, high-performing models, inventory shortages, discount patterns, order backlogs, and regional opportunities**.

> ⚠️ **Data Disclaimer:**
> This project uses a **synthetic / illustrative dataset** created for Power BI portfolio and learning purposes. It is **not official BMW data** and should not be presented as real BMW sales or business information.

---

# 📸 Dashboard Preview

### 🌍 Global Dashboard

![Global Dashboard](images/global_dashboard.png)

### 🏢 Dealership Spotlight

![Dealership Spotlight](images/dealership_spotlight.png)

### 📊 Sales Insights

![Sales Insights](images/sales_insights.png)

> Add your Power BI screenshots to the `images/` folder using the filenames above, or update the image paths to match your repository.

---

# 📑 Table of Contents

* [Overview](#-overview)
* [Key Metrics](#-key-metrics)
* [Business Questions Answered](#-business-questions-answered)
* [Key Insights](#-key-insights)
* [Data Model](#-data-model)
* [DAX Measures](#-dax-measures)
* [Data Cleaning](#-data-cleaning)
* [Repository Structure](#-repository-structure)
* [How to Run](#-how-to-run)
* [Recommendations](#-recommendations)
* [Future Improvements](#-future-improvements)
* [Skills Demonstrated](#-skills-demonstrated)
* [Author](#-author)

---

# 🚗 Overview

This project converts raw BMW-style transaction and inventory data into an interactive Power BI report.

The dashboard helps sales and operations teams understand:

* What models generate the most revenue
* Which countries and dealerships perform best
* How sales are changing over time
* Where discounts are highest
* How ICE, BEV and PHEV vehicles contribute to sales
* Where inventory shortages exist
* How much revenue is tied up in pending and in-transit orders
* Which dealerships have large order backlogs

| Category              | Details                            |
| --------------------- | ---------------------------------- |
| **Tools**             | Power BI Desktop, Power Query, DAX |
| **Dataset**           | `BMW_Sales_Dashboard_Dataset.xlsx` |
| **Period**            | January 2023 – December 2024       |
| **Sales Records**     | 3,500 transactions                 |
| **Inventory Records** | 196                                |
| **Dealerships**       | 28                                 |
| **Countries**         | 10                                 |
| **Models**            | 18                                 |
| **Report Pages**      | 3                                  |
| **Data Model**        | Star Schema                        |

---

# 📊 Key Metrics

| KPI                       |           Value |
| ------------------------- | --------------: |
| **Total Sales Revenue**   |      **$6.19B** |
| **Total Units Sold**      |      **91,865** |
| **Average Deal Size**     |      **$67.4K** |
| **YoY Unit Growth**       |        **+39%** |
| **Average Discount**      |       **3.99%** |
| **2023 Average Discount** |       **3.90%** |
| **2024 Average Discount** |       **4.06%** |
| **ICE Revenue Share**     |       **47.2%** |
| **BEV Revenue Share**     | **31% approx.** |
| **PHEV Revenue Share**    | **19% approx.** |

---

# ❓ Business Questions Answered

The dashboard was designed to answer the following business questions:

1. Which BMW-style models generate the most revenue?
2. Which countries and dealerships are the strongest performers?
3. How are sales changing year over year?
4. Which quarters show the strongest sales performance?
5. How much revenue comes from ICE, BEV and PHEV vehicles?
6. Where are discounts highest?
7. Are discounts increasing over time?
8. How much revenue is currently in **In Transit** or **Pending** orders?
9. Which dealerships have low inventory?
10. Which dealerships have large customer order backlogs?
11. Which models have the highest low-stock alerts?
12. Where should inventory be reallocated?

---

# 💡 Key Insights

|     # | Insight                                         | Evidence                                                                                      |
| ----: | ----------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **1** | **High-margin EV inventory shortage**           | 7 Series, i7, i4 and iX represent **68.1% of Low Stock alerts** (32 of 47)                    |
| **2** | **Large capital tied up in pipeline**           | **$736.7M** is tied up in In Transit and Pending orders                                       |
| **3** | **Flagship discount creep**                     | 7 Series ICE: **4.31%**, i7 BEV: **4.18%**, 3 Series PHEV: **4.16%** vs 3.99% network average |
| **4** | **ICE remains a major revenue contributor**     | **$2.92B**, representing **47.2%** of revenue                                                 |
| **5** | **Geographic concentration**                    | São Paulo Jardins and Seoul Gangnam are among the strongest dealership locations              |
| **6** | **Backlogs at major hubs**                      | Frankfurt: **70.0%**, São Paulo: **64.1%**, Toronto: **62.7%** backlog-to-stock ratio         |
| **7** | **Discount pressure**                           | Average discount increased from **3.90% to 4.06%** while units grew **39%**                   |
| **8** | **EV lineup performance differs significantly** | i4 generates **$790.8M**, while i7 and iX show slower volume conversion                       |
| **9** | **Category concentration**                      | Sedans and SUVs together contribute approximately **58.3% of revenue**                        |

> **Note:** All insights are based on the synthetic dataset created for this portfolio project.

---

# 🗂️ Data Model

The report uses a **star-schema data model** with two fact tables and two dimension tables.

### Data Model Structure

```text
                         ┌─────────────────────┐
                         │     Dim_Model       │
                         │                     │
                         │ Model_Series        │
                         │ Fuel_Type           │
                         │ Category            │
                         │ Base_MSRP_USD       │
                         └──────────┬──────────┘
                                    │
                                    │
                    ┌───────────────┴───────────────┐
                    │                               │
                    ▼                               ▼
          ┌──────────────────┐             ┌──────────────────┐
          │   FACT_SALES     │             │ FACT_INVENTORY   │
          │                  │             │                  │
          │ Transaction_ID   │             │ Available Stock  │
          │ Date             │             │ Pending Orders   │
          │ Units Sold      │             │ Stock Status     │
          │ Discount %      │             └──────────────────┘
          │ Revenue         │
          │ Order Status    │
          └────────┬─────────┘
                   │
                   │
                   ▼
          ┌─────────────────────┐
          │   Dim_Dealerships   │
          │                     │
          │ Dealership Center   │
          │ City                │
          │ Country             │
          │ Region              │
          │ Latitude            │
          │ Longitude           │
          └─────────────────────┘
```

---

## 📋 Dataset Tables

| Table                 | Type      |  Rows | Purpose                                                 |
| --------------------- | --------- | ----: | ------------------------------------------------------- |
| `BMW Fact Sales Data` | Fact      | 3,500 | Sales transactions, revenue, discounts and order status |
| `Fact_Inventory`      | Fact      |   196 | Available stock and pending customer orders             |
| `Dim_Model`           | Dimension |    18 | Model, fuel type, category and MSRP information         |
| `Dim_Dealerships`     | Dimension |    28 | Dealership, city, country, region and map coordinates   |

---

# 🧮 DAX Measures

The dashboard uses DAX measures for KPI calculations, time intelligence, pipeline analysis and inventory analysis.

```DAX
Total Sales Revenue =
SUM('BMW Fact Sales Data'[Total_Sales_Revenue_USD])
```

```DAX
Total Units Sold =
SUM('BMW Fact Sales Data'[Units_Sold])
```

```DAX
Average Deal Size =
DIVIDE(
    [Total Sales Revenue],
    [Total Units Sold]
)
```

```DAX
Units PY =
CALCULATE(
    [Total Units Sold],
    SAMEPERIODLASTYEAR('Calendar'[Date])
)
```

```DAX
YoY Growth % =
DIVIDE(
    [Total Units Sold] - [Units PY],
    [Units PY]
)
```

```DAX
Avg Discount % =
AVERAGE(
    'BMW Fact Sales Data'[Discount_Pct]
)
```

```DAX
Pipeline Revenue =
CALCULATE(
    [Total Sales Revenue],
    'BMW Fact Sales Data'[Order_Status]
        IN {"In Transit", "Pending"}
)
```

```DAX
Backlog to Stock Ratio =
DIVIDE(
    SUM(Fact_Inventory[Pending_Customer_Orders]),
    SUM(Fact_Inventory[Available_Stock_Units])
)
```

```DAX
Revenue 2024 =
CALCULATE(
    [Total Sales Revenue],
    'BMW Fact Sales Data'[Year] = 2024
)
```

---

# 🧹 Data Cleaning

The dataset was prepared and cleaned before building the Power BI report.

### Cleaning Steps

* Removed the grand-total row where `Transaction_ID = "Total"` to prevent double counting.
* Corrected data types for dates, years, prices and numerical columns.
* Converted `Date` columns to the correct Date data type.
* Converted `Year` to Whole Number.
* Converted price and revenue fields to Decimal Number.
* Checked for duplicate `Transaction_ID` values.
* Created a dedicated `Calendar` table for time-intelligence analysis.
* Connected sales and inventory data to the dealership dimension.
* Connected sales and inventory data to the model dimension.
* Validated relationships between fact and dimension tables.
* Prepared geographic fields for map-based analysis.

---

# 📁 Repository Structure

```text
BMW-Sales-Dashboard/
│
├── data/
│   └── BMW_Sales_Dashboard_Dataset.xlsx
│
├── report/
│   ├── BMW_Sales_Dashboard.pbix
│   └── bmw_sales.pdf
│
├── images/
│   ├── global_dashboard.png
│   ├── dealership_spotlight.png
│   └── sales_insights.png
│
└── README.md
```

---

# ▶️ How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/BMW-Sales-Dashboard.git
```

### 2. Open the Power BI Report

Open:

```text
report/BMW_Sales_Dashboard.pbix
```

using **Power BI Desktop**.

### 3. Update the Data Source

If Power BI cannot locate the Excel dataset:

**Home → Transform data → Data source settings → Change Source**

Select:

```text
data/BMW_Sales_Dashboard_Dataset.xlsx
```

### 4. Refresh the Report

Click:

**Home → Refresh**

The dashboard should now load the data and update the visuals.

---

# ✅ Recommendations

Based on the analysis, the following actions can be considered:

### 1. Rebalance EV Inventory

Increase inventory allocation for **7 Series, i7, i4 and iX** where low-stock alerts are concentrated.

### 2. Reduce Order Pipeline

Prioritise the approximately **$737M** tied up in **In Transit** and **Pending** orders.

### 3. Control Flagship Discounts

Review discounting strategies for premium models where discounts are already above the network average.

### 4. Reallocate Inventory

Consider moving available stock toward locations such as:

* Frankfurt
* São Paulo
* Toronto

where backlog-to-stock ratios are high.

### 5. Improve Underperforming Markets

Investigate performance gaps in locations such as:

* New York
* Miami
* Dallas

and identify opportunities to improve sales conversion.

---

# 🔮 Future Improvements

Potential improvements for future versions include:

* 2025 sales forecasting by region and model
* Discount vs. sales-volume analysis
* Automated low-stock alert dashboard
* Sales forecasting using machine learning
* Customer segmentation
* Profit-margin analysis
* Dealer performance benchmarking
* Geographic drill-down analysis
* Row-level security by region
* Automated Power BI Service refresh

---

# 🛠️ Skills Demonstrated

### Power BI

* Power BI Desktop
* Power Query
* DAX
* Data Modelling
* Star Schema
* Time Intelligence
* Interactive Dashboard Development

### Data Visualization

* KPI Cards
* Bar Charts
* Column Charts
* Line Charts
* Donut Charts
* Maps
* Slicers
* Tooltips
* Cross-filtering

### Data Analysis

* Sales Analysis
* Inventory Analysis
* Discount Analysis
* YoY Growth Analysis
* Order Pipeline Analysis
* Dealership Performance
* Geographic Analysis
* Business Insight Generation

---

# 🎯 Project Objective

The objective of this project was to demonstrate how raw sales and inventory data can be transformed into an interactive **Business Intelligence solution** using Power BI.

The project follows the complete analytical workflow:

```text
Raw Data
   ↓
Data Cleaning
   ↓
Power Query
   ↓
Data Modelling
   ↓
DAX Measures
   ↓
Data Visualization
   ↓
Business Analysis
   ↓
Actionable Insights
```

---

# 👤 Author

**Mayur Nalgirkar**

BCA Graduate | Data Science & AI/ML Enthusiast | Python | SQL | Power BI

---

# ⚠️ Disclaimer

This project is intended **only for educational, portfolio and learning purposes**.

The dataset, figures, dealership information, sales values, inventory data and business insights are **synthetic / illustrative**.

This project is **not affiliated with, sponsored by, or representative of BMW Group**, and the information should not be interpreted as official BMW sales or business data.

---

⭐ **If you find this project useful, consider giving the repository a star!**
