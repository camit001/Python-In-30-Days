
<div align="center">
  <h1> # Python — Introduction, Theory, Core Concepts and Interview Notes</h1>
  <!-- <a class="header-badge" target="_blank" href="">
  <img src="https://img.shields.io/badge/style--5eba00.svg?label=LinkedIn&logo=linkedin&style=social">
  </a>
  <a class="header-badge" target="_blank" href="">
  <img alt="Twitter Follow" src=""> -->
  </a>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>

</div>

**[Day 2 >>](Day_02_Variables_builtin_functions/02_variables_builtin_functions.md)**

## 1. Introduction to Python

Python is a high-level, general-purpose, interpreted programming language known for its simple syntax, readability, and large ecosystem of libraries.

Python was created by **Guido van Rossum** and first released in **1991**.

Python is commonly used for:

- Data Engineering
- Data Science
- Machine Learning
- Web Development
- Automation and Scripting
- API Development
- DevOps
- Testing
- Application Development

### Why Python is popular

1. Easy-to-read syntax
2. Large standard library
3. Huge third-party ecosystem
4. Cross-platform support
5. Supports object-oriented, procedural, and functional programming
6. Strong community support
7. Excellent support for data processing and analytics

---

# 2. Key Characteristics of Python

## High-Level Language

Python hides low-level memory-management details from the developer.

```python
name = "Amit"
print(name)
```

The developer does not need to manually allocate and release memory.

## Interpreted Language

Python programs are generally executed through the Python interpreter rather than being compiled directly into native machine code by the programmer.

Internally, CPython compiles source code into **bytecode**, which is then executed by the Python Virtual Machine.

```text
Python Source Code
        |
        v
     Bytecode
        |
        v
 Python Virtual Machine
```

## Dynamically Typed

The type of a variable is determined at runtime.

```python
x = 10
x = "Python"
```

The same variable name can refer to objects of different types at different times.

## Strongly Typed

Python does not automatically perform arbitrary incompatible type conversions.

```python
x = "10"
y = 5

# x + y
# TypeError
```

Explicit conversion is required:

```python
result = int(x) + y
print(result)
```

## Cross-Platform

Python applications can run on Windows, Linux, and macOS, provided the required Python version and dependencies are available.

## Open Source

Python is freely available and has a large open-source community.

---

# 3. Python Implementations

An implementation is a system that executes Python code.

### CPython

The default and most widely used Python implementation.

It is written primarily in C.

### PyPy

A Python implementation that uses Just-In-Time compilation and can improve performance for some workloads.

### Jython

Python implemented on the Java Virtual Machine.

### IronPython

Python implementation designed for the .NET ecosystem.

For most Python and PySpark development, **CPython** is the common implementation.

---

# 4. Python Program Structure

Example:

```python
name = "Amit"
age = 25

if age >= 18:
    print(name, "is an adult")
```

Python uses indentation to define blocks of code.

```python
if condition:
    statement
```

Incorrect indentation can result in an error:

```python
if True:
print("Hello")
```

Correct:

```python
if True:
    print("Hello")
```

---

# 5. Comments

Comments are ignored during program execution.

## Single-line comment

```python
# This is a comment
name = "Amit"
```

## Multi-line documentation

Triple-quoted strings are commonly used for docstrings:

```python
def add(a, b):
    """Return the sum of two numbers."""
    return a + b
```

---

# 6. Variables

A variable is a name that refers to an object.

```python
x = 10
name = "Amit"
salary = 50000.50
```

Python variables do not require explicit type declarations.

```python
x = 10
print(type(x))
```

Output:

```text
<class 'int'>
```

### Variable naming rules

Valid:

```python
first_name = "Amit"
age2 = 25
_total = 100
```

Invalid:

```python
# 2age = 25
# first-name = "Amit"
```

Python is case-sensitive:

```python
name = "Amit"
Name = "Rahul"
```

`name` and `Name` are different variables.

---

# 7. Data Types

Python provides several built-in data types.

| Category | Types |
|---|---|
| Numeric | int, float, complex |
| Boolean | bool |
| Text | str |
| Sequence | list, tuple, range |
| Set | set, frozenset |
| Mapping | dict |
| Binary | bytes, bytearray |
| None | NoneType |

Example:

