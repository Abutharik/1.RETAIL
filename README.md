# Retail Business Performance & Profitability Analysis

## Objective:
Analyze transactional retail data to uncover profit-draining categories, optimize inventory turnover, and identify seasonal product behavior.

## Tools Used:
- SQL
- Python (Pandas, Seaborn)
- Tableau

## Key SQL Queries:
```sql
-- 1. Remove or filter out null/missing records
DELETE FROM retail_data
WHERE product_id IS NULL
   OR category IS NULL
   OR sub_category IS NULL
   OR sales IS NULL
   OR profit IS NULL;

-- 2. Profit margin (%) by category & sub-category
SELECT category, sub_category,
       ROUND(SUM(profit) / NULLIF(SUM(sales), 0) * 100, 2) AS profit_margin_percent
FROM retail_data
GROUP BY category, sub_category
ORDER BY profit_margin_percent ASC;

-- 3. Total sales & profit by region
SELECT region,
       ROUND(SUM(sales), 2) AS total_sales,
       ROUND(SUM(profit), 2) AS total_profit
FROM retail_data
GROUP BY region
ORDER BY total_profit DESC;

