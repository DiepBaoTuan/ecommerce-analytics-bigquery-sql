# Explore E-commerce Dataset with SQL

Analysis of website traffic, user behaviour and sales for an online store, using the **Google Analytics sample dataset** on **BigQuery**.

| | |
|---|---|
| **Tool** | Google BigQuery (Standard SQL) |
| **Dataset** | `bigquery-public-data.google_analytics_sample.ga_sessions_2017*` |
| **Period** | January to July 2017 |
| **SQL file** | [`DAC K20 - Diep Bao Tuan.sql`](DAC%20K20%20-%20Diep%20Bao%20Tuan.sql) |

## Business questions

| # | Question | Key techniques |
|---|---|---|
| 1 | Total visits, pageviews and transactions for Jan to Mar 2017 | `_TABLE_SUFFIX`, date parsing, aggregation |
| 2 | Bounce rate per traffic source in July 2017 | Ratio metrics, `GROUP BY` |
| 3 | Revenue by traffic source, by week and by month (June 2017) | `UNNEST` nested fields, `UNION ALL` |
| 4 | Average pageviews: purchasers vs. non-purchasers (June, July 2017) | CTEs, segment comparison, `JOIN` |
| 5 | Average number of transactions per purchasing user (July 2017) | `COUNT(DISTINCT)` |
| 6 | Average revenue per session for purchasers (July 2017) | Revenue normalisation |
| 7 | Other products bought by customers who bought "YouTube Men's Vintage Henley" | Sub-queries, market-basket analysis |
| 8 | Funnel from product view to add-to-cart to purchase (Jan to Mar 2017) | Conditional counts, conversion rates |

## Example: Bounce rate by traffic source

```sql
SELECT
    trafficSource.source                           AS source,
    SUM(totals.visits)                             AS total_visits,
    SUM(totals.bounces)                            AS total_bounces,
    SUM(totals.bounces) / SUM(totals.visits) * 100 AS bounce_rate
FROM `bigquery-public-data.google_analytics_sample.ga_sessions_201707*`
GROUP BY source
ORDER BY total_visits DESC;
```

## How to run

1. Open the [BigQuery console](https://console.cloud.google.com/bigquery). The free sandbox is enough.
2. Copy any query from the SQL file and run it. The dataset is public, so no setup is needed.
