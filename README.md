<p align="center">
  <img src="MavenMarket_Logo_WithCard.png" alt="Maven Market" width="420"/>
</p>

<h1 align="center">Maven Market — Power BI Sales & Returns Dashboard</h1>

<p align="center">
  A decision-ready Power BI report for a multi-national grocery chain (USA · Canada · Mexico)<br/>
  tracking revenue, profit, margins, and returns across countries, regions, stores, products, and customers.
</p>

<p align="center">
  <img alt="Power BI" src="https://img.shields.io/badge/Power%20BI-Desktop-F2C811?logo=powerbi&logoColor=black"/>
  <img alt="DAX" src="https://img.shields.io/badge/DAX-Measures-0FA678"/>
  <img alt="Data" src="https://img.shields.io/badge/Data-1997--1998-7BC043"/>
  <img alt="Status" src="https://img.shields.io/badge/Status-Complete-4CAF50"/>
</p>

---

## 📊 Overview

Maven Market is a multi-national grocery chain with stores in the **United States, Canada, and Mexico**. This project builds a full **star-schema data model** and a **4-page Power BI report** that gives the sales team a single source of truth for performance monitoring and drill-down analysis.

**Data coverage:** January 1997 – December 1998
**Fact tables:** Sales (269,722 rows) · Returns (7,088 rows)
**Dimensions:** Products · Customers · Stores · Regions · Calendar

---

## 📁 Repository Contents

| File | Description |
|---|---|
| `Maven_Market_Dashboard.pbix` | Full Power BI file — data model, DAX measures, and 4 report pages |
| `Maven_Market_Readme.docx` | Detailed README — KPI reference, filter guide, and page-by-page screenshots |
| `/screenshots` | PNG exports of each report page |

> 📌 If the `.pbix` file isn't in this repo (large file), the download link is here: **[Download .pbix](#)**

---

## 🧱 Data Model

Star schema with two fact tables and five conformed dimensions:

```
                    ┌─────────────┐
                    │  Calendar   │
                    └──────┬──────┘
                           │
   ┌───────────┐    ┌──────────────┐    ┌───────────┐
   │  Products │────│  Sales_Fact  │────│ Customers │
   └───────────┘    └──────┬───────┘    └───────────┘
                           │
                    ┌──────┴───────┐
                    │   Returns    │
                    └──────┬───────┘
                           │
                    ┌──────┴───────┐
                    │    Stores    │───────┐
                    └──────────────┘       │
                                     ┌──────┴──────┐
                                     │   Regions   │
                                     └─────────────┘
```

---

## 📐 Core KPIs

| Measure | DAX |
|---|---|
| Total Revenue | `SUMX(Sales_Fact, quantity * RELATED(product_retail_price))` |
| Total Cost | `SUMX(Sales_Fact, quantity * RELATED(product_cost))` |
| Total Profit | `[Total Revenue] - [Total Cost]` |
| Profit Margin | `DIVIDE([Total Profit], [Total Revenue])` |
| Total Orders | `COUNTROWS(Sales_Fact)` |
| Total Qty Sold | `SUM(Sales_Fact[quantity])` |
| Total Returns | `COUNTROWS(Returns)` |
| Qty Returned | `SUM(Returns[quantity])` |
| Return Rate | `DIVIDE([Qty Returned], [Total Qty Sold])` |
| Active Customers | `DISTINCTCOUNT(Sales_Fact[customer_id])` |

Full measure list with formatting notes → see `Maven_Market_Readme.docx`.

---

## 📄 Report Pages

### 1. Executive Overview
KPI cards (Revenue, Profit, Margin %, Return Rate %) · Monthly trend line · Revenue by Country map & donut · Global filters (Date, Country, Region, Store)

### 2. Products
Profit by Brand (treemap) · Product Profitability Breakdown (matrix with conditional formatting) · Top 10 Products by Return Rate

### 3. Customers
Top 10 Customers by Revenue · Revenue by Gender · Revenue by Membership Type · Customers by Home Ownership

### 4. Returns
Return Rate Trend Over Time · Return Rate by Region / Store / Brand

---

## 🎨 Visual Identity

| Color | Hex | Usage |
|---|---|---|
| 🟢 Bright Green | `#7BC043` | Primary accent |
| 🟢 Medium Green | `#4CAF50` | Secondary series |
| 🔷 Teal | `#0FA678` | Tertiary series |
| 🔷 Dark Teal | `#0D3B3E` | Cards & panels |
| ⚫ Near-Black Teal | `#0B1F1F` | Page background |
| ⚪ Off-White | `#E6F2ED` | Text on dark background |

Font: **Poppins**

---

## ⚙️ How to Use

1. Download `Maven_Market_Dashboard.pbix` and open it in **Power BI Desktop**.
2. Use the sidebar navigation (left) to move between the four report pages.
3. Filter by **Date, Country, Region, or Store** from the header — filters apply across all pages via bookmarked navigation and are preserved when switching pages.
4. Click any bar, brand, or region to cross-filter related visuals on the same page.

---

## 📝 Implementation Notes

- Calendar table built with DAX (`CALENDAR` + `ADDCOLUMNS`); Month Name sorted by Month Number for correct chronological order.
- `Stores → Regions` relationship enables country/region/store roll-ups.
- Surrogate keys and non-additive numeric fields (SKU, postal code) set to **Don't Summarize**.
- The source dataset does not include a product category/department column — **brand** was used as the grouping dimension for all brand/category analysis.
- Map visuals required enabling `File > Options and settings > Options > Global > Security > Use Map and Filled Map visuals`, followed by a full Power BI Desktop restart.

---

## 👤 Author

**Mohamed Kabil**
Graduation Project — Retail Analytics with Power BI

---

<p align="center"><i>Data as of December 1998 · Built with Power BI Desktop</i></p>
