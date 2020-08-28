```sql
ALTER TABLE subscriptions
    ADD year_start INTEGER;
ALTER TABLE subscriptions
    ADD month_start INTEGER;
ALTER TABLE subscriptions
    ADD year_canceled INTEGER;
ALTER TABLE subscriptions
    ADD month_canceled INTEGER;
ALTER TABLE subscriptions
    ADD day_canceled INTEGER;

UPDATE subscriptions
SET
    year_start = strftime('%Y', subscription_start),
    month_start = strftime('%m', subscription_start),
    year_canceled = strftime('%Y', subscription_end),
    month_canceled = strftime('%m', subscription_end),
    day_canceled = strftime('%d', subscription_end);

WITH 
    months AS (
        SELECT DISTINCT month_canceled AS month
        FROM subscriptions
        WHERE month NOT NULL
        ORDER BY month
    ),
    cross_join AS (
        SELECT * FROM subscriptions
        CROSS JOIN months
    ),
    status AS (
        SELECT 
            id, month, segment,
            CASE
                WHEN (year_start < 2017 OR month_start < month)
                    AND (month_canceled > month 
                        OR (month_canceled = month AND day_canceled > 1)
                        OR month_canceled IS NULL) 
                THEN 1 ELSE 0
                END AS active,
            CASE
                WHEN month_canceled = month 
                THEN 1 ELSE 0
                END AS canceled
        FROM cross_join
    ),
    status_total AS (
        SELECT 
            month, segment,
            SUM(active) AS active,
            SUM(canceled) AS canceled
        FROM status
        GROUP BY 1, 2
    )
    SELECT 
        month, segment,
        ROUND(1.*canceled/active, 4) AS churn_rate
    FROM status_totals;
```
