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
<img width="722" height="524" alt="image" src="https://github.com/user-attachments/assets/b70e85bd-aec5-43e3-8893-1ee8e5ad12d3" />
South Africa leads clearly at ~$109K, roughly 30% ahead of Nigeria in second (~$82K). Kenya, Senegal, and Uganda are close together in the $72–77K range. Revenue isn't evenly spread — one country dominates, so growth strategy shouldn't treat all markets equally.

<img width="531" height="502" alt="image" src="https://github.com/user-attachments/assets/ef07024b-1b03-451b-87fc-5fe890305a8a" />
Delivered is the largest slice at 22.5%, but it's barely ahead of Shipped (20.9%) and Cancelled (20.5%). The five statuses are almost evenly split, which is unusual — normally "Delivered" should dominate by a wide margin. This flat distribution is really what's behind the 37.5% cancel/return finding.

<img width="687" height="544" alt="image" src="https://github.com/user-attachments/assets/8bd16023-7fc2-47dd-9664-443d1e9d8018" />
 Fairly even across categories (66–82 orders), with Clothing on top and Toys lowest. No single category dominates order volume, so the cancellation problem is unlikely to be a "one bad category" issue — worth checking if it's evenly distributed too.

<img width="691" height="544" alt="image" src="https://github.com/user-attachments/assets/af6d3882-1a76-470e-bfc5-4b215937b876" />
All categories cluster tightly between ~2.9 and ~3.3 (out of 5). Electronics and Clothing edge out slightly higher; Toys and Books slightly lower. The differences are small enough that this likely isn't statistically meaningful — ratings are fairly uniform across categories, which (combined with the 39.5% missing-rating rate) means I wouldn't lean hard on "Electronics is the best-rated category" as a strong finding.

<img width="687" height="468" alt="image" src="https://github.com/user-attachments/assets/1c367e82-42bf-47ca-84c5-a51b0320abb3" />
Delivery Days Histogram — Roughly flat/uniform distribution from 2–20 days, with a notable spike at 13–15 days. There's no strong clustering around a "typical" delivery time — deliveries are essentially random across the full 2–20 day range, reinforcing that fulfillment isn't standardized.

## Conclusion:
The business generated $637K in revenue across 502 orders, with South Africa, Nigeria, and Kenya as the strongest markets. However, a 37.5% cancellation/return rate signals a significant operational issue that's likely limiting overall growth more than any marketing or expansion effort would help. Delivery times are inconsistent (2–20 days), which may be contributing to that cancellation rate. Overall, the data suggests the business has solid demand and clear regional strengths, but needs to fix fulfillment reliability and tighten data collection before scaling further

## Suggested Next Steps

- Investigate the 37.5% cancel/return rate by category, country, and payment method to find the biggest lever
- Segment delivery day outliers (20-day deliveries) to see if they cluster by country or carrier
- Re-collect ratings at checkout to close the 39.5% missing-rating gap
