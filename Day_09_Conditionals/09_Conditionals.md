<div align="center">
  <h1>Python In 30 Days: Day 9 - Conditionals</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 8](../Day_08_Dictionaries/08_Dictionaries.md) | [Day 10 >>](../Day_10_Loops/10_Loops.md)

**Python In 30 Days**

- [📘 Day 9](#-day-9)
  - [Conditionals](#conditionals)
    - [If Condition](#if-condition)
    - [If Else](#if-else)
    - [If Elif Else](#if-elif-else)
    - [Short Hand](#short-hand)
    - [Nested Conditions](#nested-conditions)
    - [If Condition and Logical Operators](#if-condition-and-logical-operators)
    - [If and Or Logical Operators](#if-and-or-logical-operators)
    - [Practical Conditional Patterns](#practical-conditional-patterns)
    - [Truthiness in Python](#truthiness-in-python)
  - [💻 Exercises: Day 9](#-exercises-day-9)
    - [Exercises: Level 1](#exercises-level-1)
    - [Exercises: Level 2](#exercises-level-2)
    - [Exercises: Level 3](#exercises-level-3)

# 📘 Day 9

## Conditionals

Python normally executes statements from top to bottom. Conditional statements allow the program to choose which block of code should run based on whether a condition is `True` or `False`.

The main conditional keywords are:

- `if`: runs code when a condition is true.
- `elif`: checks another condition when the previous condition was false.
- `else`: runs when none of the preceding conditions are true.

### If Condition

The `if` keyword checks whether a condition is true and executes the indented block when it is.

Remember the indentation after the colon.

```py
# syntax
if condition:
    code
```

**Example:**

```py
a = 3

if a > 0:
    print('A is a positive number')

# A is a positive number
```

If the condition is false, the indented block is skipped.

### If Else

Use `else` when you want one block to run when the `if` condition is true and another block to run when it is false.

```py
# syntax
if condition:
    code_if_true
else:
    code_if_false
```

**Example:**

```py
a = 3

if a < 0:
    print('A is a negative number')
else:
    print('A is a positive number')
```

### If Elif Else

Use `elif` when you need to check multiple conditions.

```py
# syntax
if condition:
    code
elif condition:
    code
else:
    code
```

**Example:**

```py
a = 0

if a > 0:
    print('A is a positive number')
elif a < 0:
    print('A is a negative number')
else:
    print('A is zero')
```

Python checks the conditions from top to bottom. Once one condition is true, its block runs and the remaining `elif` conditions are skipped.

### Short Hand

A conditional expression can be written on one line:

```py
# syntax
value_if_true if condition else value_if_false
```

**Example:**

```py
a = 3

result = 'A is positive' if a > 0 else 'A is negative or zero'
print(result)
```

The short-hand form is useful for simple expressions. For complex logic, a normal `if/else` block is easier to read.

### Nested Conditions

A conditional statement can contain another conditional statement.

```py
a = 0

if a > 0:
    if a % 2 == 0:
        print('A is a positive and even integer')
    else:
        print('A is a positive odd integer')
elif a == 0:
    print('A is zero')
else:
    print('A is a negative number')
```

Nested conditions are useful when the second decision depends on the first decision.

However, deeply nested conditions can become difficult to read. Logical operators can often simplify them.

### If Condition and Logical Operators

The `and` operator requires both conditions to be true.

```py
# syntax
if condition1 and condition2:
    code
```

**Example:**

```py
a = 0

if a > 0 and a % 2 == 0:
    print('A is an even and positive integer')
elif a > 0 and a % 2 != 0:
    print('A is a positive integer')
elif a == 0:
    print('A is zero')
else:
    print('A is negative')
```

### If and Or Logical Operators

The `or` operator requires at least one condition to be true.

```py
# syntax
if condition1 or condition2:
    code
```

**Example:**

```py
user = 'James'
access_level = 3

if user == 'admin' or access_level >= 4:
    print('Access granted!')
else:
    print('Access denied!')
```

Here, access is granted if either the user is `admin` or the access level is at least `4`.

## Practical Conditional Patterns

Conditionals are commonly used to validate data and make decisions.

### Checking a Range

```py
score = 85

if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'F'

print(grade)  # B
```

Notice that the conditions are checked from highest to lowest. The first matching condition wins.

### Validating User Input

```py
age = int(input('Enter your age: '))

if age < 0:
    print('Age cannot be negative')
elif age >= 18:
    print('You are an adult')
else:
    print('You are a minor')
```

### Combining Conditions

```py
age = 25
has_id = True

if age >= 18 and has_id:
    print('Access granted')
else:
    print('Access denied')
```

## Truthiness in Python

Python conditions do not always have to be explicit comparisons. Python evaluates many values as either **truthy** or **falsy**.

Common falsy values include:

```py
False
None
0
0.0
''
[]
()
{}
set()
```

Most other values are truthy.

Example:

```py
name = ''

if name:
    print('Name was provided')
else:
    print('Name is empty')
```

This is useful when checking whether a string, list, dictionary, or other collection contains a value.

**Practical tip:** Prefer clear conditions. For example:

```py
if items:
    print('Items are available')
```

is usually clearer than:

```py
if len(items) > 0:
    print('Items are available')
```

## 💻 Exercises: Day 9

### Exercises: Level 1

1. Get user input using `input("Enter your age: ")`. If the user is 18 or older, print:

```text
You are old enough to learn to drive.
```

If the user is below 18, print how many more years they need to wait.

Example:

```text
Enter your age: 15
You need 3 more years to learn to drive.
```

2. Compare `my_age` and `your_age` using `if ... else`. Determine who is older. Use `input("Enter your age: ")` to get the user's age. If the difference is 1, use `year`; otherwise use `years`. If both ages are equal, print a suitable message.

3. Get two numbers from the user. Compare them and print whether the first number is greater than, less than, or equal to the second number.

Example:

```text
Enter number one: 4
Enter number two: 3
4 is greater than 3
```

### Exercises: Level 2

1. Write a program that gives a grade according to a student's score:

```text
90-100, A
80-89, B
70-79, C
60-69, D
0-59, F
```

2. Get a month from the user and determine the season:

```text
September, October, November -> Autumn
December, January, February -> Winter
March, April, May -> Spring
June, July, August -> Summer
```

3. The following list contains some fruits:

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
```

Ask the user for a fruit. If it does not exist in the list, add it and print the modified list. If it already exists, print:

```text
That fruit already exists in the list.
```

### Exercises: Level 3

1. Use the following person dictionary. Feel free to modify it:

```py
person = {
    'first_name': 'Amit',
    'last_name': 'Kumar',
    'age': 25,
    'country': 'India',
    'is_married': False,
    'skills': ['Python', 'SQL', 'PySpark', 'Databricks'],
    'address': {
        'city': 'Mumbai',
        'zipcode': '400001'
    }
}
```

Complete the following:

- Check whether the `person` dictionary has a `skills` key. If it does, print the middle skill in the skills list.
- Check whether the person has the `Python` skill and print the result.
- If the person has only JavaScript and React, print `He is a front end developer`.
- If the person has Node, Python, and MongoDB, print `He is a backend developer`.
- If the person has React, Node, and MongoDB, print `He is a fullstack developer`.
- Otherwise, print `unknown title`.
- If the person is married and lives in India, print information in this format:

```text
Amit Kumar lives in India. He is married.
```

### Extra Practice

4. Write a program that checks whether a number is positive, negative, or zero.

5. Write a program that checks whether a number is even or odd.

6. Write a program that checks whether a user has permission based on:

```py
is_admin = False
has_permission = True
```

7. Write a program that accepts a temperature and prints:

```text
Below 10 -> Cold
10-24 -> Cool
25-34 -> Warm
35 or above -> Hot
```

8. Write a program that checks whether a list is empty using truthiness.

9. Write a program that validates a username:

- It must not be empty.
- It must contain at least 3 characters.
- Otherwise, print an appropriate error message.

🎉 CONGRATULATIONS! 🎉

[<< Day 8](../Day_08_Dictionaries/08_Dictionaries.md) | [Day 10 >>](../Day_10_Loops/10_Loops.md)