```python
age = 25
salary = 50000.50
name = "Amit"
active = True
skills = ["Python", "SQL"]
details = {"name": "Amit", "age": 25}
```

---

# 8. Mutable vs Immutable Objects

This is an important Python concept.

## Mutable

An object can be modified after creation.

Examples:

- list
- dictionary
- set
- bytearray

```python
numbers = [1, 2, 3]
numbers.append(4)

print(numbers)
```

## Immutable

An object cannot be modified after creation.

Examples:

- int
- float
- bool
- str
- tuple
- frozenset
- bytes

```python
name = "Amit"

# A new string object is created when the value changes.
name = name + " Kumar"
```

The original string object is not modified.

---

# 9. Operators

## Arithmetic Operators

```python
a = 10
b = 3

print(a + b)
print(a - b)
print(a * b)
print(a / b)
print(a // b)
print(a % b)
print(a ** b)
```

Operators:

| Operator | Meaning |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| // | Floor division |
| % | Modulus |
| ** | Exponentiation |

## Comparison Operators

```python
a == b
a != b
a > b
a < b
a >= b
a <= b
```

## Logical Operators

```python
and
or
not
```

Example:

```python
age = 25

if age >= 18 and age <= 60:
    print("Eligible")
```

## Membership Operators

```python
in
not in
```

```python
skills = ["Python", "SQL"]

print("Python" in skills)
```

## Identity Operators

```python
is
is not
```

`is` checks whether two references point to the same object.

`==` checks whether two objects have equal values.

---

# 10. Type Conversion

Type conversion changes an object from one data type to another.

```python
x = "100"

num = int(x)
value = float(x)
text = str(num)
```

Common functions:

```python
int()
float()
str()
bool()
list()
tuple()
set()
dict()
```

Example:

```python
numbers = ["1", "2", "3"]

result = [int(x) for x in numbers]

print(result)
```

---

# 11. Conditional Statements

## if

```python
age = 20

if age >= 18:
    print("Adult")
```

## if-else

```python
age = 16

if age >= 18:
    print("Adult")
else:
    print("Minor")
```

## if-elif-else

```python
marks = 80

if marks >= 90:
    grade = "A"
elif marks >= 75:
    grade = "B"
else:
    grade = "C"
```

---

# 12. Loops

Loops execute a block repeatedly.

## for loop

```python
for i in range(5):
    print(i)
```

## while loop

```python
i = 0

while i < 5:
    print(i)
    i += 1
```

## break

Stops the loop.

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

## continue

Skips the current iteration.

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

## pass

Does nothing and is used as a placeholder.

```python
if True:
    pass
```

---

# 13. Strings

A string is an immutable sequence of characters.

```python
name = "Amit Kumar"
```

## Indexing

```python
name = "Python"

print(name[0])
print(name[-1])
```

## Slicing

```python
print(name[0:3])
print(name[:3])
print(name[2:])
print(name[::-1])
```

## Common String Methods

```python
text.upper()
text.lower()
text.strip()
text.replace()
text.split()
text.startswith()
text.endswith()
text.find()
text.count()
```

Example:

```python
text = "Python Data Engineering"

print(text.upper())
print(text.split())
```

## f-strings

Preferred for readable string formatting:

```python
name = "Amit"
age = 25

message = f"My name is {name} and my age is {age}"
print(message)
```

---

# 14. Lists

A list is an ordered and mutable collection.

```python
numbers = [10, 20, 30, 40]
```

Lists can contain different data types:

```python
data = [10, "Python", True, 10.5]
```

Common methods:

```python
append()
extend()
insert()
remove()
pop()
clear()
sort()
reverse()
```

Example:

```python
numbers = [3, 1, 2]

numbers.append(4)
numbers.sort()

print(numbers)
```

---

# 15. Tuples

A tuple is an ordered and immutable collection.

```python
data = (10, 20, 30)
```

Tuples are useful when the collection should not be modified.

```python
coordinates = (19.07, 72.87)
```

Tuple unpacking:

```python
x, y = coordinates
```

---

# 16. Sets

A set is an unordered collection of unique elements.

```python
numbers = {1, 2, 3, 3}

print(numbers)
```

Output contains only unique values.

Common operations:

```python
union()
intersection()
difference()
```

