-- 1. Remove or filter out null/missing records from transactional data
DELETE FROM retail_data
WHERE product_id IS NULL
   OR category IS NULL
   OR sub_category IS NULL
   OR sales IS NULL
   OR profit IS NULL;

-- 2. Calculate profit margin (%) by category and sub-category
SELECT
    category,
    sub_category,
    ROUND(SUM(profit) / NULLIF(SUM(sales), 0) * 100, 2) AS profit_margin_percent
FROM retail_data
GROUP BY category, sub_category
ORDER BY profit_margin_percent ASC;

-- 3. Calculate total sales, total profit by region
SELECT
    region,
    ROUND(SUM(sales), 2) AS total_sales,
    ROUND(SUM(profit), 2) AS total_profit
FROM retail_data
GROUP BY region
ORDER BY total_profit DESC;

-- 4. Ide
