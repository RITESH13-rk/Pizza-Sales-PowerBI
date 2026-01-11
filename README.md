# 🍕 Pizza Sales Analysis Dashboard | Power BI
An interactive Power BI dashboard analyzing pizza store sales to uncover revenue trends, customer ordering behavior, product performance, and strategic insights.


## 📌 Project Overview
This project analyzes pizza sales data using Power BI to uncover revenue trends, customer ordering behavior, and product performance.

The dashboard is designed with multiple pages to provide both high-level business insights and detailed product-level analysis.

---

## 🎯 Project Objectives
- Analyze total revenue, total orders, and average order value
- Identify best and worst-selling pizzas
- Understand customer ordering trends by day, month, category, and size
- Support business decision-making with interactive dashboards

---

## 🛠 Tools & Technologies
- Power BI  
- Microsoft Excel (data preparation)  
- SQL (logic-based analysis)  
- Data Cleaning & Transformation  
- Data Visualization

---

## 📊 Dashboard Pages & Highlights

### 🏠 Page 1: Home (Sales Overview)
- Total Revenue
- Total Orders
- Average Order Value
- Daily order trends
- Monthly order trends
- Sales contribution by:
  - Pizza category
  - Pizza size
- Interactive slicers for category and date range

📸 **Dashboard Preview – Home**

<img width="1302" height="706" alt="Pizza Sales 1pg" src="https://github.com/user-attachments/assets/8f6a93dd-acc2-4023-9fa3-f3aeed3ae524" />

---

### ⭐ Page 2: Best & Worst Sellers
- Top 5 pizzas by:
  - Revenue
  - Quantity sold
  - Total orders
- Bottom 5 pizzas by:
  - Revenue
  - Quantity sold
  - Total orders
- Product-level performance comparison

📸 **Dashboard Preview – Best & Worst Sellers**

<img width="1298" height="706" alt="Pizza Sales 2pg" src="https://github.com/user-attachments/assets/a5453fab-3727-493f-90c5-53d54d8baac1" />

---

## 🧮 SQL Equivalent
The following SQL queries were used to perform KPI calculations and trend analysis for the Pizza Sales Dashboard.
These queries helped extract business insights directly from the transactional dataset.

### A. Key Performance Indicators (KPIs)**

- **Total Revenue**

      SELECT SUM(total_price) AS Total_Revenue
      FROM pizza_sales;

- **Average Order Value**

       SELECT
          SUM(total_price) / COUNT(DISTINCT order_id) AS Average_Order_Value
       FROM pizza_sales;

- **Total Pizzas Sold**

       SELECT SUM(quantity) AS Total_Pizzas_Sold
       FROM pizza_sales;

- **Total Orders**

       SELECT COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales;

- **Average Pizzas per Order**

            SELECT
         CAST(
            CAST(SUM(quantity) AS DECIMAL(10,2)) /
            CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2))
        AS DECIMAL(10,2)) AS Average_Pizzas_Per_Order
        FROM pizza_sales;

  ## B. Daily Trend for Total Orders

        SELECT
            DATENAME(WEEKDAY, order_date) AS Order_Day,
            COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY DATENAME(WEEKDAY, order_date);

  ## C. Monthly Trend for Orders

        SELECT
            DATENAME(MONTH, order_date) AS Month_Name,
            COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY DATENAME(MONTH, order_date)
        ORDER BY Total_Orders DESC;

  ## D. Percentage of Sales by Pizza Category

        SELECT
            pizza_category,
            SUM(total_price) AS Total_Sales,
            SUM(total_price) * 100 /
                (SELECT SUM(total_price)
                FROM pizza_sales
                WHERE MONTH(order_date) = 1) AS Sales_Percentage
        FROM pizza_sales
        WHERE MONTH(order_date) = 1
        GROUP BY pizza_category;

  ## E. Percentage of Sales by Pizza Size

        SELECT
            pizza_size,
            CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Sales,
            CAST(
                SUM(total_price) * 100 /
                (SELECT SUM(total_price)
                 FROM pizza_sales
                 WHERE DATEPART(QUARTER, order_date) = 1)
            AS DECIMAL(10,2)) AS Sales_Percentage
        FROM pizza_sales
        WHERE DATEPART(QUARTER, order_date) = 1
        GROUP BY pizza_size
        ORDER BY Sales_Percentage DESC;

  ## F. Total Pizzas Sold by Category

        SELECT
            pizza_category,
            SUM(quantity) AS Total_Quantity_Sold
        FROM pizza_sales
        WHERE MONTH(order_date) = 2
        GROUP BY pizza_category
        ORDER BY Total_Quantity_Sold DESC;

## G. Top & Bottom Performing Pizzas

- **Top 5 Pizzas by Revenue**

        SELECT TOP 5
            pizza_name,
            CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Revenue DESC;

- **Top 5 Pizzas by Revenue**

        SELECT TOP 5
            pizza_name,
            CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Revenue
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Revenue DESC;

- **Top 5 Pizzas by Quantity Sold**

        SELECT TOP 5
            pizza_name,
            SUM(quantity) AS Total_Pizzas_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizzas_Sold DESC;

- **Top 5 Pizzas by Quantity Sold**

        SELECT TOP 5
            pizza_name,
            SUM(quantity) AS Total_Pizzas_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizzas_Sold DESC;

- **Bottom 5 Pizzas by Quantity Sold**

        SELECT TOP 5
            pizza_name,
            SUM(quantity) AS Total_Pizzas_Sold
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Pizzas_Sold ASC;

- **Top 5 Pizzas by Total Orders**

        SELECT TOP 5
            pizza_name,
            COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Orders DESC;

- **Bottom 5 Pizzas by Total Orders**

        SELECT TOP 5
            pizza_name,
            COUNT(DISTINCT order_id) AS Total_Orders
        FROM pizza_sales
        GROUP BY pizza_name
        ORDER BY Total_Orders ASC;

## 📁 Project Structure
- **Dataset**: Raw pizza sales data  
- **Dashboard**: Power BI `.pbix` file  
- **Images**: Dashboard screenshots  

---

## 👤 Author
**Ritesh Koushal**
