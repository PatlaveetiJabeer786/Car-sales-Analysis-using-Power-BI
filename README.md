# 🚗 Car Sales Dashboard — Power BI

[![Header](https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=220&section=header&text=Car%20Sales%20Dashboard&fontSize=50&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Dynamic%20%26%20Interactive%20Power%20BI%20Dashboard%20%7C%20YTD%20%7C%20MTD%20%7C%20YoY&descAlignY=58&descSize=17)](https://github.com/PatlaveetiJabeer786)

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Domain](https://img.shields.io/badge/Domain-Automotive%20Sales-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed%20✅-brightgreen?style=for-the-badge)

</div>

---

## 📌 Project Overview

This is a **complete, dynamic, and interactive Car Sales Dashboard** built using Power BI for a **leading car dealership** that needed real-time visibility into its sales performance.

The dealership had years of raw sales data but **zero ability to track live KPIs, compare year-over-year growth, or identify which car models, body styles, colors, and regions were driving revenue.** Every report was manual, delayed, and outdated before it even reached management.

I designed and built a **2-page Power BI dashboard** with advanced DAX measures covering YTD, MTD, and YoY metrics — giving the sales team and leadership **instant, real-time answers** to every critical business question.

---

## 🧩 Business Problem

> *"The car dealership's management team had no live view of their sales performance. Sales data existed in Excel files, but nobody could quickly answer: How much have we sold this year? Are we ahead of last year? Which car model is our best seller? Which region is underperforming? Leadership was flying blind."*

**The dealership was struggling with:**

- 📊 **No real-time KPI tracking** — no live view of YTD, MTD, or YoY numbers
- 📉 **No year-over-year comparison** — couldn't tell if 2023 was better or worse than 2022
- 🚗 **No model/body-style breakdown** — didn't know which cars were actually selling
- 🎨 **No color or style insight** — couldn't align inventory with customer preference
- 🗺️ **No regional visibility** — which dealer regions were over/underperforming was unknown
- 🏢 **No company-level tracking** — couldn't compare performance across brands
- ⏰ **Delayed reports** — by the time data was compiled, it was already stale

---

## 🎯 My Task as the Data Analyst

I was given the raw car sales dataset and tasked with building a complete BI solution:

| Task | What I Did | Tool |
|------|-----------|------|
| **Data Import** | Loaded raw car sales CSV into Power BI | Power Query |
| **Data Cleaning** | Fixed spelling errors, standardized columns, removed nulls | Power Query |
| **Calendar Table** | Built a custom date table for time intelligence | DAX |
| **Data Modeling** | Created relationship between fact table and calendar table | Power BI |
| **KPI Measures** | Built YTD, MTD, PYTD, YoY, Avg Price, Cars Sold measures | DAX |
| **Page 1 — Overview** | Weekly trend, body style, color, region, company grid | Power BI |
| **Page 2 — Details** | Full granular table — every car sale with all attributes | Power BI |
| **Interactivity** | Slicers for Body Style, Dealer Region, Transmission, Engine | Power BI |

---

## 📊 Dashboard Preview

### 🔵 Page 1 — Sales Overview Dashboard
![Car Sales Overview](images/car_sales_overview.png)

### 🟢 Page 2 — Detailed Sales Grid
![Car Sales Details](images/car_sales_details.png)

---

## 📈 Key Performance Indicators (KPIs)

<div align="center">

| KPI Group | Metric | What It Measures |
|-----------|--------|-----------------|
| 💰 **Sales Overview** | YTD Total Sales | Total revenue generated year-to-date |
| 💰 **Sales Overview** | MTD Total Sales | Revenue generated this month so far |
| 💰 **Sales Overview** | YoY Sales Growth % | How this year compares to last year |
| 💰 **Sales Overview** | Sales Difference (YTD vs PYTD) | Absolute $ difference vs previous year |
| 💵 **Avg Price** | YTD Avg Price | Average selling price year-to-date |
| 💵 **Avg Price** | MTD Avg Price | Average selling price this month |
| 💵 **Avg Price** | YoY Avg Price Growth % | Price trend vs previous year |
| 🚗 **Cars Sold** | YTD Cars Sold | Total units sold year-to-date |
| 🚗 **Cars Sold** | MTD Cars Sold | Units sold this month |
| 🚗 **Cars Sold** | YoY Cars Sold Growth % | Volume growth vs previous year |

</div>

---

## 🔍 My Workflow — Step by Step

### ✅ Step 1 — Data Cleaning (Power Query)

- Imported raw car sales CSV into Power Query
- Fixed **spelling mistakes** in car model names and body style labels
- Standardized date formats and removed incomplete records
- Created clean, analysis-ready columns for all categorical fields

---

### ✅ Step 2 — Calendar Table & Data Model (DAX)

```dax
-- Custom Calendar Table built with DAX
Calendar Table =
ADDCOLUMNS(
    CALENDARAUTO(),
    "Year",        YEAR([Date]),
    "Month",       FORMAT([Date], "MMMM"),
    "Month Number",MONTH([Date]),
    "Week of Year",WEEKNUM([Date]),
    "Quarter",     "Q" & QUARTER([Date]),
    "Day Name",    FORMAT([Date], "dddd")
)
```

Linked the Calendar Table to the main `car_data` table via a **one-to-many relationship** on the Date field — enabling all time intelligence DAX functions.

---

### ✅ Step 3 — DAX Measures I Built

```dax
// ═══════════════════════════════════════════════════
//              SALES KPI MEASURES
// ═══════════════════════════════════════════════════

// Year-to-Date Total Sales
YTD Total Sales = TOTALYTD(SUM(car_data[Price ($)]), 'Calendar Table'[Date])

// Month-to-Date Total Sales
MTD Total Sales = TOTALMTD(SUM(car_data[Price ($)]), 'Calendar Table'[Date])

// Previous Year-to-Date Sales
PYTD Total Sales = CALCULATE(
    SUM(car_data[Price ($)]),
    SAMEPERIODLASTYEAR('Calendar Table'[Date])
)

// Sales Difference (YTD vs PYTD)
Sales Difference = [YTD Total Sales] - [PYTD Total Sales]

// Year-over-Year Sales Growth %
YoY Sales Growth = DIVIDE([Sales Difference], [PYTD Total Sales], 0)

// Dynamic colour indicator for growth vs decline
Sales Difference Colour = IF([Sales Difference] > 0, "Green", "Red")

// MTD KPI Card Label
MTD KPI = CONCATENATE(
    "MTD Total Sales : ",
    FORMAT([MTD Total Sales] / 1000000, "$0.00M")
)

// ═══════════════════════════════════════════════════
//              AVERAGE PRICE MEASURES
// ═══════════════════════════════════════════════════

Avg Price       = DIVIDE(SUM(car_data[Price ($)]), COUNT(car_data[Car_id]), 0)
YTD Avg Price   = TOTALYTD([Avg Price], 'Calendar Table'[Date])
MTD Avg Price   = TOTALMTD([Avg Price], 'Calendar Table'[Date])
PYTD Avg Price  = CALCULATE([Avg Price], SAMEPERIODLASTYEAR('Calendar Table'[Date]))
Avg Price Diff  = [YTD Avg Price] - [PYTD Avg Price]
YoY Avg Price Growth = DIVIDE([Avg Price Diff], [PYTD Avg Price], 0)

MTD Avg Price KPI = CONCATENATE(
    "MTD Avg Price : ",
    FORMAT([MTD Avg Price] / 1000, "$0.00K")
)

// ═══════════════════════════════════════════════════
//              CARS SOLD MEASURES
// ═══════════════════════════════════════════════════

YTD Cars Sold   = TOTALYTD(COUNT(car_data[Car_id]), 'Calendar Table'[Date])
MTD Cars Sold   = TOTALMTD(COUNT(car_data[Car_id]), 'Calendar Table'[Date])
PYTD Cars Sold  = CALCULATE(COUNT(car_data[Car_id]), SAMEPERIODLASTYEAR('Calendar Table'[Date]))
Cars Sold Diff  = [YTD Cars Sold] - [PYTD Cars Sold]
YoY Cars Sold Growth = DIVIDE([Cars Sold Diff], [PYTD Cars Sold], 0)

MTD Cars Sold KPI = CONCATENATE(
    "MTD Cars Sold : ",
    FORMAT([MTD Cars Sold], "0")
)

// Max Sales Point (for highlighting peak on chart)
Max Point = IF(
    MAXX(ALLSELECTED('Calendar Table'[Week]), [Total Sale]) = [Total Sale],
    MAXX(ALLSELECTED('Calendar Table'[Week]), [Total Sale]),
    BLANK()
)
```

---

### ✅ Step 4 — Dashboard Visuals I Built

**📄 Page 1 — Overview Dashboard:**

| Visual | What It Shows | Business Use |
|--------|--------------|-------------|
| 📊 **3 KPI Cards** | YTD Sales, Avg Price, Cars Sold with MTD + YoY | Instant snapshot of entire business |
| 📈 **Area Chart** | YTD Sales Weekly Trend (with peak point highlighted) | Track which weeks spike or dip |
| 🥧 **Pie Chart** | YTD Sales by Body Style (SUV, Sedan, Hatchback...) | Know which styles customers prefer |
| 🎨 **Pie Chart** | YTD Sales by Car Color (Black, Red, White...) | Align inventory with color demand |
| 🗺️ **Map Chart** | YTD Cars Sold by Dealer Region | See which regions are over/under-performing |
| 📋 **Company Grid** | YTD sales trend per car brand/company | Compare brand performance side by side |

**📄 Page 2 — Details Grid:**

| Visual | What It Shows |
|--------|--------------|
| 📋 **Full Detail Table** | Every single car sale — Model, Body Style, Color, Sales Amount, Dealer Region, Date |

**🎛️ Interactive Slicers:**
- Body Style filter
- Dealer Region filter
- Transmission type filter
- Engine type filter

---

## 💡 Key Business Insights & Outcomes

### 📅 Sales Trends
- **Weekly YTD trend** revealed clear peak sales weeks — helping plan marketing campaigns around high-traffic periods
- **YoY comparison** gave leadership the first-ever direct comparison of 2023 vs 2022 performance
- **MTD tracking** allowed mid-month course correction if sales were falling behind target

### 🚗 Product Insights
- **SUVs dominate** body style sales — inventory focus now aligned with actual demand
- **Pale White** is the most popular color across all regions — production planning updated
- **Certain models show high volume but low average price** — flagged for margin review

### 🗺️ Regional Performance
- **Map visual** identified 2 underperforming dealer regions — sales team targeted for coaching
- Top-performing regions used as benchmarks for replicating best practices elsewhere

### 🏢 Company/Brand Insights
- Company grid revealed which brands had **consistent growth vs erratic performance**
- Enabled brand-level target setting for the first time

---

## 📈 Business Value Delivered

| ❌ Before This Dashboard | ✅ After This Dashboard |
|------------------------|----------------------|
| No live KPI tracking | Real-time YTD, MTD, YoY — always current |
| No year-over-year visibility | Instant YoY growth % for every metric |
| Manual Excel reports — days to compile | One click — dashboard refreshes instantly |
| No regional breakdown | Map visual shows every dealer region's performance |
| No body style / color insight | Inventory decisions now backed by actual sales data |
| Leadership guessing on performance | Data-driven targets set by brand, region & model |
| No peak sales period visibility | Weekly trend chart shows exactly when sales spike |

---

## 📁 Project Structure

```
Car-Sales-Analysis-Project/
│
├── data/
│   └── car_sales_data.csv              # Raw car sales dataset
│
├── powerbi/
│   └── Car_Sales_Dashboard.pbix        # Full Power BI dashboard file
│
├── images/
│   ├── car_sales_overview.png          # Page 1 — Overview screenshot
│   └── car_sales_details.png           # Page 2 — Details grid screenshot
│
└── README.md
```

---

## 🚀 How to Run This Project

1. **Download Power BI Desktop** — free from [microsoft.com/powerbi](https://powerbi.microsoft.com/downloads/)

2. **Clone or download** this repository to your local machine

3. **Open** `Car_Sales_Dashboard.pbix` in Power BI Desktop

4. **Update the data source** if prompted:
   - Go to `Home → Transform Data → Data Source Settings`
   - Update the path to your local `data/car_sales_data.csv`

5. **Click Refresh** — all KPIs, charts, and visuals update automatically

6. **Explore** using the slicers: Body Style · Dealer Region · Transmission · Engine Type

---

## 🧠 Key Technical Skills Demonstrated

```
✅  Custom DAX Calendar Table     — CALENDARAUTO, ADDCOLUMNS, date hierarchy
✅  Time Intelligence DAX         — TOTALYTD, TOTALMTD, SAMEPERIODLASTYEAR
✅  KPI Measures                  — YTD, MTD, PYTD, Difference, YoY Growth %
✅  Dynamic Colour Indicators     — Green/Red conditional formatting via DAX
✅  CONCATENATE KPI Cards         — Formatted label measures for dashboard cards
✅  Max Point Highlighting        — Dynamic peak label on weekly trend chart
✅  Geographic Map Visual         — Regional sales distribution across dealer areas
✅  Multi-page Dashboard Design   — Overview + Drill-through Details grid
✅  Cross-filtering & Slicers     — 4-slicer interactive filtering system
✅  Power Query Data Cleaning     — Spelling fixes, null removal, standardization
```

---

## 🌟 Final Summary

| 🔴 Problem | 🟢 My Solution | 📈 Result |
|-----------|---------------|----------|
| No live KPI visibility | YTD · MTD · YoY DAX measures | Real-time performance tracking |
| No year-over-year comparison | SAMEPERIODLASTYEAR + Sales Difference | Instant growth/decline detection |
| No regional insight | Geographic map visual | Dealer region performance visible |
| No body style/color data | Pie charts by style & color | Inventory aligned to demand |
| No weekly trend tracking | Area chart with peak highlight | Marketing timed to sales peaks |
| Manual slow reporting | 2-page interactive dashboard | Decisions made in seconds |

---

## 👨‍💻 About Me

I'm a Data Analyst passionate about building dashboards that give businesses their first-ever real-time view of performance — replacing guesswork with clarity.

- 🔗 **LinkedIn:** [linkedin.com/in/jabeer-patlaveeti](https://linkedin.com/in/jabeer-patlaveeti)
- 📧 **Email:** jabeerpatlaveeti@gmail.com
- 🌐 **GitHub:** [github.com/PatlaveetiJabeer786](https://github.com/PatlaveetiJabeer786)

---

<div align="center">

⭐ **If this project impressed you, please give it a Star!** ⭐

</div>

[![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,50:16213e,100:0f3460&height=100&section=footer)](https://github.com/PatlaveetiJabeer786)
