# Global E-commerce Sales & Customer Analytics
**Tools:** SQL | BigQuery | Excel | Data Visualization | GitHub
## Project Overview
This project analyzes e-commerce sales data to understand revenue, profitability, customer behavior, product performance, and geographic performance.
The goal is to use data analysis to identify business trends and opportunities that could support better commercial decision-making.

## Executive Summary

The analysis shows that Furniture is the strongest product category, generating the highest sales and total profit. Consumer customers are the most valuable customer segment, leading both sales and profitability.

Credit Card is the most commonly used payment method by sales, followed by PayPal. From a geographic perspective, Europe and North America are the strongest regions for profitability.

Sales also fluctuate across months, indicating opportunities to improve seasonal planning, marketing campaigns, inventory management, and promotional strategies.

### Key Findings

- *Furniture* generated the highest sales at approximately *$2.26M* and the highest total profit at approximately *$7.60M*.
- *Technology* ranked second in both sales and profit.
- *Consumer* customers generated the highest sales at approximately *$22.41M* and the highest profit at approximately *$7.95M*.
- *Credit Card* generated the highest sales among payment methods at approximately *$16.42M, followed by PayPal at *$12.34M**.
- *Europe* generated the highest regional profit at approximately *$4.38M, followed closely by North America at *$4.20M**.
- The average order value was approximately *$20,920.33*.
- Monthly sales varied throughout the three-year period, highlighting potential seasonal trends and opportunities for improved planning.

## Dashboard

The dashboard highlights key trends and performance across sales, products, profitability, and regions.

### Monthly Sales Trend
Shows monthly sales fluctuations from 2023–2025.

![Monthly Sales Trend](dashboard/total_sales%20by%20month.png)

### Sales by Product Category
Compares total sales across product categories.

![Sales by Product Category](dashboard/total_sales%20by%20Product_Category.png)

### Profit by Region
Shows which regions generate the highest total profit.

![Profit by Region](dashboard/total_profit%20by%20Region.png)

### Top Products by Sales
Highlights the highest-selling products.

![Top Products by Sales](dashboard/total_sales%20by%20product_name.png)


### Lowest-Profit Products
Identifies products with the weakest profitability and potential areas for improvement.

![Lowest-Profit Products](dashboard/total_profit%20by%20product_name.png)

## Business Problem
The company wants to understand:
- How sales and profit are performing over time
- Which products and categories generate the most revenue
- Which customer segments are most valuable
- Which regions perform best
- Where there may be opportunities to improve profitability
## Business Questions
### Sales Performance
- What is the total sales revenue?
- How does revenue change over time?
- Which products and categories generate the most sales?
### Profitability
- What is total profit?
- Which products and categories generate the most profit?
- Which areas have strong sales but weak profitability?
### Customer Analysis
- Which customer segments generate the most revenue?
- Which customer segments generate the most profit?
- What is the average order value?
### Geographic Analysis
- Which countries generate the most revenue?
- Which regions are most profitable?
- Are there geographic markets that deserve further attention?
## Dataset
The dataset contains e-commerce transaction information including:
- Order ID
- Order date
- Customer name
- Customer segment
- Country
- Region
- Product category
- Product name
- Quantity
- Unit price
- Discount percentage
- Total sales
- Shipping cost
- Profit
- Payment method
The dataset contains 2,000 transactions covering 2023–2025.
## Tools
- SQL
- Excel
- Data visualisation
- GitHub
## Project Workflow
1. Data quality assessment
2. Data cleaning and validation
3. Exploratory analysis
4. SQL analysis
5. Business insights
6. Dashboard development
7. Recommendations
## Project Status
✅ Completed core SQL analysis covering sales, profitability, customers, payment methods and geographic performance.


## SQL Analysis

### 1. Sales by Product Category

***Business Question:***
Which product categories generate the most sales?

**SQL Query:**
```sql
select Product_Category,
       sum(Total_Sales) as total_sales
from `ecommerce-sales-portfolio.ecommerce_sales.sales`
group by Product_Category
order by total_sales desc;
```
*Results:*

| Product Category | Total Sales |
|---|---:|
| Furniture | 2,261,386.3 |
| Technology | 1,189,778.8 |
| Clothing & Accessories | 565,432.5 |
| Office Supplies | 167,468.8 |

*Key Insight:*  

Furniture generated the highest total sales at 2,261,386.3, while Office Supplies generated the lowest at 167,468.8.

*Business Relevance:*  

This analysis helps identify which product categories contribute most to revenue and can support marketing prioritization and resource allocation.

### 2. Profit by Product Category

**Business Question:**  
Which product categories generate the most profit?

**SQL Query:**

```sql
SELECT
  Product_Category,
  SUM(Profit) AS total_profit
FROM `ecommerce-sales-portfolio.ecommerce_sales.sales`
GROUP BY Product_Category
ORDER BY total_profit DESC;
```
*Results:*

| Product Category | Total Profit |
|---|---:|
| Furniture | 7,599,018 |
| Technology | 4,334,601 |
| Clothing & Accessories | 2,352,634 |
| Office Supplies | 307,652 |

*Key Insight:*

Furniture generated the highest total profit at 7,599,018, followed by Technology at 4,334,601. Office Supplies generated the lowest total profit at 307,652.

*Business Relevance:*

Furniture is the strongest-performing category based on both total sales and total profit. This suggests that it may be an important category for marketing focus and operational planning. Office Supplies may require further investigation to understand its relatively low contribution.

### 3. Monthly Sales Trend

**Business Question:**
  
How do sales change over time?

