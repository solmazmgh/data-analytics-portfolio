# Global E-commerce Sales & Customer Analytics
## Project Overview
This project analyzes e-commerce sales data to understand revenue, profitability, customer behavior, product performance, and geographic performance.
The goal is to use data analysis to identify business trends and opportunities that could support better commercial decision-making.
## Business Problem
The company wants to understand:
- How sales and profit are performing over time
- Which products and categories generate the most revenue
- Which customer segments are most valuable
- Which countries and regions perform best
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
- Data visualization
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
🚧 In progress
More analysis and visualizations will be added as the project develops.

## SQL Analysis
### 1. Sales by product Category
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

### 5. Lowest-Profit Products

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

### 9. Sales by Payment Method

**Business Question:***
Which payment methods generate the most sales?

*Results:*

| Product Category | Total Sales |
|---|---:|
|Credit Card |16,417,070|
|PayPal|12,342,573|
|Cash on Delivery|6,719,273|
|Bank Transfer|6,361,748|

*Key Insight:*
Credit Card generates the highest sales at 16.4M, followed by PayPal at 12.3M.

*Business Relevance:*
Customers strongly favor digital payment methods, suggesting the business should prioritize and optimize Credit Card and PayPal payment experiences.