Example:

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a.intersection(b))
```

---

# 17. Dictionaries

A dictionary stores data as key-value pairs.

```python
employee = {
    "id": 101,
    "name": "Amit",
    "department": "Data Engineering"
}
```

Access values:

```python
print(employee["name"])
print(employee.get("name"))
```

Add/update:

```python
employee["salary"] = 60000
employee["department"] = "Analytics"
```

Common methods:

```python
keys()
values()
items()
get()
update()
pop()
```

Iteration:

```python
for key, value in employee.items():
    print(key, value)
```

---

# 18. Functions

A function is a reusable block of code.

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)
```

Benefits:

- Code reuse
- Better organization
- Easier testing
- Easier maintenance
- Reduced duplication

## Default Arguments

```python
def greet(name="User"):
    print(f"Hello {name}")
```

## Keyword Arguments

```python
def employee(name, age):
    print(name, age)

employee(age=25, name="Amit")
```

---

# 19. *args and **kwargs

## *args

Used to accept a variable number of positional arguments.

```python
def total(*args):
    return sum(args)

print(total(10, 20, 30))
```

Inside the function, `args` is a tuple.

## **kwargs

Used to accept a variable number of keyword arguments.

```python
def display(**kwargs):
    for key, value in kwargs.items():
        print(key, value)

display(name="Amit", age=25)
```

Inside the function, `kwargs` is a dictionary.

---

# 20. Lambda Functions

A lambda is a small anonymous function.

```python
square = lambda x: x * x

print(square(5))
```

Lambda functions are commonly used with functional operations.

```python
numbers = [1, 2, 3, 4]

result = list(map(lambda x: x * 2, numbers))

print(result)
```

---

# 21. map(), filter() and reduce()

## map()

Applies a function to each element.

```python
numbers = [1, 2, 3]

result = list(map(lambda x: x * 2, numbers))
```

## filter()

Filters elements based on a condition.

```python
numbers = [1, 2, 3, 4, 5]

result = list(filter(lambda x: x % 2 == 0, numbers))
```

## reduce()

Reduces a collection to a single result.

```python
from functools import reduce

numbers = [1, 2, 3, 4]

result = reduce(lambda x, y: x + y, numbers)
```

---

# 22. List Comprehension

List comprehensions provide a concise way to create lists.

Normal approach:

```python
numbers = []

for i in range(5):
    numbers.append(i * 2)
```

Comprehension:

```python
numbers = [i * 2 for i in range(5)]
```

With condition:

```python
even_numbers = [i for i in range(10) if i % 2 == 0]
```

---

# 23. Dictionary Comprehension

```python
numbers = [1, 2, 3, 4]

squares = {x: x * x for x in numbers}

print(squares)
```

---

# 24. Set Comprehension

```python
numbers = [1, 2, 2, 3]

squares = {x * x for x in numbers}
```

---

# 25. Exception Handling

Exceptions are runtime errors that interrupt normal program execution.

Python provides:

```python
try
except
else
finally
```

Example:

```python
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
```

## else

Runs when no exception occurs.

```python
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Error")
else:
    print(result)
```

## finally

Runs regardless of whether an exception occurs.

```python
try:
    print("Processing")
finally:
    print("Cleanup")
```

## Raising Exceptions

```python
age = -1

if age < 0:
    raise ValueError("Age cannot be negative")
```

---

# 26. File Handling

Python can read and write files using `open()`.

```python
file = open("data.txt", "r")

content = file.read()

file.close()
```

Preferred approach:

```python
with open("data.txt", "r") as file:
    content = file.read()
```

The `with` statement automatically handles resource cleanup.

Common modes:

| Mode | Meaning |
|---|---|
| r | Read |
| w | Write |
| a | Append |
| x | Create |
| rb | Read binary |
| wb | Write binary |

---

# 27. Modules

A module is a Python file containing reusable code.

Example:

```python
# calculator.py

def add(a, b):
    return a + b
```

Use it:

```python
import calculator

print(calculator.add(10, 20))
```

Specific import:

```python
from calculator import add
```

---

# 28. Packages

A package is a collection of related Python modules.

Example:

```text
project/
│
├── main.py
└── utilities/
    ├── __init__.py
    ├── string_utils.py
    └── math_utils.py
```

Packages help organize large applications.

---

# 29. __name__ == "__main__"

Python files can be used both as modules and as standalone scripts.

