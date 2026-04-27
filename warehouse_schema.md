# Warehouse Schema: Star Schema

## Overview

A **Star Schema** is a data warehouse schema design that organizes data into a central **fact table** surrounded by multiple **dimension tables**. It resembles a star shape, hence the name. It is the most widely used schema in business intelligence and data warehousing due to its simplicity and query performance.

---

## Structure

### Fact Table
The fact table sits at the center of the star schema. It contains:
- **Quantitative measures** (metrics) such as sales revenue, quantity sold, or profit.
- **Foreign keys** that reference each dimension table.

### Dimension Tables
Dimension tables surround the fact table and contain **descriptive attributes** used to filter, group, or label the facts. Examples include customers, products, time, and location.

---

## Example: Sales Star Schema

```
              [Date Dimension]
                     |
[Product Dimension]--[Sales Fact Table]--[Customer Dimension]
                     |
              [Store Dimension]
```

### Sales Fact Table

| Column         | Type    | Description                  |
|----------------|---------|------------------------------|
| sale_id        | INT (PK)| Unique sale identifier       |
| date_key       | INT (FK)| Reference to Date dimension  |
| product_key    | INT (FK)| Reference to Product dimension|
| customer_key   | INT (FK)| Reference to Customer dimension|
| store_key      | INT (FK)| Reference to Store dimension |
| quantity_sold  | INT     | Number of units sold         |
| revenue        | DECIMAL | Total revenue from the sale  |
| discount       | DECIMAL | Discount applied             |

### Date Dimension

| Column       | Type    | Description            |
|--------------|---------|------------------------|
| date_key     | INT (PK)| Unique date identifier |
| full_date    | DATE    | Full calendar date     |
| day_of_week  | VARCHAR | e.g., Monday           |
| month        | VARCHAR | e.g., April            |
| quarter      | VARCHAR | e.g., Q2               |
| year         | INT     | e.g., 2026             |

### Product Dimension

| Column        | Type    | Description              |
|---------------|---------|--------------------------|
| product_key   | INT (PK)| Unique product identifier|
| product_name  | VARCHAR | Name of the product      |
| category      | VARCHAR | Product category         |
| brand         | VARCHAR | Brand name               |
| unit_price    | DECIMAL | Standard price per unit  |

### Customer Dimension

| Column        | Type    | Description                |
|---------------|---------|----------------------------|
| customer_key  | INT (PK)| Unique customer identifier |
| customer_name | VARCHAR | Full name of customer      |
| email         | VARCHAR | Customer email address     |
| region        | VARCHAR | Geographic region          |
| segment       | VARCHAR | e.g., Retail, Wholesale    |

### Store Dimension

| Column      | Type    | Description              |
|-------------|---------|--------------------------|
| store_key   | INT (PK)| Unique store identifier  |
| store_name  | VARCHAR | Name of the store        |
| city        | VARCHAR | City where store is located|
| country     | VARCHAR | Country of the store     |

---

## Advantages of Star Schema

- **Simple design** — easy to understand and navigate.
- **Fast query performance** — fewer joins needed compared to normalized schemas.
- **Well-suited for BI tools** — compatible with tools like Power BI, Tableau, and Looker.
- **Easy aggregation** — metrics can quickly be rolled up across dimensions.

## Disadvantages

- **Data redundancy** — dimension tables may contain repeated data.
- **Not ideal for complex relationships** — many-to-many relationships require additional bridge tables.
- **Maintenance overhead** — updates to dimension data must be carefully managed (slowly changing dimensions).

---

## Star Schema vs Snowflake Schema

| Feature          | Star Schema         | Snowflake Schema         |
|------------------|---------------------|--------------------------|
| Dimension tables | Denormalized        | Normalized               |
| Query complexity | Simple (fewer joins)| Complex (more joins)     |
| Storage          | More space used     | Less space used          |
| Performance      | Faster queries      | Slightly slower queries  |

---

## References

- Kimball, R., & Ross, M. (2013). *The Data Warehouse Toolkit* (3rd ed.). Wiley.
- Microsoft. (2024). [Star schema and the importance for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
