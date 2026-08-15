# Project 03 - Sales Data Analyzer

## Scenario

A retail company stores order transactions in CSV format. Management wants revenue, product, region, and salesperson analysis.

## Dataset

Create `sales.csv`:

```csv
order_id,date,product,category,region,salesperson,quantity,unit_price
ORD001,2026-01-02,Laptop,Electronics,West,Amit,2,65000
ORD002,2026-01-03,Mouse,Accessories,North,Rahul,10,800
ORD003,2026-01-04,Keyboard,Accessories,West,Neha,5,1500
ORD004,2026-01-05,Monitor,Electronics,South,Priya,3,18000
ORD005,2026-01-06,Laptop,Electronics,North,Vikas,1,65000
ORD006,2026-01-07,Headphones,Accessories,East,Riya,8,2500
ORD007,2026-01-08,Keyboard,Accessories,South,Amit,7,1500
ORD008,2026-01-09,Monitor,Electronics,West,Rahul,4,18000
ORD009,2026-01-10,Laptop,Electronics,East,Neha,2,65000
ORD010,2026-01-11,Mouse,Accessories,North,Priya,15,800
```

## Business Questions

1. What is total revenue?
2. What is total quantity sold?
3. Which product generated the most revenue?
4. Which region generated the most revenue?
5. Which salesperson generated the most revenue?
6. What is average order value?
7. Which category generated the most revenue?
8. Which orders exceed ₹50,000?

## Step-by-Step Solution

### 1. Read CSV

```python
import csv

with open("sales.csv", "r") as file:
    sales = list(csv.DictReader(file))
```

### 2. Convert numeric fields

```python
for row in sales:
    row["quantity"] = int(row["quantity"])
    row["unit_price"] = float(row["unit_price"])
```

### 3. Calculate revenue

```python
for row in sales:
    row["total_sales"] = row["quantity"] * row["unit_price"]
```

### 4. Calculate total revenue

```python
total_sales = sum(row["total_sales"] for row in sales)

print(total_sales)
```

### 5. Product-wise revenue

```python
product_sales = {}

for row in sales:
    product = row["product"]

    product_sales[product] = (
        product_sales.get(product, 0)
        + row["total_sales"]
    )

print(product_sales)
```

### 6. Find best product

```python
best_product = max(
    product_sales,
    key=product_sales.get
)

print(best_product)
```

### 7. Pandas version

```python
import pandas as pd

df = pd.read_csv("sales.csv")

df["total_sales"] = df["quantity"] * df["unit_price"]

print(
    df.groupby("product")["total_sales"]
      .sum()
      .sort_values(ascending=False)
)
```

## Complete Solution

```python
import csv

with open("sales.csv", "r") as file:
    sales = list(csv.DictReader(file))

for row in sales:
    row["quantity"] = int(row["quantity"])
    row["unit_price"] = float(row["unit_price"])
    row["total_sales"] = row["quantity"] * row["unit_price"]

total_sales = sum(row["total_sales"] for row in sales)
total_quantity = sum(row["quantity"] for row in sales)

product_sales = {}
region_sales = {}
salesperson_sales = {}

for row in sales:
    revenue = row["total_sales"]

    product_sales[row["product"]] = (
        product_sales.get(row["product"], 0) + revenue
    )

    region_sales[row["region"]] = (
        region_sales.get(row["region"], 0) + revenue
    )

    salesperson_sales[row["salesperson"]] = (
        salesperson_sales.get(row["salesperson"], 0) + revenue
    )

best_product = max(product_sales, key=product_sales.get)
best_region = max(region_sales, key=region_sales.get)
best_salesperson = max(
    salesperson_sales,
    key=salesperson_sales.get
)

average_order_value = total_sales / len(sales)

print("Total Revenue:", total_sales)
print("Total Quantity:", total_quantity)
print("Average Order Value:", average_order_value)
print("Best Product:", best_product)
print("Best Region:", best_region)
print("Best Salesperson:", best_salesperson)
```

## Extra Challenges

1. Add discount and profit.
2. Calculate monthly revenue.
3. Find top 3 products.
4. Calculate region rankings.
5. Create charts.
6. Export an Excel report.
7. Process a large CSV efficiently.

## Data Engineering Connection

```text
Orders
 ↓
Raw CSV
 ↓
Ingestion
 ↓
Schema Conversion
 ↓
Transformation
 ↓
Aggregation
 ↓
Analytics
```