```python
def main():
    print("Application started")

if __name__ == "__main__":
    main()
```

When the file is executed directly, `__name__` is `"__main__"`.

When imported, that block does not execute automatically.

---

# 30. Object-Oriented Programming

Python supports object-oriented programming.

The main OOP concepts are:

1. Class
2. Object
3. Encapsulation
4. Inheritance
5. Polymorphism
6. Abstraction

---

# 31. Class and Object

A class is a blueprint.

An object is an instance of a class.

```python
class Employee:

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def display(self):
        print(self.name, self.salary)


employee = Employee("Amit", 60000)

employee.display()
```

---

# 32. __init__

`__init__` is commonly used as an initializer for an object.

```python
class Employee:

    def __init__(self, name):
        self.name = name
```

When an object is created, the initializer is called.

---

# 33. self

`self` refers to the current object instance.

```python
class Employee:

    def __init__(self, name):
        self.name = name
```

`self.name` is an instance attribute.

---

# 34. Encapsulation

Encapsulation means keeping data and behavior together and controlling access to implementation details.

Python does not enforce traditional private access as strictly as languages such as Java or C#.

Naming conventions include:

```python
_name
__name
```

A double underscore triggers name mangling.

---

# 35. Inheritance

Inheritance allows one class to reuse or extend another class.

```python
class Employee:

    def display(self):
        print("Employee")


class Developer(Employee):

    def code(self):
        print("Writing code")


developer = Developer()

developer.display()
developer.code()
```

---

# 36. Polymorphism

Polymorphism means the same interface can behave differently for different objects.

```python
class Dog:

    def sound(self):
        return "Bark"


class Cat:

    def sound(self):
        return "Meow"


animals = [Dog(), Cat()]

for animal in animals:
    print(animal.sound())
```

---

# 37. Abstraction

Abstraction hides implementation details and exposes the required interface.

Python provides the `abc` module for abstract base classes.

```python
from abc import ABC, abstractmethod


class Employee(ABC):

    @abstractmethod
    def work(self):
        pass
```

A child class must implement the abstract method.

---

# 38. Iterators

An iterator is an object that returns values one at a time.

It implements:

```python
__iter__()
__next__()
```

Example:

```python
numbers = iter([10, 20, 30])

print(next(numbers))
print(next(numbers))
```

---

# 39. Generators

Generators produce values lazily using `yield`.

```python
def numbers():
    for i in range(5):
        yield i

for value in numbers():
    print(value)
```

### Why generators are useful

Generators do not need to create the entire result in memory at once.

This is useful when processing:

- Large files
- Large datasets
- Streaming data
- Data pipelines

---

# 40. Iterator vs Generator

| Iterator | Generator |
|---|---|
| Implements iterator protocol | Usually created using `yield` |
| Can be implemented manually | Python handles much of the iterator machinery |
| More code may be required | Usually simpler |
| Can provide lazy evaluation | Provides lazy evaluation |

---

# 41. Decorators

A decorator modifies or extends the behavior of a function without changing its source code.

Example:

```python
def logger(func):

    def wrapper():
        print("Function started")
        func()
        print("Function completed")

    return wrapper


@logger
def process():
    print("Processing data")


process()
```

Common uses:

- Logging
- Authentication
- Authorization
- Timing
- Validation
- Caching

---

# 42. Context Managers

Context managers manage resources automatically.

The most common example is file handling:

```python
with open("data.txt", "r") as file:
    data = file.read()
```

The `with` statement ensures the resource is properly released.

Custom context managers can implement:

```python
__enter__()
__exit__()
```

---

# 43. Shallow Copy vs Deep Copy

## Shallow Copy

Creates a new outer object but nested objects can still be shared.

```python
import copy

original = [[1, 2], [3, 4]]

shallow = copy.copy(original)
```

## Deep Copy

Recursively copies nested objects.

```python
deep = copy.deepcopy(original)
```

### Difference

```text
Shallow Copy
Outer object -> copied
Nested objects -> shared

Deep Copy
Outer object -> copied
Nested objects -> copied
```

---

# 44. is vs ==

This is a common interview question.

`==` compares values.

`is` checks object identity.

```python
a = [1, 2]
b = [1, 2]

print(a == b)   # True
print(a is b)   # False
```

