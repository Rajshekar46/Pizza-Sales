# 🍕 Plato's Pizza Sales Analysis

**Project | Business Intelligence & Analytics**  
**Tools Used:** Excel • SQL • Power BI

This project is part of a Business analysis challenge using a real-world dataset from Maven Analytics As a BI Consultant for Plato’s Pizza—a Greek-inspired pizzeria in New Jersey—I was tasked with analyzing one year of transaction data to uncover insights that can help the business optimize operations and increase revenue.

---

## 📌 Project Overview

**Client:** Plato’s Pizza, New Jersey  
**Objective:** Improve sales, understand customer behavior, and utilize seating capacity effectively using transactional data.  
**Dataset:** Pizza sales records from a full year, including pizza types, sizes, order timestamps, and pricing.

---

## 📂 Table of Contents

- [Dataset Description](https://github.com/Rajshekar46/Pizza-Sales/main/README.md#-dataset-description)
- [Business Questions](https://github.com/Rajshekar46/Pizza-Sales/edit/main/README.md#-Business-Questions)
- [Tools & Techniques](https://github.com/Rajshekar46/Pizza-Sales/edit/main/README.md#-Tools-&-Techniques)
- [Data Cleaning & Preparation](https://github.com/Rajshekar46/Pizza-Sales/edit/main/README.md#-Data-Cleaning-&-Preparation)
- [Dashboard & Visuals](https://github.com/Rajshekar46/Pizza-Sales/edit/main/README.md#-Dashboard-&-Visuals)
- [Key Insights](https://github.com/Rajshekar46/Pizza-Sales/edit/main/README.md#-Key-Insights)

---

## 📊 Dataset Description

The dataset contains **12 fields** describing every pizza order:

- `order_id`, `order_details_id`, `pizza_id`
- `pizza_name`, `pizza_type`, `pizza_ingredients`
- `quantity`, `unit_price`, `total_price`
- `order_date`, `order_time`, `pizza_size`

---

## ❓ Business Questions

1. What days and times do we tend to be busiest?
2. How many pizzas are made during peak periods?
3. What are our best and worst-selling pizzas?
4. What's the average order value?
5. How well are we utilizing our seating capacity (15 tables, 60 seats)?

---

## 🛠️ Tools & Techniques

- **Excel Version 2016:** Initial data exploration, formatting, null checks
- **Mysql Workbench 8.0.36:** Querying key metrics (sales by hour/day, top pizzas, Avergare order value)
- **Power BI 2.142.928.0:** Interactive dashboards & KPIs visualization

---

## 🧹 Data Cleaning & Preparation

- Standardized date & time formats  
- Converted price fields from string to numeric  
- Replaced abbreviated pizza sizes with full names for better clarity and consistency:

      - "S" → "Small"
      - "M" → "Medium"
      - "L" → "Large"
      - "XL" → "X Large"
      - "XXL" → "XX Large"

- Created calculated columns for peak hour categorization  

---

## 📈 Dashboard & Visuals

### 🔍 Dashboard Preview
- #### Pizza Sales Overview
![Pizza Sales Overview](https://github.com/user-attachments/assets/e3efaf06-5406-4fd4-995b-05b78a6cc9cb)

1. Total Revenue:
```sql
SELECT SUM(total_price) AS total_revenue FROM pizza_sales;
```
2. Average Order Value:
```sql
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS avg_order_value FROM pizza_sales;
```
3.	Total Pizza Sold:
```sql
SELECT SUM(quantity) AS total_pizza_sold FROM pizza_sales;
```
4.	Total Orders:
```sql
SELECT COUNT(DISTINCT order_id) AS total_order FROM pizza_sales;
```
5.	Average Pizzas Per Order:
```sql
SELECT CAST(SUM(QUANTITY)/ COUNT(DISTINCT ORDER_ID) AS DECIMAL (10,2)) AS AVG_PIZZA_PER_ORDER
 FROM pizza_sales;
```
6. % of Sales by Pizza Category
```sql
SELECT pizza_category,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales 
GROUP BY pizza_category;
```
7. % of Sales by Pizza Size
```sql
SELECT pizza_size,
    ROUND(SUM(total_price), 2) AS total_revenue,
    ROUND(SUM(total_price) * 100 / (SELECT SUM(total_price) FROM pizza_sales), 2) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
8. Pizzas Sold by Pizza Category
```sql
SELECT pizza_category, SUM(quantity) AS Total_Quantity_Sold
FROM pizza_sales
-- WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
- #### Pizza Performance  Ranking
![Pizza Sales Performance  Ranking](https://github.com/user-attachments/assets/612d1243-180c-4591-b6b1-0e73dc6f7a52)

1.	Top 5 Pizzas by Revenue
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM  pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC LIMIT 5;
```
2. Bottom 5 Pizzas by Revenue
```sql
SELECT pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC LIMIT 5;
```
3. Top 5 Pizzas by Quantity
```sql
SELECT pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
 LIMIT 5;
```
4. Top 5 Pizzas by Total Orders
```sql
SELECT pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
LIMIT 5;
```
5. Bottom 5 Pizzas by Total Orders
```sql
SELECT 
    pizza_name, 
    COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
LIMIT 5;
```

 **KPIs Tracked:**
> - Total Revenue
> - Average Order Value  
> - Total Pizza Sold
> - Total Orders
> - Average Pizza Per Order



![Pizza Sales - Dashboard-03-05-2025_page-0001](https://github.com/user-attachments/assets/da84427b-190f-410a-8541-f509cc1f7125)

---

## 💡 Key Insights

- **Fridays & Thursday** are the busiest days.
- **12PM to 1PM** & **4PM to 7PM**  is the peak window for orders.
- **Thai Chicken Pizza** is the top-selling item.
- **Classic** Categrory Pizza is the Highest Selling 

---
![Pizza Sales - Dashboard-03-05-2025_page-0002](https://github.com/user-attachments/assets/64970c2a-bf4f-4527-a495-3a68d13ebbc9)

Feel free to explore the repo and connect with me for feedback or collaboration!
### ✨ Thank You
**Raja Shekar Reddy**  
[LinkedIn](linkedin.com/in/raj-shekar-reddy) | [Email](mailto:rajshekarreddy996@gmail.com)



