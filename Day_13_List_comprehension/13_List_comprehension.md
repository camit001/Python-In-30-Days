<div align="center">
  <h1>Python In 30 Days: Day 13 - List Comprehension</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 12](../Day_12_Modules/12_Modules.md) | [Day 14 >>](../Day_14_Higher_order_functions/14_Higher_order_functions.md)

**Python In 30 Days**

- [📘 Day 13](#-day-13)
  - [List Comprehension](#list-comprehension)
    - [Basic Syntax](#basic-syntax)
    - [Transforming Values](#transforming-values)
    - [Filtering Values](#filtering-values)
    - [Conditional Expressions](#conditional-expressions)
    - [Nested List Comprehensions](#nested-list-comprehensions)
    - [Flattening Nested Lists](#flattening-nested-lists)
    - [Set and Dictionary Comprehensions](#set-and-dictionary-comprehensions)
    - [When Not to Use Comprehensions](#when-not-to-use-comprehensions)
  - [Lambda Function](#lambda-function)
    - [Creating a Lambda Function](#creating-a-lambda-function)
    - [Lambda Function Inside Another Function](#lambda-function-inside-another-function)
    - [Lambda Functions with Built-in Functions](#lambda-functions-with-built-in-functions)
  - [💻 Exercises: Day 13](#-exercises-day-13)

# 📘 Day 13

## List Comprehension

List comprehension is a compact way to create a new list from an iterable.

Instead of writing a complete `for` loop to build a list, we can often express the same operation in one readable line.

### Basic Syntax

The general syntax is:

```py
[expression for item in iterable]
```

A condition can also be added:

```py
[expression for item in iterable if condition]
```

Think of it as:

```text
Take each item
    ↓
Optionally check a condition
    ↓
Create a new value
    ↓
Put that value into a new list
```

### Example: Creating a List of Characters

```py
language = 'Python'

lst = list(language)

print(lst)
# ['P', 'y', 't', 'h', 'o', 'n']
```

The same result can be produced with a list comprehension:

```py
lst = [letter for letter in language]

print(lst)
# ['P', 'y', 't', 'h', 'o', 'n']
```

### Example: Generating Numbers

```py
numbers = [i for i in range(11)]

print(numbers)
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

A traditional loop would be:

```py
numbers = []

for i in range(11):
    numbers.append(i)
```

Both approaches produce the same result.

---

## Transforming Values

A list comprehension can transform every item in an iterable.

### Squares

```py
squares = [i * i for i in range(11)]

print(squares)
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

Using exponentiation:

```py
squares = [i ** 2 for i in range(11)]
```

### Creating Tuples

The expression does not have to return a single number. It can return a tuple.

```py
numbers = [(i, i * i) for i in range(6)]

print(numbers)
# [(0, 0), (1, 1), (2, 4), (3, 9), (4, 16), (5, 25)]
```

### Transforming Strings

```py
names = ['amit', 'rahul', 'priya']

upper_names = [name.upper() for name in names]

print(upper_names)
# ['AMIT', 'RAHUL', 'PRIYA']
```

---

## Filtering Values

A condition can be added after the `for` clause.

```py
[expression for item in iterable if condition]
```

### Even Numbers

```py
even_numbers = [i for i in range(21) if i % 2 == 0]

print(even_numbers)
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

### Odd Numbers

```py
odd_numbers = [i for i in range(21) if i % 2 != 0]

print(odd_numbers)
# [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
```

### Positive Even Numbers

```py
numbers = [-8, -7, -3, -1, 0, 1, 3, 4, 5, 7, 6, 8, 10]

positive_even_numbers = [
    i for i in numbers
    if i > 0 and i % 2 == 0
]

print(positive_even_numbers)
# [4, 6, 8, 10]
```

Notice that the original example's expected output did not match its input. There is no `2` in the input list, so the correct result is `[4, 6, 8, 10]`. Tiny data mistakes are how computers acquire their reputation for being difficult.

---

## Conditional Expressions

A conditional expression can be used inside a list comprehension when you want to transform every item differently depending on a condition.

Syntax:

```py
[value_if_true if condition else value_if_false for item in iterable]
```

Example:

```py
numbers = [1, 2, 3, 4, 5]

labels = [
    'even' if number % 2 == 0 else 'odd'
    for number in numbers
]

print(labels)
# ['odd', 'even', 'odd', 'even', 'odd']
```

Another example:

```py
numbers = [-2, -1, 0, 1, 2]

result = [
    'positive' if number > 0
    else 'negative' if number < 0
    else 'zero'
    for number in numbers
]

print(result)
# ['negative', 'negative', 'zero', 'positive', 'positive']
```

For complicated conditions, a normal `for` loop is usually easier to understand.

---

## Nested List Comprehensions

A list comprehension can contain more than one `for` clause.

```py
pairs = [
    (x, y)
    for x in range(3)
    for y in range(3)
]

print(pairs)
```

Output:

```text
[(0, 0), (0, 1), (0, 2),
 (1, 0), (1, 1), (1, 2),
 (2, 0), (2, 1), (2, 2)]
```

This is equivalent to:

```py
pairs = []

for x in range(3):
    for y in range(3):
        pairs.append((x, y))
```

Nested comprehensions are powerful, but readability should come first.

---

## Flattening Nested Lists

List comprehensions are useful for flattening a two-dimensional list.

```py
list_of_lists = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

flattened_list = [
    number
    for row in list_of_lists
    for number in row
]

print(flattened_list)
# [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

The equivalent nested loop is:

```py
flattened_list = []

for row in list_of_lists:
    for number in row:
        flattened_list.append(number)
```

---

## Set and Dictionary Comprehensions

List comprehensions are not the only comprehensions available in Python.

### Set Comprehension

Use `{}` with an expression and `for` to create a set.

```py
numbers = [1, 2, 2, 3, 3, 4]

unique_squares = {number ** 2 for number in numbers}

print(unique_squares)
# {1, 4, 9, 16}
```

Sets automatically remove duplicate values.

### Dictionary Comprehension

Dictionary comprehensions create key-value pairs.

```py
numbers = range(1, 6)

squares = {
    number: number ** 2
    for number in numbers
}

print(squares)
# {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

Filtering can also be used:

```py
even_squares = {
    number: number ** 2
    for number in range(1, 11)
    if number % 2 == 0
}

print(even_squares)
# {2: 4, 4: 16, 6: 36, 8: 64, 10: 100}
```

---

## When Not to Use Comprehensions

Comprehensions are excellent for short and clear transformations, but they are not automatically better than loops.

Avoid overly complicated comprehensions such as:

```py
result = [
    complicated_function(x, y)
    for x in data
    for y in other_data
    if complex_condition(x, y)
]
```

If a comprehension becomes difficult to read, use a normal loop:

```py
result = []

for x in data:
    for y in other_data:
        if complex_condition(x, y):
            result.append(complicated_function(x, y))
```

**Rule of thumb:**

> Use a comprehension when it makes the code shorter **and** easier to understand.

---

# Lambda Function

A lambda function is a small anonymous function.

A lambda can accept multiple arguments, but its body must contain a single expression. The expression's result is returned automatically.

Lambda syntax:

```py
lambda parameters: expression
```

A lambda is useful when a short function is needed temporarily, especially when passing a function to another function.

## Creating a Lambda Function

A normal function:

```py
def add_two_nums(a, b):
    return a + b

print(add_two_nums(2, 3))
# 5
```

The same operation with a lambda:

```py
add_two_nums = lambda a, b: a + b

print(add_two_nums(2, 3))
# 5
```

### Square and Cube

```py
square = lambda x: x ** 2
cube = lambda x: x ** 3

print(square(3))
# 9

print(cube(3))
# 27
```

### Multiple Variables

```py
multiple_variable = lambda a, b, c: a ** 2 - 3 * b + 4 * c

print(multiple_variable(5, 5, 3))
# 22
```

### Immediately Invoked Lambda

A lambda can be created and called immediately:

```py
result = (lambda a, b: a + b)(2, 3)

print(result)
# 5
```

This is valid Python, but it is uncommon. Usually a named function or a lambda passed to another function is clearer.

---

## Lambda Function Inside Another Function

A function can return another function.

```py
def power(x):
    return lambda n: x ** n

cube = power(2)(3)

print(cube)
# 8

two_power_of_five = power(2)(5)

print(two_power_of_five)
# 32
```

Here:

```py
power(2)
```

returns a lambda function, and:

```py
power(2)(3)
```

calls that returned function with `3`.

This is an example of a function remembering a value from its surrounding scope.

---

## Lambda Functions with Built-in Functions

Lambda functions are especially useful with functions such as `sorted()`, `map()`, and `filter()`.

### `sorted()` with Lambda

Sort employees by salary:

```py
employees = [
    {'name': 'Amit', 'salary': 70000},
    {'name': 'Rahul', 'salary': 50000},
    {'name': 'Priya', 'salary': 90000}
]

employees_by_salary = sorted(
    employees,
    key=lambda employee: employee['salary']
)

print(employees_by_salary)
```

Descending order:

```py
employees_by_salary = sorted(
    employees,
    key=lambda employee: employee['salary'],
    reverse=True
)
```

### `map()` with Lambda

`map()` applies a function to each item.

```py
numbers = [1, 2, 3, 4, 5]

squares = list(map(lambda x: x ** 2, numbers))

print(squares)
# [1, 4, 9, 16, 25]
```

For simple transformations, a list comprehension is often more readable:

```py
squares = [x ** 2 for x in numbers]
```

### `filter()` with Lambda

`filter()` keeps items for which the function returns `True`.

```py
numbers = [1, 2, 3, 4, 5, 6]

even_numbers = list(
    filter(lambda x: x % 2 == 0, numbers)
)

print(even_numbers)
# [2, 4, 6]
```

Again, a list comprehension is often clearer:

```py
even_numbers = [x for x in numbers if x % 2 == 0]
```

---

## Practical Data Engineering Example

List comprehensions and lambdas are useful for simple data transformations.

```py
employees = [
    {'name': ' amit ', 'department': 'data engineering'},
    {'name': ' rahul ', 'department': 'analytics'},
    {'name': ' priya ', 'department': 'data engineering'}
]

cleaned_names = [
    employee['name'].strip().title()
    for employee in employees
]

print(cleaned_names)
# ['Amit', 'Rahul', 'Priya']
```

Filtering records:

```py
data_engineers = [
    employee
    for employee in employees
    if employee['department'] == 'data engineering'
]

print(data_engineers)
```

Sorting records:

```py
employees = [
    {'name': 'Amit', 'salary': 70000},
    {'name': 'Rahul', 'salary': 50000},
    {'name': 'Priya', 'salary': 90000}
]

sorted_employees = sorted(
    employees,
    key=lambda employee: employee['salary']
)

print(sorted_employees)
```

These patterns appear frequently when preparing data before loading it into another system.

---

## 💻 Exercises: Day 13

### Exercises: Level 1

1. Filter only negative and zero values from the list using list comprehension:

```py
numbers = [-4, -3, -2, -1, 0, 2, 4, 6]
```

Expected output:

```py
[-4, -3, -2, -1, 0]
```

2. Flatten the following list of lists into a one-dimensional list:

```py
list_of_lists = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Output:
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

3. Using list comprehension, create the following list of tuples:

```py
[
    (0, 1, 0, 0, 0, 0, 0),
    (1, 1, 1, 1, 1, 1, 1),
    (2, 1, 2, 4, 8, 16, 32),
    (3, 1, 3, 9, 27, 81, 243),
    (4, 1, 4, 16, 64, 256, 1024),
    (5, 1, 5, 25, 125, 625, 3125),
    (6, 1, 6, 36, 216, 1296, 7776),
    (7, 1, 7, 49, 343, 2401, 16807),
    (8, 1, 8, 64, 512, 4096, 32768),
    (9, 1, 9, 81, 729, 6561, 59049),
    (10, 1, 10, 100, 1000, 10000, 100000)
]
```

### Exercises: Level 2

4. Transform the following list into:

```py
countries = [
    [('Finland', 'Helsinki')],
    [('Sweden', 'Stockholm')],
    [('Norway', 'Oslo')]
]
```

Expected output:

```py
[
    ['FINLAND', 'FIN', 'HELSINKI'],
    ['SWEDEN', 'SWE', 'STOCKHOLM'],
    ['NORWAY', 'NOR', 'OSLO']
]
```

5. Change the following list into a list of dictionaries:

```py
countries = [
    [('Finland', 'Helsinki')],
    [('Sweden', 'Stockholm')],
    [('Norway', 'Oslo')]
]
```

Expected output:

```py
[
    {'country': 'FINLAND', 'city': 'HELSINKI'},
    {'country': 'SWEDEN', 'city': 'STOCKHOLM'},
    {'country': 'NORWAY', 'city': 'OSLO'}
]
```

6. Change the following list of lists into a list of concatenated strings:

```py
names = [
    [('Amit', 'Kumar')],
    [('David', 'Smith')],
    [('Donald', 'Trump')],
    [('Bill', 'Gates')]
]
```

Expected output:

```py
['Amit Kumar', 'David Smith', 'Donald Trump', 'Bill Gates']
```

7. Write a lambda function that calculates the slope of a linear function:

```text
y = mx + b
```

Given two points `(x1, y1)` and `(x2, y2)`, use:

```text
m = (y2 - y1) / (x2 - x1)
```

Handle the case where `x2 == x1`.

### Exercises: Level 3

8. Use a list comprehension to create a list of all numbers from `1` to `100` divisible by both `3` and `5`.

9. Use a dictionary comprehension to create a dictionary where numbers `1` to `10` are keys and their cubes are values.

10. Use a set comprehension to extract the unique first letters from:

```py
names = ['Amit', 'Anita', 'Rahul', 'Ravi', 'Priya']
```

11. Use `sorted()` with a lambda to sort employees by salary in descending order.

12. Use `filter()` with a lambda to keep only employees whose salary is greater than `60000`.

13. Use `map()` with a lambda to convert a list of Celsius temperatures to Fahrenheit.

14. Given a list of employee dictionaries, use a list comprehension to keep only employees from the `Data Engineering` department.

15. Write the same transformation once with a list comprehension and once with a normal `for` loop. Compare which version is easier to read.

16. Create a nested list comprehension that generates all `(x, y)` coordinate pairs for `x` and `y` from `0` to `4`.

🎉 CONGRATULATIONS! 🎉

[<< Day 12](../Day_12_Modules/12_Modules.md) | [Day 14 >>](../Day_14_Higher_order_functions/14_Higher_order_functions.md)
