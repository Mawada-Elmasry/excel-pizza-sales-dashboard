# 🍕 Pizza Sales Dashboard — Excel PivotTables & PivotCharts

An interactive sales dashboard built in **Microsoft Excel** from a year of pizza orders (2015).
The raw order data is structured as an Excel Table and given a calculated **Sales** column. **PivotTables** summarise it, and **PivotCharts**, **slicers** and a **timeline** make up a single-page dashboard that shows what sells, when, and in which sizes.

<img width="1557" height="691" alt="pizza dashboard" src="https://github.com/user-attachments/assets/b918816b-e2fa-4eba-b7fd-88944ee8138f" />

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Tools & Features](#-tools--features)
- [Dataset](#-dataset)
- [Project Workflow](#-project-workflow)
- [Data Preparation](#-data-preparation)
- [Pivot Tables](#-pivot-tables)
- [Dashboard](#-dashboard)
- [Key Insights](#-key-insights)
- [Repository Structure](#-repository-structure)
- [How to Use](#-how-to-use)
- [Notes & Limitations](#-notes--limitations)
- [Skills Demonstrated](#-skills-demonstrated)
- [Acknowledgements](#-acknowledgements)

---

## 🎯 Project Overview

**Goal:** turn a flat list of pizza orders into a dashboard that answers:

- How much did we sell, and how many pizzas?
- Which **categories** and **sizes** bring in the most revenue?
- Which **months** and **days of the week** are busiest?
- Which pizzas are the **best sellers**, and which are the **weakest**?

**Headline numbers (2015):**

| KPI | Value |
|---|---|
| 💰 Total Sales | **$8,436** |
| 🍕 Total Quantity | **511** pizzas |
| 🧾 Total Orders | **499** |
| 🛒 Average Order Value | **$16.91** |
| 👥 Total Customers | **499** (see [Notes](#-notes--limitations)) |

---

## 🛠 Tools & Features

| Tool / Feature | Used for |
|---|---|
| **Excel Table** (`Table1`) | Structured, auto-expanding source range for all pivots |
| **Calculated column** | `Sales = unit_price × quantity` |
| **PivotTables** | 10 summaries behind the KPIs and charts |
| **Value Filters (Top 10)** | Top 5 and Bottom 5 pizzas by sales |
| **Show Values As → % of Grand Total** | Sales share by category and by size |
| **Date grouping** | Order dates grouped into months |
| **PivotCharts** | Doughnut, line, bar, column and pie charts |
| **Slicers** | Filter by `pizza_size` and `pizza_category` |
| **Timeline** | Filter by `order_date` (months of 2015) |

---

## 🗂 Dataset

**499 orders × 13 columns**, covering **1 Jan 2015 – 29 Dec 2015**.
Column headers are **bilingual (English + Arabic)**, so the workbook works for both audiences.

| Column | Arabic header | Description |
|---|---|---|
| `order_id` | رقم الطلب | Unique order number (1–499) |
| `pizza_id` | رقم البيتزا | Pizza code incl. size, e.g. `classic_dlx_m` |
| `Customer Name` | اسم العميل | Customer who placed the order |
| `quantity` | الكمية | Pizzas in the order (1–4) |
| `order_date` | تاريخ الطلب | Order date |
| `WeekDay` | — | Day name from `order_date` (Monday … Sunday) |
| `order_time` | وقت الطلب | Order time |
| `unit_price` | سعر الوحدة | Price of one pizza ($9.75 – $25.50) |
| `Sales` | — | **Calculated:** `unit_price × quantity` |
| `pizza_size` | حجم البيتزا | S, M, L, XL |
| `pizza_category` | فئة البيتزا | Chicken, Classic, Supreme, Veggie |
| `pizza_ingredients` | مكونات البيتزا | Ingredient list |
| `pizza_name` | اسم البيتزا | Pizza name (32 different pizzas) |

The workbook also has a **Definition** sheet that explains, in Arabic, what a PivotTable is, what it is used for, and why it helps.

---

## 🔄 Project Workflow

```
Raw order data
     │
     ▼
Excel Table (Table1) ──► add WeekDay + calculated Sales column
     │
     ▼
PivotTables ──► KPIs, % of total, monthly/weekly counts, Top/Bottom 5
     │
     ▼
PivotCharts + Slicers + Timeline ──► Interactive dashboard
```

---

## 🧹 Data Preparation

1. **Converted the data range into an Excel Table** (`Table1`, `A1:M500`), so new rows are picked up automatically when the pivots are refreshed.
2. **Added a `WeekDay` column** with the day name of each order date, for the weekly distribution chart.
3. **Added a calculated `Sales` column** using structured references:

   ```excel
   =Table1[[#This Row],[unit_price (سعر الوحدة)]] * Table1[[#This Row],[quantity (الكمية)]]
   ```

4. **Checked data quality:** no blank cells in any of the 13 columns, `order_id` is unique (1–499), and every `WeekDay` value matches its `order_date`.
5. **Grouped `order_date` by month** in the PivotTables for the monthly trend.

---

## 📋 Pivot Tables

All PivotTables share one pivot cache built on `Table1`:

![Pivot Tables](images/pivot_tables.png)

| PivotTable | Rows | Values | Setting |
|---|---|---|---|
| Sales by Category | `pizza_category` | Sum of Sales | % of Grand Total |
| Sales by Size | `pizza_size` | Sum of Sales | % of Grand Total |
| Monthly Orders | `order_date` (grouped by month) | Count of `order_id` | — |
| Weekly Orders | `WeekDay` | Count of `order_id` | — |
| Top 5 Pizzas | `pizza_name` | Sum of Sales | Value filter: **Top 5** |
| Bottom 5 Pizzas | `pizza_name` | Sum of Sales | Value filter: **Bottom 5** |
| KPI – Total Sales | — | Sum of Sales | — |
| KPI – Total Quantity | — | Sum of `quantity` | — |
| KPI – Total Orders | — | Count of `order_id` | — |
| KPI – Total Customers | — | Count of `Customer Name` | — |

---

## 📈 Dashboard

<img width="1557" height="691" alt="pizza dashboard" src="https://github.com/user-attachments/assets/2154aa42-45c4-4ca5-b3b7-8aa6a15242b8" />


**KPI header:** Total Sales · Total Quantity · Total Orders · Total Customers

| Visual | Chart type | Answers |
|---|---|---|
| Total Sales per Category | Doughnut | Which category earns the biggest share? |
| Monthly Order Volume Peaks | Line | Which months are busiest? |
| Top 5 Best-Selling Pizzas | Bar | Which pizzas bring in the most revenue? |
| Sales Distribution by Pizza Size | Pie | Which sizes customers buy most? |
| Weekly Order Distribution | Column | Which days of the week are busiest? |
| Bottom 5 Least-Selling Pizzas | Bar | Which pizzas underperform? |

**Interactive filters** (connected to every PivotTable):

- 📏 **pizza_size** slicer — S, M, L, XL
- 🏷 **pizza_category** slicer — Chicken, Classic, Supreme, Veggie
- 📅 **order_date** timeline — filter by month of 2015

The busiest day (**Friday**) is highlighted in gold, and the bar charts use colour gradients so the top and bottom performers stand out.

---

## 💡 Key Insights

### By Category

| Category | Sales | Share | Orders |
|---|---:|---:|---:|
| **Veggie** | **$2,365.25** | **28.04%** | 134 |
| Classic | $2,274.75 | 26.96% | **149** |
| Supreme | $2,052.05 | 24.32% | 122 |
| Chicken | $1,744.00 | 20.67% | 94 |

- **Veggie** brings in the most revenue, even though **Classic** has more orders, so Veggie pizzas sell at higher prices on average.
- **Chicken** is the smallest category on both sales and orders.

### By Size

| Size | Share of Sales | Orders |
|---|---:|---:|
| **L** | **47%** | 197 |
| M | 27% | 138 |
| S | 22% | 153 |
| XL | 3% | 11 |

- **Large** pizzas bring in almost **half** of all revenue.
- **XL** is barely ordered (11 orders, 3% of sales). It could be promoted or reconsidered.

### By Month

| Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 33 | 32 | **30** | 34 | 47 | **54** | 47 | 51 | 47 | 44 | 34 | 46 |

- Orders climb sharply from **April to June**, peaking in **June (54 orders)**.
- **March** is the quietest month (30 orders).
- The second half of the year (269 orders) is busier than the first half (230 orders).

### By Day of Week

| Mon | Tue | Wed | Thu | Fri | Sat | Sun |
|---:|---:|---:|---:|---:|---:|---:|
| 66 | 72 | **48** | 73 | **91** | 77 | 72 |

- **Friday** is the busiest day (91 orders), followed by Saturday (77).
- **Wednesday** is the slowest day (48 orders), which makes it a good day for mid-week offers.

### Best & Worst Sellers (by Sales)

| 🏆 Top 5 | Sales | | 🔻 Bottom 5 | Sales |
|---|---:|---|---|---:|
| The Classic Deluxe Pizza | $459.00 | | The Brie Carre Pizza | $47.30 |
| The Four Cheese Pizza | $432.75 | | The Spinach Supreme Pizza | $74.75 |
| The Thai Chicken Pizza | $428.50 | | The Chicken Alfredo Pizza | $87.75 |
| The Greek Pizza | $402.00 | | The Pepperoni, Mushroom, and Peppers Pizza | $122.50 |
| The Barbecue Chicken Pizza | $383.75 | | The Calabrese Pizza | $166.50 |

- **The Classic Deluxe Pizza** is the top seller, at almost **10×** the revenue of the weakest pizza.
- **The Brie Carre Pizza** is far behind every other pizza and is the first candidate for a menu review.

---

## 📁 Repository Structure

```
excel-pizza-sales-dashboard/
│
├── README.md
├── Pizza_Sales_Dashboard.xlsx      # Data, PivotTables and dashboard
│
└── images/
    ├── pizza_sales_dashboard.png
    └── pivot_tables.png
```

**Workbook sheets:**

| Sheet | Contents |
|---|---|
| `Defintion` | Arabic explanation of PivotTables: what they are, their uses and benefits |
| `Data` | The order data as `Table1` |
| `Pivot Table` | All PivotTables behind the dashboard |
| `pizza sales dashboard` | The interactive dashboard |

---

## ▶️ How to Use

1. **Clone or download** this repository.
   ```bash
   git clone https://github.com/Mawada-Elmasry/excel-pizza-sales-dashboard.git
   ```
2. Open **`Pizza_Sales_Dashboard.xlsx`** in **Excel 2013 or later** (timelines need 2013+; Microsoft 365 recommended).
3. Go to the **`pizza sales dashboard`** sheet.
4. Use the **pizza_size** and **pizza_category** slicers and the **order_date** timeline to filter every chart at once.
5. After adding new rows to `Table1`, click **Data → Refresh All**.

---

## ⚠️ Notes & Limitations

- **Total Customers** uses *Count of Customer Name*, which counts one entry per order (**499**). The data has **466 unique customer names**, because some customers ordered more than once. To show unique customers, load the table into the Data Model and use **Distinct Count**.
- The Top 5 / Bottom 5 rankings are based on **sales value**, not quantity sold.
- The dataset is a **sample of 499 orders** from 2015, so treat the insights as patterns rather than full-year business results.

---

## 🧠 Skills Demonstrated

- Structuring data as an **Excel Table** with **structured-reference** formulas
- Building **PivotTables** with **% of Grand Total**, **date grouping** and **Top/Bottom N** filters
- Designing **PivotCharts** that fit together as one dashboard
- Connecting **slicers** and a **timeline** to multiple PivotTables
- Working with a **bilingual (English/Arabic)** dataset
- Turning numbers into clear **business insights**

---

⭐ If you found this project useful, consider giving the repository a star!
