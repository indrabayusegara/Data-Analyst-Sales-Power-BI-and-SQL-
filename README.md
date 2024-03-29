---
# Data-Analyst-Power-BI-and-SQL-
### A.SQL (PIZZA SALES SQL QUERIES)
---
> 1. Total Revenue: 
```
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```

> 2. Average Order Value
```
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales
```

> 3. Total Pizzas Sold
```
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales
```

> 4. Total Orders
```
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales
```

> 5. Average Pizzas Per Order
```
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS
DECIMAL(10,2)) AS Avg_Pizzas_per_order FROM pizza_sales
```


### B. Daily Trend for Total Orders
---
```
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)
```

### C. Monthly Trend for Orders
---
```
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date)
```

### D. % of Sales by Pizza Category
---
```
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category
```

### E. % of Sales by Pizza Size
---
```
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size
```

### F. Total Pizzas Sold by Pizza Category
---
```
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC
```

### G. Top 5 Pizzas by Revenue
---
```
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC
```

### H. Bottom 5 Pizzas by Revenue
---
```
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
```

### I. Top 5 Pizzas by Quantity
---
```
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC
```

### J. Bottom 5 Pizzas by Quantity
---
```
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
```

### K. Top 5 Pizzas by Total Orders
---
```
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
```

### L. Borrom 5 Pizzas by Total Orders 
---
```
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC
```

### NOTE
---
#### If you want to apply the pizza_category or pizza_size filters to the above queries you can use WHERE clause. Follow some of below examples
```
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders ASC
```

### Sales analysis
---
#### The results obtained from conducting this sales analysis are as follows :
> Insight
---
##### 1. BUSIEST DAYS & TIMES
###### A. DAYS
###### | Orders are Highest on weekends, Friday/Saturday evenings
###### B. MONTHLY
###### | There are Maximum orders from month of July and January
---
##### 2. SALES PERFORMANCE
###### A. CATEGORY
###### | Classic Category contibutes to maximum sales & total orders.
###### B. SIZE
###### | Large size pizza contibutes to maximum sales
---
##### 3. BEST SELLERS
###### A. REVENUE
###### | The Thai Chicken Pizza Contributes to maximum Revenue
###### B. QUANTITY
###### | The Classic Deluxe Pizza Contributes to maximum Total Quantities
###### C. TOTAL ORDERS
###### | The Classic Deluxe Pizza Contributes to maximum Total Orders
---
##### 4. WORST SELLERS
###### A. REVENUE
###### | The Brie Carre minimum Revenue
###### B. QUANTITY
###### | The Brie Carre Pizza Contributes to minimum Total qunatity
###### C. TOTAL ORDERS
###### | The Brie Carre Pizza Contributes to minimum Total Orders
---

### Result with Power BI
#### Home Interactive Page
![Home BI](https://github.com/indrabayusegara/Data-Analyst-Power-BI-and-SQL-/assets/75928437/e7661974-b8ff-4217-bf3d-8fe8f65ea512)

#### Worst/Best Seller Page
![Worst-Best_seller](https://github.com/indrabayusegara/Data-Analyst-Power-BI-and-SQL-/assets/75928437/bd94a572-a42b-4051-a45a-1c4e82e7f788)
