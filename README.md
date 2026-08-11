# Ecommerce Orders Analysis

Analysis of 618 raw orders (502 after cleaning) from an African ecommerce platform, covering orders across 8 countries, 7 product categories, and 4 payment methods.

## Key Findings

- **Total revenue: $637,266** across 502 valid orders (~$1,270 average order value). **South Africa is the top market** at $108,561, followed by Nigeria ($81,941), Kenya ($76,613), Senegal ($74,773), and Uganda ($72,084).
- **37.5% of orders are Cancelled or Returned** — a notably high combined rate that's worth investigating further (payment method, product category, or delivery delays as possible drivers).
- **Delivery takes 11 days on average**, ranging from 2 to 20 days (25th percentile: 6 days, 75th percentile: 16 days) — a wide spread suggesting inconsistent fulfillment or shipping performance.
- **Mobile Money is the most-used payment method**, ahead of Credit Card, Bank Transfer, and PayPal — reflecting the mobile-first payment landscape across the represented markets.
- **Data quality was a major issue in the raw file**: 39.5% of orders were missing a `Rating` (customers who didn't leave a review), plus inconsistent text casing (e.g. `Electronics` / `electronics` / `ELECTRONICS`), 15 exact duplicate rows, and ~16% of orders missing a delivery date (order not yet delivered).

## Dataset

| Stage | Rows | Columns |
|---|---|---|
| Raw | 618 | 15 |
| After cleaning (dedup + drop undelivered) | 502 | 19 |

**Cleaning steps applied:** standardized text casing across `Category`/`PaymentMethod`/`Country`/`OrderStatus`/`Product`; filled missing `UnitPrice`/`Quantity` with median, `Discount` with 0, `Country`/`CustomerEmail` with "Unknown"; dropped 15 duplicate rows; dropped rows with no `DeliveryDate` (undelivered orders); derived `TotalRevenue`, `DeliveryDays`, `OrderMonth`, `OrderYear`.

## Additional Metrics

- Average discount applied: **6.8%**
- Top category by order volume: **Clothing**
- Highest-rated category: **Electronics**
- Best revenue month: **May**
- Top products by units sold: Novel (115), Wireless Earbuds (105), Laptop Stand (103), Data Science Handbook (102), Running Shoes (99)

## Charts

| | |
|---|---|
| `1_top_countries_revenue.png` | Revenue leaders by country |
| `2_order_status.png` | Order status breakdown (Delivered/Shipped/Cancelled/Processing/Returned) |
| `3_top_products_quantity.png` | Best-selling products by units |
| `4_missing_values.png` | Data quality — missing values per column (raw data) |
| `5_delivery_days_summary.png` | Delivery time distribution |

Conclusion:
The business generated $637K in revenue across 502 orders, with South Africa, Nigeria, and Kenya as the strongest markets. However, a 37.5% cancellation/return rate signals a significant operational issue that's likely limiting overall growth more than any marketing or expansion effort would help. Delivery times are inconsistent (2–20 days), which may be contributing to that cancellation rate. Overall, the data suggests the business has solid demand and clear regional strengths, but needs to fix fulfillment reliability and tighten data collection before scaling further

Regenerate these (and 6 more — orders by category, revenue by month, rating by category, delivery-day histogram) anytime by running `analyze_orders.py` against the raw or cleaned CSV.

## Suggested Next Steps

- Investigate the 37.5% cancel/return rate by category, country, and payment method to find the biggest lever
- Segment delivery-day outliers (20-day deliveries) to see if they cluster by country or carrier
- Re-collect ratings at checkout to close the 39.5% missing-rating gap
