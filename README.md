# Data-Analytics-Project---Sales-Performance-Analysis

-- Clean and aggregate data in SQL

-- Remove duplicates
DELETE FROM sales_data
WHERE ROWID NOT IN (
    SELECT MIN(ROWID)
    FROM sales_data
    GROUP BY product_id, order_date
);

-- Handle missing values
UPDATE sales_data
SET sales_amount = 0
WHERE sales_amount IS NULL;

-- Aggregate data by month
CREATE VIEW monthly_sales AS
SELECT
    YEAR(order_date) AS year,
    MONTH(order_date) AS month,
    SUM(sales_amount) AS total_sales
FROM sales_data
GROUP BY year, month;



