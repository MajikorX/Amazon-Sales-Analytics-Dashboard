# Amazon Sales Analytics Dashboard (Power BI)

This repository contains an interactive **Amazon Sales Analytics Dashboard** built in **Microsoft Power BI**.

The report analyzes a single month of Amazon product data and focuses on:

1. **What is happening?** – Overall performance  
2. **Why is it happening?** – Key drivers such as discounts, coupons, Buy Box, and Sponsored status  
3. **How is a specific product performing?** – Product-level deep dive with images and KPIs  

---

## 🔧 Tech & Tools

- **Power BI Desktop**
- Data model based on:
  - `FactAmazon` (fact table)
  - `DimDate` (date dimension – one month, multiple days)
  - `DimCategory` (product categories)
- Custom DAX measures for:
  - Total Sales  
  - Total Units  
  - Average Selling Price  
  - Average Rating  
  - Coupon Sales Share  
  - Buy Box Sales Share  
  - Sponsored Sales Share  
  - Average Discount %  
- Image URLs (`product_image_url`) are used to render product images directly in the report.

---

## 📁 Files in this repo

- `Amazon_Sales_Dashboard.pbix` – Main Power BI report file  
- `assets/overview.png` – Screenshot of Overview page  
- `assets/drivers.png` – Screenshot of Drivers page  
- `assets/product-deep-dive.png` – Screenshot of Product Deep Dive page  
- `docs/Amazon_Sales_Dashboard_Visualization_Steps.docx` – (Optional) Documentation of build steps

---

## 📊 Data Model (Summary)

The core of the model is:

- **FactAmazon**
  - Product-level rows
  - Fields such as: product_title, product_rating, total_reviews, purchased_last_month, discounted_price, original_price, discount_percentage, has_coupon, is_sponsored, buy_box_availability, product_image_url, etc.

- **DimDate**
  - Continuous date table for one month
  - Linked to FactAmazon via `data_collected_at`/date key
  - Used for all time-based visuals (daily trend)

- **DimCategory**
  - Product category dimension
  - Linked to FactAmazon via category key

The Date table is configured for a **single month with multiple days**, to match the dataset and avoid misleading time aggregations.

---

## 🧭 Report Pages

### 1. Overview

**Goal:** Answer _“What is happening overall?”_

Key elements:

- **KPI cards**
  - Total Sales  
  - Total Units  
  - Average Selling Price  
  - Average Rating  

- **Sales by Category (Bar Chart)**
  - Shows which categories generate the most revenue.

- **Daily Sales Trend (Line Chart)**
  - Visualizes how sales evolve day by day within the month.

- **Top 10 Products by Sales (Table)**
  - Product title, category, sales, units, rating
  - Flags for:
    - Coupon (Yes/No)
    - Buy Box (Yes/No)
    - Sponsored (Yes/No)

- **Filter panel (left)**
  - Day
  - Category
  - Coupon Status (Yes/No)
  - Buy Box Status (Yes/No)
  - Sponsored Status (Yes/No)
  - “Clear Filters” button  

The design uses an **Amazon-inspired dark theme** with orange and blue accents, rounded cards, and soft shadows.

> 📷 See `assets/overview.png`

---

### 2. Drivers

**Goal:** Answer _“Why are sales behaving this way?”_

Top KPIs on this page:

- Average Discount %
- Coupon Sales Share
- Buy Box Sales Share
- Sponsored Sales Share

Main visuals:

- **Discount vs Units (Scatter)**
  - X-axis: Average Discount %
  - Y-axis: Total Units
  - Bubbles: categories, sized by Total Sales  
  - Shows whether higher discounts actually drive volume.

- **Coupon Impact by Category (Clustered Bar)**
  - Sales With Coupon vs Sales Without Coupon
  - Per category

- **Buy Box Impact by Category (Clustered Bar)**
  - Sales With Buy Box vs Sales Without Buy Box
  - Per category

- **Sponsored vs Organic Sales (Donut)**
  - Share of sales that comes from Sponsored vs Organic listings

All visuals are controlled by the same left filter panel (Day, Category, Buy Box, Coupon, Sponsored), so the user can focus on specific slices of the data.

> 📷 See `assets/drivers.png`

---

### 3. Product Deep Dive

**Goal:** Answer _“How is this specific product performing?”_

User flow:

- On the **Overview** page, the user selects a product from the **Top 10 Products by Sales** table.
- Navigation / drillthrough takes the user to **Product Deep Dive**, filtered to that product.

Layout:

- **Large product image**
  - Rendered from `product_image_url` (categorized as Image URL in Power BI)

- **KPI cards (for the selected product)**
  - Product Sales (Total Sales)
  - Units Sold (Total Units)
  - Avg Selling Price
  - Avg Rating

- **Product Details table**
  - Product title
  - Category
  - Sales, Units, Avg Price, Rating
  - Discount %
  - Coupon Status, Buy Box Status, Sponsored Status
  - Total reviews
  - Original & discounted price

This page is intentionally kept **very simple**: one image, a few KPIs, and a clean detail table, so the user can quickly understand the performance of a single product.

> 📷 See `assets/product-deep-dive.png`

---

## 🎨 Design & UX Notes

- Consistent dark theme using:
  - Background: near-black
  - Accent colors: Amazon orange (`#ff9900`) and deep blue (`#146eb4`)
- Rounded rectangles and soft shadows for a modern dashboard feel
- Fixed left filter panel with Amazon logo and a **Clear Filters** button
- Slicers synced across pages for a smooth experience

---

## 🚀 How to Use

1. Open `Amazon_Sales_Dashboard.pbix` in **Power BI Desktop**.
2. Start with the **Overview** page:
   - Explore total sales, daily trend, and Top 10 products.
3. Go to the **Drivers** page:
   - Analyze how discounts, coupons, Buy Box, and Sponsored status influence sales.
4. From the Top 10 table on the Overview page:
   - Select a product and navigate to **Product Deep Dive** to inspect that product’s metrics and attributes in detail.

---

## 📌 Possible Future Improvements

- Add month-over-month or year-over-year comparisons (requires more time periods).
- Add segmentation by region or marketplace if data is available.
- Add RLS (Row-Level Security) for user-specific views.
- Publish to Power BI Service and embed in a portfolio website.

---

## 👤 Author

- **Name:** _[إYoussef Kamal El Deen]_  
- **Role:** Data Analyst / BI Developer  
- **Tools:** Power BI, DAX, Data Modeling, Dashboard Design  

Feel free to fork, open issues, or suggest improvements!
