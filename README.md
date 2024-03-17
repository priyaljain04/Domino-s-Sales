# Domino's-Sales-Insight : Data-Analysis-using-SQL-and-TABLEAU

# OVERVIEW:
1. PROJECT NAME
2. PROBLEM STATEMENTS
3. APPROACH - PROJECT PLANNING & AIMS GRID
4. DATA ANALYSIS USING SQL
5. DATA ANALYSIS USING TABLEAU
6. NOTE


# PROJECT NAME:
Domino's SALES INSIGHT – DATA ANALYSIS USING SQL AND TABLEAU

## About Project:

    •	Performed Data Cleaning, Analysing and Visualization on Pizza company sales insights.

    •	Developed ETL mappings using SQL to extract the data from unstructured data and 
            transformed it to the staging area to conduct data cleaning.
            
    •	Developed a Tableau dashboard to perform analysis, producing quantitative visualizations 
            in Tableau to draw valuable insights based on different parameters affecting the company 
            performance and further provide business solutions.
            
## About Domino's:

    •	Domino's is a global pizza delivery corporation known for its wide variety of pizza options, efficient delivery service, and innovative ordering technology.

## Technologies Used:

    •  MySQL | SQL Serve

    •	Tableau

    •	Statistics

# PROBLEM STATEMENTS:

Analyze key indicators for pizza sales data to gain insights into business performance. Specifically, calculate the following metrics:

1. Total Revenue: The sum of the total price of all pizza orders.
2. Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.
4. Total Pizzas Sold: The sum of the quantities of all pizzas sold.
5. Total Orders: The total number of orders placed.
6. Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

# APPROACH - PROJECT PLANNING & AIMS GRID

## Purpose: What? Why? What do we want to achieve?
To unlock sales insights that are not visible before for sales team for decision support & automate them to reduced manual time spent in data gathering.

## Stake Holders: Who will be involved?
 •	Sales Director
 •	I.T. Team
 •	Customer Service Team
 •	Data & Analytics Team

## End Result: What do we want to achieve?
An automated dashboard providing quick & latest sales insights in order to support data driven decision making.

## Success Criteria: What will be our success criteria?
  •	Dashboards uncovering sales order insights with latest data available.
  •	Sales team able to take better decision & prove 10% cost savings of total spend.
  •	Sales analysts stop data gathering manually in order to save 20% of their business time & reinvest it in value added activity.


# DATA ANALYSIS USING SQL:
1. Total Revenue:
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;

2. Average Order Value :
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales

3. Total Pizzas Sold :
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales

4. Total Orders :
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales

5. Average Pizzas Per Order :
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales

6. Hourly Trend for Total Pizzas Sold :
SELECT DATEPART(HOUR, order_time) as order_hours, SUM(quantity) as total_pizzas_sold
from pizza_sales
group by DATEPART(HOUR, order_time)
order by DATEPART(HOUR, order_time)

8. Weekly Trend for Orders :
SELECT 
    DATEPART(ISO_WEEK, order_date) AS WeekNumber,
    YEAR(order_date) AS Year,
    COUNT(DISTINCT order_id) AS Total_orders
FROM 
    pizza_sales
GROUP BY 
    DATEPART(ISO_WEEK, order_date),
    YEAR(order_date)
ORDER BY 
    Year, WeekNumber;

9. % of Sales by Pizza Category :
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category

10. % of Sales by Pizza Size:
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size

11. Total Pizzas Sold by Pizza Category :
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC








# DATA ANALYSIS USING TABLEAU:


![image](https://github.com/priyaljain04/Dominos-Sales/assets/44484014/367f01b0-cf5d-493a-b28d-28457663ead2)


![image](https://github.com/priyaljain04/Dominos-Sales/assets/44484014/7929440a-7d31-451b-9b62-6c774602ff57)






# RECOMMENDATION:
Based on the dashboards Insights:
1. HOURS - Peak orders are between 12:00 PM and 1 PM and in evening from 4:00 PM to 7:00 PM. 
2. WEEKS - Significant variations in weekly orders, with highest peak during the 4th week from the month of Dec.
3. CATEGORY -Classic Category contributes to maximum Sales, Total Orders & Total Pizza Sold.
4. SIZE - Large Pizza Size contributes to maximum Sales.