The lists contain the same values but are different objects.

---

# 45. Python Memory Management

Python manages memory automatically.

Important concepts include:

- Reference counting
- Garbage collection
- Private heap
- Python memory allocator

In CPython, reference counting is a major mechanism for tracking object lifetime.

The garbage collector additionally handles reference cycles.

Example:

```python
import gc

gc.collect()
```

---

# 46. Garbage Collection

Garbage collection removes objects that are no longer reachable.

Example:

```python
class Employee:
    pass

employee = Employee()

del employee
```

After the reference is removed and the object is no longer reachable, its memory can eventually be reclaimed.

---

# 47. Python Scope

Python follows the LEGB rule:

```text
L = Local
E = Enclosing
G = Global
B = Built-in
```

Example:

```python
x = "global"

def outer():

    x = "enclosing"

    def inner():
        x = "local"
        print(x)

    inner()

outer()
```

Python searches for names in the LEGB order.

---

# 48. global and nonlocal

## global

Used to modify a global variable from inside a function.

```python
count = 0

def increment():
    global count
    count += 1
```

## nonlocal

Used to modify a variable from an enclosing function.

```python
def outer():

    count = 0

    def inner():
        nonlocal count
        count += 1

    inner()
    print(count)
```

---

# 49. Python Virtual Environment

A virtual environment isolates project dependencies.

Create:

```bash
python -m venv venv
```

Windows activation:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
source venv/bin/activate
```

Deactivate:

```bash
deactivate
```

---

# 50. pip

`pip` is Python's package installer.

Install:

```bash
pip install pandas
```

Install a specific version:

```bash
pip install pandas==2.2.0
```

List packages:

```bash
pip list
```

Save dependencies:

```bash
pip freeze > requirements.txt
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

# 51. Python Package Management

A typical project may contain:

```text
project/
│
├── venv/
├── src/
│   ├── main.py
│   └── utilities.py
├── tests/
├── requirements.txt
└── README.md
```

For production projects, dependency versions should be controlled and reproducible.

---

# 52. JSON Handling

Python provides the `json` module.

```python
import json

data = {
    "name": "Amit",
    "age": 25
}

json_string = json.dumps(data)

print(json_string)
```

JSON string to Python object:

```python
data = json.loads(json_string)
```

File example:

```python
with open("employee.json", "r") as file:
    data = json.load(file)
```

---

# 53. Working with CSV

Python provides the `csv` module.

```python
import csv

with open("employees.csv", "r") as file:

    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

For analytics workloads, pandas is commonly used:

```python
import pandas as pd

df = pd.read_csv("employees.csv")
```

---

# 54. Python and SQL

Python is frequently used with databases.

Example concept:

```text
Python Application
       |
       v
Database Driver
       |
       v
SQL Database
```

Common database libraries include drivers and client libraries for:

- SQL Server
- PostgreSQL
- MySQL
- Oracle
- SQLite

---

# 55. Python for Data Engineering

Python is widely used in data engineering because it integrates with:

- Apache Spark
- PySpark
- Pandas
- SQL databases
- REST APIs
- Cloud storage
- Kafka
- Azure
- AWS
- GCP

Typical architecture:

```text
Source Systems
     |
     v
Python / ADF / Kafka
     |
     v
Raw Data
     |
     v
PySpark
     |
     v
Transformation
     |
     v
Delta / Warehouse
     |
     v
BI / Analytics
```

---

# 56. Python and PySpark

PySpark is the Python API for Apache Spark.

Basic example:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("Example") \
    .getOrCreate()

df = spark.read.csv(
    "/data/employees.csv",
    header=True,
    inferSchema=True
)

df.show()
```

---

# 57. Python Data Structures vs PySpark DataFrames

Python list:

```python
employees = [
    {"id": 1, "name": "Amit"},
    {"id": 2, "name": "Rahul"}
]
```

PySpark DataFrame:

```python
df = spark.createDataFrame(employees)

df.show()
```

### Important difference

Python collections normally operate in the Python process.

PySpark DataFrames represent distributed data processing using Spark.

For large datasets, PySpark DataFrames are generally more appropriate than Python lists.

---

# 58. PySpark Functions

Common PySpark functions are imported as:

```python
from pyspark.sql import functions as F
```

Example:

