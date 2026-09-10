# 🍕 Domino's Sales Analysis Dashboard

A Power BI sales analytics project built to analyze Domino's pizza sales performance, product demand, revenue trends, order patterns, and peak ordering hours.

The dashboard combines multiple CSV datasets, a relational data model, calculated fields, DAX-based measures, and interactive Power BI visuals to turn raw transaction data into business insights.

---

## 📊 Project Overview

This project analyzes pizza sales data from **January 1, 2015 to September 9, 2015**.

The analysis focuses on:

- Overall revenue and order performance
- Total pizza quantity sold
- Average ticket size
- Pizza category performance
- Best-performing pizza products
- Monthly revenue trends
- Peak ordering hours
- Monthly pizza quantity distribution
- Yearly order distribution
- Category-level analysis for Classic, Supreme, Veggie, and Chicken pizzas

### Key Performance Indicators

| KPI | Value |
|---|---:|
| Total Revenue | **₹817.86K** |
| Total Orders | **21.35K** |
| Total Pizzas Sold | **49.57K** |
| Revenue per Pizza | **₹16.50** |
| Data Period | **Jan 1, 2015 – Sep 9, 2015** |

> Note: The dashboard displays rounded KPI values, such as ₹818K revenue, 49K orders, 50K pizzas, and ₹17 ticket size.

---

## 🎯 Business Objectives

The main objectives of this project are:

1. Measure overall pizza sales performance.
2. Identify high-performing pizza products.
3. Understand demand across pizza categories.
4. Analyze monthly revenue and quantity trends.
5. Identify peak ordering hours.
6. Compare Classic, Supreme, Veggie, and Chicken categories.
7. Build an interactive dashboard that can support business decision-making.

---

## 🗂️ Dataset Description

The project uses four related CSV datasets.

### 1. `order_id.csv`

Contains order-level information.

| Column | Description |
|---|---|
| `order_id` | Unique order identifier |
| `date` | Order date |
| `time` | Order time |

**Rows:** 21,350

---

### 2. `order_detail.csv`

Contains individual pizza items included in each order.

| Column | Description |
|---|---|
| `order_details_id` | Unique order-detail identifier |
| `order_id` | Related order identifier |
| `pizza_id` | Pizza identifier |
| `quantity` | Number of pizzas ordered |

**Rows:** 48,620

---

### 3. `pizza.csv`

Contains pizza-level pricing and size information.

| Column | Description |
|---|---|
| `pizza_id` | Unique pizza identifier |
| `pizza_type_id` | Related pizza type identifier |
| `size` | Pizza size |
| `price` | Price per pizza |

**Rows:** 96

---

### 4. `pizza_types.csv`

Contains pizza names, categories, and ingredients.

| Column | Description |
|---|---|
| `pizza_type_id` | Unique pizza type identifier |
| `name` | Pizza name |
| `category` | Classic, Supreme, Veggie, or Chicken |
| `ingredients` | Pizza ingredients |

**Rows:** 32

---

## 🔗 Data Model

The Power BI model connects the datasets through primary and foreign key relationships.

### Relationship Structure

```text
                 pizza_types
                      │
                      │ pizza_type_id
                      ▼
                   pizzas
                      │
                      │ pizza_id
                      ▼
                order_details
                      │
                      │ order_id
                      ▼
                    orders
```

A separate calculated date table is used for time-based analysis.

```text
Calculated Dates
      │
      └── Date / Month / Quarter / Year analysis
```

This model allows the dashboard to move from high-level sales metrics to detailed product and time analysis.

---

## 🧮 Calculations and Measures

### Revenue

Revenue is calculated from the quantity sold and the pizza price:

```text
Revenue = Quantity × Pizza Price
```

In DAX, the equivalent logic can be represented as:

```DAX
Revenue =
SUMX(
    'order_details',
    'order_details'[quantity] * RELATED('pizzas'[price])
)
```

### Total Orders

```DAX
Total Orders =
DISTINCTCOUNT('orders'[order_id])
```

### Total Pizza Quantity

```DAX
Total Pizza Quantity =
SUM('order_details'[quantity])
```

### Average Revenue per Pizza

```DAX
Average Ticket Size =
DIVIDE(
    [Revenue],
    [Total Pizza Quantity]
)
```

> In this dashboard, "Ticket Size" represents average revenue per pizza sold, not revenue per customer order.

### Date Analysis

The calculated date table supports:

- Date
- Month Name
- Month Number
- Quarter
- Week of Year
- MTD
- YTD

---

## 📈 Dashboard Pages

The Power BI report contains six main pages.

### 1. Overview

The Overview page provides a high-level view of the business.

It includes:

- Revenue
- Ticket Size
- Pizza Quantity
- Orders
- Yearly Revenue
- Monthly Revenue
- Category distribution
- Pizza size distribution
- Top pizza products
- Monthly revenue trend
- Peak ordering hours
- Monthly pizza quantity

![Overview Dashboard](assets/overview.png)

---

### 2. Classic Category

The Classic page focuses on Classic pizzas.

It includes:

- Category revenue
- Pizza size distribution
- Top Classic pizza products
- Monthly revenue trend
- Peak ordering hours
- Yearly order distribution
- Monthly quantity sold

![Classic Dashboard](assets/classic.png)

---

### 3. Supreme Category

The Supreme page provides the same analytical structure for Supreme pizzas.

![Supreme Dashboard](assets/supreme.png)

---

### 4. Veggie Category

