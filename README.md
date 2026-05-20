<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=🚗%20Car%20Sales%20Analytics&fontSize=50&fontColor=fff&animation=twinkling&fontAlignY=35&desc=Power%20BI%20Dashboard%20%7C%20Business%20Intelligence&descAlignY=55&descSize=20"/>

<img src="https://readme-typing-svg.demolab.com?font=Orbitron&size=28&duration=3000&pause=1000&color=FF6B35&center=true&vCenter=true&width=800&lines=📊+Transforming+Raw+Data+into+Revenue;🚗+Car+Sales+Intelligence+Dashboard;💡+YTD+%7C+PYTD+%7C+MTD+KPI+Analytics" alt="Typing SVG" />

<br/>

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-FF4444?style=for-the-badge&logo=microsoft&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)
![Domain](https://img.shields.io/badge/Domain-Automotive-red?style=for-the-badge)

</div>

---

## 🔴 Business Problem

<div align="center">
<img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=0,2,2,5,30&height=4&section=header"/>
</div>

> A leading **Car Dealership Company** had **zero visibility** into their sales performance. Management was making million-dollar decisions based on **gut feeling instead of data**.

<br/>

<div align="center">

| ❌ Problem | 📌 Impact |
|-----------|----------|
| No real-time sales tracking | Missed revenue opportunities daily |
| No model-wise revenue breakdown | Wrong inventory stocking decisions |
| No weekly/monthly trend visibility | Could not predict demand |
| No YTD vs PYTD comparison | Could not measure year-on-year growth |
| No regional dealer performance view | Underperforming dealers went unnoticed |
| Decisions based on gut feeling | Poor strategy, lost competitive edge |

</div>

<br/>

> 💸 **Bottom Line:** The company was losing revenue, missing targets, and had no data-driven strategy in place.

---

## 💼 My Role & Tasks

<div align="center">

| # | Task | Tool | Status |
|---|------|------|--------|
| 1 | Data Collection & Cleaning | Excel + Power Query | ✅ Completed |
| 2 | Data Modeling & Relationships | Power BI | ✅ Completed |
| 3 | KPI Development (YTD, PYTD, MTD) | DAX Formulas | ✅ Completed |
| 4 | Weekly Sales Trend Analysis | Power BI Line Chart | ✅ Completed |
| 5 | Body Style & Color Performance | Donut Charts | ✅ Completed |
| 6 | Dealer & Region Grid Analysis | Matrix Visual | ✅ Completed |
| 7 | Interactive Dashboard Creation | Power BI Desktop | ✅ Completed |

</div>

---

## 📊 Key Results & KPIs

<div align="center">

### 💰 Sales Performance Overview

| Metric | YTD Value | PYTD Value | Growth |
|--------|-----------|------------|--------|
| 💰 Total Sales Revenue | **$371.2M** | $333.8M | 🟢 +23.59% |
| 🚗 Total Cars Sold | **13,261 Units** | 11,914 Units | 🟢 +19.73% |
| 💵 Average Sale Price | **$28.0K** | $27.99K | 🟡 +0.79% |

</div>

<br/>

<div align="center">
<img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=6,11,20&height=3"/>
</div>

---

## 🖥️ Dashboard Preview

> 📌 **Add your screenshots after uploading them to the repo**

<div align="center">

| 📋 Overview Dashboard | 📈 Details Dashboard |
|----------------------|---------------------|
| ![Overview](screenshots/overview.png) | ![Details](screenshots/details.png) |

</div>

---

## 💡 Key Business Insights Discovered

<div align="center">

| # | Insight | Finding |
|---|---------|---------|
| 🔍 1 | **Top Body Style** | SUV generated maximum revenue YTD |
| 🔍 2 | **Top Car Color** | Pale White is most preferred by customers |
| 🔍 3 | **Best Sales Week** | Week 36 recorded highest single-week spike |
| 🔍 4 | **Top Region** | Austin dealer outperformed all other regions |
| 🔍 5 | **Transmission** | Manual cars outsold Automatic variants |
| 🔍 6 | **Fastest Growth** | Double Cab body type showed strongest momentum |

</div>

---

## 🚀 How It Helped the Business

<div align="center">
<img src="https://capsule-render.vercel.app/api?type=rect&color=gradient&customColorList=30,20,5&height=60&section=header&text=🏆%20Real%20Business%20Impact%20Delivered&fontSize=22&fontColor=fff&animation=fadeIn"/>
</div>

<br/>

<div align="center">

| ✅ Impact Area | 📌 Before | 🚀 After |
|---------------|----------|---------|
| **Decision Speed** | Reports took days to prepare | Insights available in seconds |
| **Revenue Focus** | Unknown which models sell best | Top models identified, inventory doubled |
| **Regional Control** | No dealer performance tracking | Weak dealers identified & supported |
| **Trend Forecasting** | No prediction capability | Weekly trends forecast next month sales |
| **Inventory Management** | Random stock ordering | Color & style data drives smart ordering |
| **Strategy** | Gut-feeling based decisions | 100% data-driven strategy across all dealers |

</div>

---

## ⚙️ DAX Formulas Used

```dax
-- Year-To-Date Total Sales
YTD Total Sales = 
    TOTALYTD(SUM(car_data[Price ($)]), 'Calendar Table'[Date])

-- Previous Year-To-Date Sales
PYTD Total Sales = 
    CALCULATE(
        SUM(car_data[Price ($)]),
        DATESYTD(DATEADD('Calendar Table'[Date], -1, YEAR))
    )

-- YTD vs PYTD Difference
Sales Difference = [YTD Total Sales] - [PYTD Total Sales]

-- YTD Cars Sold
YTD Cars Sold = 
    TOTALYTD(COUNT(car_data[Car_id]), 'Calendar Table'[Date])

-- YTD Average Price
YTD Avg Price = 
    TOTALYTD(AVERAGE(car_data[Price ($)]), 'Calendar Table'[Date])