```python
df.select(
    F.col("employee_id"),
    F.upper(F.col("name")).alias("employee_name")
)
```

Common functions:

```python
F.col()
F.lit()
F.when()
F.coalesce()
F.sum()
F.count()
F.avg()
F.max()
F.min()
F.row_number()
F.dense_rank()
```

---

# 59. Python UDFs

A Python UDF allows custom Python logic to be applied to Spark data.

Example:

```python
from pyspark.sql.functions import udf
from pyspark.sql.types import StringType


def clean_name(name):
    return name.strip().title()


clean_name_udf = udf(clean_name, StringType())

df = df.withColumn(
    "clean_name",
    clean_name_udf("name")
)
```

### Important Data Engineering Note

Python UDFs can be slower than native Spark functions because data may need to cross the Python/JVM boundary.

Prefer built-in Spark functions when possible.

---

# 60. Pandas UDF

Pandas UDFs use vectorized operations and Apache Arrow to improve performance for supported workloads.

Example:

```python
from pyspark.sql.functions import pandas_udf

@pandas_udf("double")
def multiply_by_two(series):
    return series * 2
```

They can be useful when custom Python/Pandas logic is required.

---

# 61. Python Type Hints

Type hints improve readability and tooling.

```python
def add(a: int, b: int) -> int:
    return a + b
```

Type hints do not normally enforce types at runtime by themselves.

Example:

```python
def get_name(employee: dict) -> str:
    return employee["name"]
```

---

# 62. Dataclasses

Dataclasses simplify classes primarily used for storing data.

```python
from dataclasses import dataclass


@dataclass
class Employee:
    name: str
    age: int
    salary: float
```

Usage:

```python
employee = Employee("Amit", 25, 60000)
```

---

# 63. Named Tuples

A named tuple provides tuple-like immutable objects with named fields.

```python
from collections import namedtuple

Employee = namedtuple("Employee", ["name", "age"])

employee = Employee("Amit", 25)

print(employee.name)
```

---

# 64. Collections Module

The `collections` module provides specialized data structures.

Common classes:

```python
Counter
defaultdict
deque
namedtuple
```

Example:

```python
from collections import Counter

values = ["A", "B", "A", "C", "A"]

count = Counter(values)

print(count)
```

---

# 65. Regular Expressions

The `re` module supports regular expressions.

```python
import re

text = "Employee ID: EMP-1001"

result = re.search(r"EMP-\d+", text)

if result:
    print(result.group())
```

Regular expressions are useful for:

- Validation
- Data cleansing
- Text extraction
- Pattern matching

---

# 66. Logging

The `logging` module is preferred over `print()` for application logging.

```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Pipeline started")
logging.warning("Missing value found")
logging.error("Pipeline failed")
```

Common log levels:

```text
DEBUG
INFO
WARNING
ERROR
CRITICAL
```

---

# 67. Unit Testing

Python provides the `unittest` framework.

```python
import unittest


def add(a, b):
    return a + b


class TestMath(unittest.TestCase):

    def test_add(self):
        self.assertEqual(add(2, 3), 5)


if __name__ == "__main__":
    unittest.main()
```

Other popular testing tools include `pytest`.

---

# 68. Python Exceptions — Common Types

Common built-in exceptions:

```text
ValueError
TypeError
NameError
IndexError
KeyError
FileNotFoundError
ZeroDivisionError
AttributeError
ImportError
ModuleNotFoundError
```

Example:

```python
numbers = [1, 2, 3]

try:
    print(numbers[10])
except IndexError:
    print("Invalid index")
```

---

# 69. Common Python Interview Questions

## Q1. Is Python compiled or interpreted?

Python is commonly described as an interpreted language. In CPython, source code is compiled to bytecode and that bytecode is executed by the Python Virtual Machine.

## Q2. What is dynamic typing?

Variable types are determined at runtime.

```python
x = 10
x = "Python"
```

## Q3. What is the difference between list and tuple?

| List | Tuple |
|---|---|
| Mutable | Immutable |
| Uses `[]` | Uses `()` |
| Generally more flexible | Useful for fixed collections |

## Q4. Difference between `is` and `==`?

`==` compares values.

`is` compares object identity.

## Q5. What are mutable data types?

Examples:

```text
list
dict
set
bytearray
```

## Q6. What are immutable data types?