The Veggie page analyzes sales and demand for Veggie pizzas.

![Veggie Dashboard](assets/veggie.png)

---

### 5. Chicken Category

The Chicken page analyzes the performance of Chicken pizzas.

![Chicken Dashboard](assets/chicken.png)

---

### 6. Summary

The Summary page documents the project structure, KPIs, and overall purpose of the analysis.

![Project Summary](assets/summary.png)

---

## 🔍 Key Insights

### Revenue Performance

The dataset generates approximately **₹817.86K in revenue** across 21,350 orders.

### Pizza Demand

Approximately **49,574 pizzas** were sold during the analyzed period.

### Top Revenue-Generating Pizzas

Based on the transaction data:

| Rank | Pizza | Revenue |
|---:|---|---:|
| 1 | The Thai Chicken Pizza | ₹43,434.25 |
| 2 | The Barbecue Chicken Pizza | ₹42,768.00 |
| 3 | The California Chicken Pizza | ₹41,409.50 |
| 4 | The Classic Deluxe Pizza | ₹38,180.50 |
| 5 | The Spicy Italian Pizza | ₹34,831.25 |

### Monthly Revenue

The highest monthly revenue in the available data occurs in **July**, at approximately **₹72.56K**.

The lowest monthly revenue occurs in **October**, at approximately **₹64.03K**.

### Ordering Hours

Orders are concentrated around the main lunch and evening periods.

The strongest order activity appears around:

- **12 PM – 1 PM**
- **5 PM – 7 PM**

This indicates that staffing and preparation capacity are particularly important during lunch and evening peaks.

---

## 📊 Visualizations Used

The dashboard uses several Power BI visual types:

- KPI Cards
- Donut Charts
- Table / Matrix-style visuals
- Line Charts
- Column Charts
- Slicers / Buttons
- Interactive category navigation

The dashboard also uses category navigation for:

- Classic
- Supreme
- Veggie
- Chicken
- Overview
- Summary

---

## 🧹 Data Preparation

The project follows a basic analytics workflow:

```text
Raw CSV Files
     ↓
Data Import
     ↓
Data Cleaning
     ↓
Data Transformation
     ↓
Data Modeling
     ↓
DAX Measures
     ↓
Interactive Visualizations
     ↓
Business Insights
```

Typical preparation tasks include:

- Checking column data types
- Converting dates into proper date fields
- Extracting hour information from order times
- Creating month and quarter attributes
- Connecting tables using IDs
- Creating revenue calculations
- Validating totals and relationships

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Dashboard development and visualization |
| **Power Query** | Data cleaning and transformation |
| **DAX** | Measures and calculated analysis |
| **CSV** | Source datasets |
| **Data Modeling** | Table relationships and analytical structure |

---

## 💡 Business Recommendations

Based on the analysis, a pizza business could:

1. **Prepare for peak hours**  
   Increase staff and preparation capacity during lunch and evening demand peaks.

2. **Promote high-performing products**  
   Use top-revenue pizzas in promotions, bundles, and recommendation sections.

3. **Monitor monthly performance**  
   Investigate the causes of lower-revenue months and test targeted offers.

4. **Use category-level analysis**  
   Track Classic, Supreme, Veggie, and Chicken categories separately to understand customer preferences.

5. **Optimize inventory**  
   Use product demand patterns to improve ingredient planning and reduce waste.

---

## 📁 Project Structure

Recommended GitHub repository structure:

```text
Dominos-Sales-Analysis/
│
├── README.md
│
├── Dominos.pbix
│
├── data/
│   ├── order_id.csv
│   ├── order_detail.csv
│   ├── pizza.csv
│   └── pizza_types.csv
│
└── assets/
    ├── data-model.png
    ├── overview.png
    ├── classic.png
    ├── supreme.png
    ├── veggie.png
    ├── chicken.png
    └── summary.png
```

---

## 🚀 How to Use the Project

### Option 1: View the Dashboard

Open the `.pbix` file using **Microsoft Power BI Desktop**.

### Option 2: Explore the Data

Open the CSV files in:

- Microsoft Excel
- Power BI
- Python / Pandas
- SQL

### Option 3: Rebuild the Dashboard

1. Import the four CSV files into Power BI.
2. Create the relationships shown in the data model.
3. Create a date table.
4. Add revenue and quantity measures.
5. Build KPI cards.
6. Create category and product visuals.
7. Add monthly and hourly analysis.
8. Add slicers/navigation buttons.
9. Format the report for presentation.

---

## 📸 Dashboard Preview

The report includes an interactive blue-themed dashboard with category navigation, KPI cards, product rankings, monthly trends, peak-hour analysis, and category-specific pages.

---

## 👨‍💻 Project Skills Demonstrated

This project demonstrates practical skills in:

- Power BI
- Power Query
- DAX
- Data Cleaning
- Data Transformation
- Data Modeling
- Relationship Management
- KPI Development
- Data Visualization
- Exploratory Data Analysis
- Business Insight Generation
- Dashboard Design

---

## 📌 Project Type

**Data Analytics / Business Intelligence Project**

**Domain:** Food & Restaurant Sales Analytics

**Primary Tool:** Microsoft Power BI

---

## 📄 Disclaimer

This project is created for learning and portfolio purposes. The analysis is based on the provided pizza sales dataset and is not an official Domino's business report.

---

## ⭐ If you found this project useful

Feel free to explore the dashboard, review the data model, and use the project as a reference for learning Power BI and business analytics.
