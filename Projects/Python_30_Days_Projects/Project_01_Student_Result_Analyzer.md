# Project 01 - Student Result Analyzer

## Scenario

A college stores student examination marks in a CSV file. The administration wants a Python program that converts raw marks into useful academic information.

## Dataset

Create `students.csv`:

```csv
student_id,name,python,sql,maths,english
101,Amit,85,78,92,80
102,Rahul,72,68,75,70
103,Neha,91,88,95,90
104,Priya,65,72,68,75
105,Vikas,45,52,48,55
106,Riya,88,91,84,87
107,Karan,55,61,58,60
108,Pooja,76,82,79,85
109,Arjun,35,42,38,45
110,Anjali,94,89,96,92
```

## Business Questions

1. Calculate total marks for every student.
2. Calculate percentage.
3. Assign grades.
4. Identify Pass/Fail students.
5. Find the topper.
6. Calculate class average.
7. Count students by grade.
8. Find the highest-average subject.
9. Find students above the class average.

## Grade Rules

| Percentage | Grade |
|---|---|
| 90-100 | A+ |
| 80-89 | A |
| 70-79 | B |
| 60-69 | C |
| 50-59 | D |
| Below 50 | F |

## Step-by-Step Solution

### 1. Read the CSV

```python
import csv

with open("students.csv", "r") as file:
    students = list(csv.DictReader(file))
```

### 2. Convert marks to integers

```python
subjects = ["python", "sql", "maths", "english"]

for student in students:
    for subject in subjects:
        student[subject] = int(student[subject])
```

### 3. Create grade function

```python
def calculate_grade(percentage):
    if percentage >= 90:
        return "A+"
    elif percentage >= 80:
        return "A"
    elif percentage >= 70:
        return "B"
    elif percentage >= 60:
        return "C"
    elif percentage >= 50:
        return "D"
    return "F"
```

### 4. Calculate student results

```python
for student in students:
    student["total"] = sum(student[s] for s in subjects)
    student["percentage"] = student["total"] / 400 * 100
    student["grade"] = calculate_grade(student["percentage"])
    student["status"] = "Pass" if student["percentage"] >= 50 else "Fail"
```

### 5. Find topper and average

```python
topper = max(students, key=lambda x: x["percentage"])

average = sum(
    student["percentage"] for student in students
) / len(students)

print("Topper:", topper["name"])
print("Class Average:", round(average, 2))
```

### 6. Count grades

```python
grade_count = {}

for student in students:
    grade = student["grade"]
    grade_count[grade] = grade_count.get(grade, 0) + 1

print(grade_count)
```

## Complete Solution

```python
import csv

subjects = ["python", "sql", "maths", "english"]

with open("students.csv", "r") as file:
    students = list(csv.DictReader(file))


def calculate_grade(percentage):
    if percentage >= 90:
        return "A+"
    elif percentage >= 80:
        return "A"
    elif percentage >= 70:
        return "B"
    elif percentage >= 60:
        return "C"
    elif percentage >= 50:
        return "D"
    return "F"


for student in students:
    for subject in subjects:
        student[subject] = int(student[subject])

    student["total"] = sum(student[s] for s in subjects)
    student["percentage"] = student["total"] / 400 * 100
    student["grade"] = calculate_grade(student["percentage"])
    student["status"] = "Pass" if student["percentage"] >= 50 else "Fail"


topper = max(students, key=lambda x: x["percentage"])

class_average = sum(
    student["percentage"] for student in students
) / len(students)

grade_count = {}

for student in students:
    grade = student["grade"]
    grade_count[grade] = grade_count.get(grade, 0) + 1

print("Topper:", topper["name"])
print("Topper Percentage:", round(topper["percentage"], 2))
print("Class Average:", round(class_average, 2))
print("Grade Count:", grade_count)

for student in students:
    print(
        student["name"],
        student["total"],
        round(student["percentage"], 2),
        student["grade"],
        student["status"]
    )
```

## Extra Challenges

1. Find the topper in each subject.
2. Find the lowest-scoring student.
3. Calculate subject averages.
4. Export results to `student_results.csv`.
5. Rewrite the solution using Pandas.
6. Create a menu-driven application.

## Data Engineering Connection

```text
CSV
 ↓
Extract
 ↓
Validate
 ↓
Transform
 ↓
Aggregate
 ↓
Report
```