Examples:

```text
int
float
bool
str
tuple
bytes
frozenset
```

## Q7. What is a decorator?

A decorator modifies or extends function behavior without changing the function's source code.

## Q8. What is a generator?

A generator produces values lazily using `yield`.

## Q9. What is `*args`?

It collects variable positional arguments into a tuple.

## Q10. What is `**kwargs`?

It collects variable keyword arguments into a dictionary.

## Q11. What is the LEGB rule?

Python searches for names in:

```text
Local
Enclosing
Global
Built-in
```

## Q12. What is garbage collection?

It is the process of reclaiming memory from objects that are no longer reachable.

## Q13. What is a virtual environment?

An isolated Python environment used to manage project-specific dependencies.

## Q14. What is PEP 8?

PEP 8 is the Python style guide containing recommendations for writing readable and consistent Python code.

## Q15. Why are Python UDFs often slower in PySpark?

They can introduce serialization and Python/JVM communication overhead. Native Spark functions are generally preferable when equivalent functionality exists.

---

# 70. Important Python Concepts for Data Engineers

For a Data Engineer, the following Python topics should receive particular attention:

### Core Python

- Variables
- Data types
- Lists
- Tuples
- Sets
- Dictionaries
- Strings
- Loops
- Functions
- Exception handling

### Intermediate Python

- List comprehensions
- Dictionary comprehensions
- Lambda
- `map()`
- `filter()`
- `reduce()`
- Iterators
- Generators
- Decorators
- Context managers
- Modules and packages
- OOP

### Data Engineering Python

- File handling
- CSV
- JSON
- APIs
- Database connectivity
- Logging
- Exception handling
- Configuration management
- Environment variables
- Pandas
- PySpark
- UDFs and Pandas UDFs
- Data validation
- Unit testing

---

# 71. Recommended Learning Order

A practical learning sequence is:

```text
1. Python Syntax
       |
2. Variables and Data Types
       |
3. Operators
       |
4. Conditions
       |
5. Loops
       |
6. Strings
       |
7. Lists / Tuples / Sets / Dictionaries
       |
8. Functions
       |
9. Exception Handling
       |
10. File Handling
       |
11. Modules and Packages
       |
12. OOP
       |
13. Comprehensions
       |
14. Lambda / map / filter / reduce
       |
15. Iterators / Generators
       |
16. Decorators / Context Managers
       |
17. JSON / CSV / APIs
       |
18. Pandas
       |
19. PySpark
       |
20. Data Engineering Projects
```

---

# 72. Quick Revision Cheat Sheet

```text
Python
├── Variables
├── Data Types
│   ├── int
│   ├── float
│   ├── str
│   ├── bool
│   ├── list
│   ├── tuple
│   ├── set
│   └── dict
│
├── Operators
├── Conditions
├── Loops
│   ├── for
│   └── while
│
├── Functions
│   ├── *args
│   ├── **kwargs
│   └── lambda
│
├── Collections
├── Comprehensions
├── Exception Handling
├── File Handling
├── Modules / Packages
├── OOP
│   ├── Class
│   ├── Object
│   ├── Encapsulation
│   ├── Inheritance
│   ├── Polymorphism
│   └── Abstraction
│
├── Iterators
├── Generators
├── Decorators
├── Context Managers
├── Memory Management
├── Garbage Collection
├── Virtual Environments
├── pip
├── JSON / CSV
├── Logging
├── Testing
└── PySpark
```

---

# 73. Final Notes

Python is especially valuable for Data Engineering because it provides a simple programming model while integrating with distributed processing frameworks, databases, APIs, cloud platforms, and data-storage systems.

For a Data Engineer, understanding Python should go beyond syntax. The most important concepts are:

1. How Python objects and data types work
2. Mutable vs immutable objects
3. Functions and variable scope
4. Exception handling
5. File and JSON processing
6. Iterators and generators
7. OOP fundamentals
8. Modules and dependency management
9. Memory management
10. Performance considerations
11. Python-to-JVM overhead in PySpark
12. Native Spark functions vs Python UDFs
13. Writing maintainable and testable data-processing code

The goal should be to understand **why Python behaves the way it does**, not just memorize syntax.


**[Day 2 >>](Day_02_Variables_builtin_functions/02_variables_builtin_functions.md)**
