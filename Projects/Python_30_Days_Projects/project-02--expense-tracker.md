# Project 02 - Expense Tracker

## Scenario

A person wants to understand monthly spending. Expense transactions are stored in CSV format.

## Dataset

Create `expenses.csv`:

```csv
expense_id,date,category,description,amount,payment_method
1,2026-01-02,Food,Lunch,250,UPI
2,2026-01-03,Travel,Uber,450,Card
3,2026-01-04,Shopping,Clothes,2200,Card
4,2026-01-05,Food,Dinner,600,UPI
5,2026-01-07,Entertainment,Movie,350,Cash
6,2026-01-10,Travel,Train,800,UPI
7,2026-01-12,Food,Breakfast,180,Cash
8,2026-01-15,Bills,Internet,999,UPI
9,2026-01-18,Shopping,Shoes,2500,Card
10,2026-01-20,Food,Dinner,750,UPI
```

## Business Questions

1. What is total expenditure?
2. Which category has the highest spending?
3. What is the largest transaction?
4. How much was paid by UPI?
5. How much was paid by Card?
6. How much was paid by Cash?
7. Which transactions exceed ₹1,000?
8. What percentage of spending belongs to each category?

## Step-by-Step Solution

### 1. Read data

```python
import csv

with open("expenses.csv", "r") as file:
    expenses = list(csv.DictReader(file))
```

### 2. Convert amounts

```python
for expense in expenses:
    expense["amount"] = float(expense["amount"])
```

### 3. Calculate total

```python
total = sum(e["amount"] for e in expenses)

print("Total Expense:", total)
```

### 4. Category-wise spending

```python
category_total = {}

for expense in expenses:
    category = expense["category"]

    category_total[category] = (
        category_total.get(category, 0)
        + expense["amount"]
    )

print(category_total)
```

### 5. Payment-method analysis

```python
payment_total = {}

for expense in expenses:
    method = expense["payment_method"]

    payment_total[method] = (
        payment_total.get(method, 0)
        + expense["amount"]
    )

print(payment_total)
```

### 6. Highest transaction

```python
highest = max(expenses, key=lambda x: x["amount"])

print(highest)
```

## Complete Solution

```python
import csv

with open("expenses.csv", "r") as file:
    expenses = list(csv.DictReader(file))

for expense in expenses:
    expense["amount"] = float(expense["amount"])

total = sum(e["amount"] for e in expenses)

category_total = {}
payment_total = {}

for expense in expenses:
    category = expense["category"]
    method = expense["payment_method"]
    amount = expense["amount"]

    category_total[category] = (
        category_total.get(category, 0) + amount
    )

    payment_total[method] = (
        payment_total.get(method, 0) + amount
    )

highest = max(expenses, key=lambda x: x["amount"])

print("Total:", total)
print("Category:", category_total)
print("Payment Method:", payment_total)
print("Highest:", highest)

print("\nTransactions above ₹1,000:")

for expense in expenses:
    if expense["amount"] > 1000:
        print(expense)
```

## Extra Challenges

1. Calculate monthly spending.
2. Calculate average daily spending.
3. Add/update/delete transactions.
4. Create a budget limit.
5. Alert when a category exceeds its budget.
6. Rewrite using Pandas.
7. Create a Matplotlib spending chart.

## Data Engineering Connection

```text
Expense CSV
 ↓
Ingestion
 ↓
Type Conversion
 ↓
Cleaning
 ↓
Aggregation
 ↓
Business Metrics
```
