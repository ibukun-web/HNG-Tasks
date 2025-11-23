# HNG-Tasks
My HNG internship tasks
---
#  Ride Analytics with PostgreSQL

##  Project Overview
This project showcases advanced SQL analytics performed on a ride-sharing dataset using **PostgreSQL 18** and **pgAdmin 4**. The database contains raw tables for rides, drivers, riders, and payments. Through a series of optimized queries, we extract insights on rider behavior, driver performance, payment trends, cancellations, and revenue growth.

##  Database Schema
The analysis leverages the following tables:
- `rides_raw`: Ride details including pickup/dropoff cities, timestamps, and distances.
- `drivers_raw`: Driver profiles.
- `riders_raw`: Rider profiles and signup dates.
- `payments_raw`: Payment amounts and methods.
- `driver_stats`: Aggregated driver performance metrics.

---

##  Analytical Queries & Insights

### 1. Top 10 Longest Paid Rides
**Query Goal:** Identify the longest rides with successful payments.

**Logic:**
- Join across all four tables.
- Filter for `p.amount > 0`.
- Sort by `distance_km` descending.
- Limit to top 10.

**Insight:**  
Longest rides reached 30 km, with diverse payment methods (voucher, PayPal, cash, card) across cities like Ottawa, Calgary, and Los Angeles.

---

### 2. Riders Active from 2021 to 2024
**Query Goal:** Count riders who signed up in 2021 and paid for rides requested in 2024.

**Result:**  
**1813** distinct riders met the criteria.

---

### 3. Highest Quarterly YoY Revenue Growth
**Query Goal:** Identify the quarter with the highest year-over-year revenue increase.

**Method:**
- Use CTE to calculate revenue growth.
- Compare same quarters across consecutive years.

**Result:**  
**Q2 2022** showed a **200.82%** YoY growth.

---

### 4. Most Consistent Drivers by Month
**Query Goal:** Rank drivers by average monthly ride volume.

**Method:**
- Calculate active months using `MIN` and `MAX` of `request_time`.
- Filter for completed rides.
- Compute average monthly rides.

**Top Performers:**
| Driver Name | Total Rides | Avg Monthly Rides |
|-------------|-------------|-------------------|
| Driver_837  | 32          | 0.80              |
| Driver_537  | 19          | 0.79              |
| Driver_1181 | 31          | 0.78              |
| Driver_1787 | 30          | 0.77              |
| Driver_1018 | 31          | 0.76              |

---

### 5. City with Highest Cancellation Rate
**Query Goal:** Identify the pickup city with the most ride cancellations.

**Result:**  
**Chicago** had a **19.25%** cancellation rate (868 out of 4509 rides).

---

### 6. Riders with >10 Rides and No Cash Payments
**Query Goal:** Find riders who took more than 10 rides and never used cash.

**Result:**  
**Rider_7823** completed **12** rides without using cash.

---

### 7. Top 3 Drivers by Revenue per City (2021–2024)
**Query Goal:** Rank top 3 drivers by revenue in each pickup city between June 2021 and December 2024.

**Method:**
- Use `RANK()` window function.
- Partition by `pickup_city`.

**Sample Output:**
| City     | Driver Name   | Revenue | Rank |
|----------|---------------|---------|------|
| Boston   | Driver_1176   | 448.40  | 1    |
| Calgary  | Driver_1980   | 476.91  | 1    |
| Chicago  | Driver_1176   | 440.45  | 1    |

---

### 8. Top-Rated Drivers with Low Cancellation Rates
**Query Goal:** Select drivers with ≥30 completed rides, ≥4.5 rating, and <5% cancellation rate.

**Result:**
| Driver Name   | Completed Rides | Avg Rating | Cancel Rate |
|---------------|------------------|------------|--------------|
| Driver_837    | 32               | 5.00       | 0.00%        |
| Driver_1005   | 31               | 4.80       | 0.00%        |
| Driver_1181   | 31               | 4.60       | 0.00%        |
| Driver_1483   | 31               | 5.00       | 0.00%        |

---

##  Key Takeaways
- **Driver consistency** and **rider loyalty** can be quantified using SQL.
- **Revenue growth** and **cancellation trends** reveal operational strengths and weaknesses.
- **Window functions**, **CTEs**, and **aggregations** are powerful tools for business intelligence.

##  Tools Used
- PostgreSQL 18
- pgAdmin 4
- SQL (joins, filters, aggregates, window functions)

##  Repository Structure
```
├── screenshots/         # Raw query screenshots
├── queries.sql          # All SQL queries used
├── README.md            # Project documentation
```
