# Project 04 - Employee Data Analyzer

## Scenario

A company wants HR analytics from employee salary and department data.

## Dataset

Create `employees.csv`:

```csv
employee_id,name,department,designation,experience,salary
EMP001,Amit,Data Engineering,Data Engineer,3,75000
EMP002,Rahul,Data Engineering,Senior Data Engineer,5,110000
EMP003,Neha,Analytics,BI Developer,4,90000
EMP004,Priya,HR,HR Executive,2,55000
EMP005,Vikas,Data Engineering,Data Engineer,2,68000
EMP006,Riya,Analytics,Data Analyst,3,70000
EMP007,Karan,IT,Software Engineer,4,95000
EMP008,Pooja,HR,HR Manager,7,125000
EMP009,Arjun,IT,Senior Developer,6,130000
EMP010,Anjali,Analytics,Senior BI Developer,6,120000
```

## Business Questions

1. How many employees are there?
2. What is average salary?
3. What is highest salary?
4. What is lowest salary?
5. Which department has the most employees?
6. What is average salary by department?
7. Who earns above company average?
8. Which department has the highest average salary?
9. Who has more than five years of experience?

## Step-by-Step Solution

### 1. Read data

```python
import csv

with open("employees.csv", "r") as file:
    employees = list(csv.DictReader(file))
```

### 2. Convert numeric fields

```python
for employee in employees:
    employee["experience"] = int(employee["experience"])
    employee["salary"] = float(employee["salary"])
```

### 3. Average salary

```python
average_salary = sum(
    employee["salary"] for employee in employees
) / len(employees)

print(average_salary)
```

### 4. Highest-paid employee

```python
highest_paid = max(
    employees,
    key=lambda employee: employee["salary"]
)

print(highest_paid)
```

### 5. Department count

```python
department_count = {}

for employee in employees:
    department = employee["department"]

    department_count[department] = (
        department_count.get(department, 0) + 1
    )

print(department_count)
```

### 6. Department average salary

```python
department_salary = {}

for employee in employees:
    department = employee["department"]

    department_salary[department] = (
        department_salary.get(department, 0)
        + employee["salary"]
    )

department_average = {
    department:
        department_salary[department] / department_count[department]
    for department in department_salary
}

print(department_average)
```

## Complete Solution

```python
import csv

with open("employees.csv", "r") as file:
    employees = list(csv.DictReader(file))

for employee in employees:
    employee["experience"] = int(employee["experience"])
    employee["salary"] = float(employee["salary"])

average_salary = sum(
    employee["salary"] for employee in employees
) / len(employees)

highest_paid = max(
    employees,
    key=lambda employee: employee["salary"]
)

lowest_paid = min(
    employees,
    key=lambda employee: employee["salary"]
)

department_count = {}
department_salary = {}

for employee in employees:
    department = employee["department"]
    salary = employee["salary"]

    department_count[department] = (
        department_count.get(department, 0) + 1
    )

    department_salary[department] = (
        department_salary.get(department, 0) + salary
    )

department_average = {
    department:
        department_salary[department] / department_count[department]
    for department in department_salary
}

highest_average_department = max(
    department_average,
    key=department_average.get
)

print("Employee Count:", len(employees))
print("Average Salary:", average_salary)
print("Highest Paid:", highest_paid["name"])
print("Lowest Paid:", lowest_paid["name"])
print("Department Count:", department_count)
print("Department Average:", department_average)
print(
    "Highest Average Salary Department:",
    highest_average_department
)

print("\nEmployees Above Average:")

for employee in employees:
    if employee["salary"] > average_salary:
        print(employee["name"], employee["salary"])
```

## Extra Challenges

1. Find highest-paid employee per department.
2. Find average experience per department.
3. Find salary ranges.
4. Add employee search.
5. Add insert/update/delete.
6. Rewrite with Pandas.
7. Export an HR report to Excel.

## Data Engineering Connection

```text
Employee Master
 ↓
Ingestion
 ↓
Validation
 ↓
Transformation
 ↓
Aggregation
 ↓
HR Reporting
```