**SQL Analysis:**

```sql
select
      extract (year from order_date) as year, 
      extract (month from order_date) as month,
      sum(total_sales) as total_sales
from `ecommerce-sales-portfolio.ecommerce_sales.sales`
group by year,month
order by year,month;
```
*Result:*

The query returned 36 monthly records, covering the available three-year period.

*Key Finding:*

The analysis shows that monthly sales fluctuate throughout the year, with noticeable peaks and lower-performing months. For example, in 2023, February generated approximately $1.61M in sales, while May generated approximately $0.77M. October was another strong month with approximately $1.68M in sales.

*Business Insight:*

Sales performance is not consistent across all months. Identifying high- and low-performing periods can help the business plan inventory, marketing campaigns, and promotional activities more effectively.

### 4. Top Products by Sales

**Business Question:**
Which products generate the most sales?

**SQL Analysis:**
```sql
select
  product_name,
  product_category,
  sum(total_sales) as total_sales
from `ecommerce-sales-portfolio.ecommerce_sales.sales`
group by Product_Name, Product_Category
order by total_sales desc
limit 10;
```
*Key Finding:*

The Standing Desk Converter generated the highest total sales at approximately $4.50M, followed by the Ergonomic Office Chair at approximately $4.20M. Furniture products dominated the top of the ranking, with the first four positions occupied by Furniture products.

*Business Insight:*

The results reinforce the strong performance of the Furniture category. Products such as desks and office chairs appear to be major revenue drivers and could be prioritized for inventory planning, marketing, and promotional strategies.

### 5. Lowest Profit Products

**Business Question:**
Which products generate the least profit?

**SQL Analysis:**
```sql
select
  product_name,
  product_category,
  sum(profit) as total_profit
from `ecommerce-sales-portfolio.ecommerce_sales.sales`
group by Product_Name, Product_Category
order by total_profit asc
limit 10;
```
*Results:*

The 10 lowest-profit products were identified, with Paper Clips Box 500pc ranking lowest at -5,529 profit.

*Key Insight:*

Paper Clips Box 500pc generated a negative profit of -5,529, making it the only loss-making product among the results shown.

*Business Relevance:*

This product should be investigated for pricing, discounting, or cost issues. Reviewing its profitability could help reduce losses and improve overall margins.

### 6. Sales by Payment Method

**Business Question:**

Which payment methods generate the most sales?

*Results:*

| Payment Method | Total Sales |
|---|---:|
|Credit Card |16,417,070|
|PayPal|12,342,573|
|Cash on Delivery|6,719,273|
|Bank Transfer|6,361,748|

*Key Insight:*

Credit Card generates the highest sales at 16.4M, followed by PayPal at 12.3M.

*Business Relevance:*

Customers strongly favor digital payment methods, suggesting the business should prioritize and optimize Credit Card and PayPal payment experiences.

### 7. Sales by Customer Segment

**Business question:**
Which customer segments generate the most sales?

**SQL analysis**

```sql
SELECT
  Customer_Segment,
  SUM(Total_Sales) AS total_sales
FROM ecommerce-sales-portfolio.ecommerce_sales.sales
GROUP BY Customer_Segment
ORDER BY total_sales DESC;
```
* Results:*

| customer segment | Total Sales |
|---|---:|
| Consumer | 22,412,048 |
| Corporate | 12,446,430 |
| Home Office | 6,942,186 |


*Key Insight:*

Consumer customers generated the highest total sales at 22.4M, followed by Corporate at 12.4M and Home Office at 6.9M.

*Business Relevance:*

Consumer customers are the strongest sales segment, suggesting an opportunity to prioritize marketing and retention efforts toward this customer group.

### 8. Profit by Customer Segment

**Business question:**
Which customer segments generate the most profit?

**SQL analysis**
```sql
SELECT
  Customer_Segment,
  SUM(Profit) AS total_profit
FROM ecommerce-sales-portfolio.ecommerce_sales.sales
GROUP BY Customer_Segment
ORDER BY total_profit DESC;
```
*Results:*

| customer segment | Total Profit |
|---|---:|
| Consumer | 7,946,136 |
| Corporate | 4,067,786 |
| Home Office | 2,579,983 |

*Key Insight:*

Consumer customers generated the highest total profit at 7.95M, followed by Corporate at 4.07M and Home Office at 2.58M.

*Business Relevance:*

Consumer customers are the strongest segment for both sales and profit, making them an important target for marketing and customer-retention efforts.

### 9. Profit by Region 

**Business question:**

Which regions generate the most profit?

**SQL analysis**
```sql
SELECT
  Region,
  SUM(Profit) AS total_profit
FROM ecommerce-sales-portfolio.ecommerce_sales.sales
GROUP BY Region
ORDER BY total_profit DESC;
```

*Key Insight:*

Europe generated the highest total profit at 4.38M, followed closely by North America at 4.20M. South America and the Middle East & Africa had the lowest profit.

*Business Relevance:*

Europe and North America are the strongest markets for profitability, suggesting these regions could be prioritised for continued marketing and growth efforts.

### 10. Average Order Value

**Business question:**
What is the average sales value per order?

**SQL Analysis**
```sql
select
 round(avg(total_sales),3) as avg_order_value
from `ecommerce-sales-portfolio.ecommerce_sales.sales`;
```
*Key Insight:*
The average order value is approximately **$20,920.33**, indicating the average revenue generated per order.

*Business Relevance:*
Understanding average order value helps the business evaluate customer spending and identify opportunities to increase order size through cross-selling, bundles, or targeted promotions.
