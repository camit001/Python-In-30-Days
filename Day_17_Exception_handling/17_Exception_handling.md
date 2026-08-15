<div align="center">
  <h1>Python In 30 Days: Day 17 - Exception Handling</h1>

  <sub>Author:
  <a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
  </sub>
</div>

[<< Day 16](../Day_16_Python_date_time/16_Python_date_time.md) | [Day 18 >>](../Day_18_Regular_expressions/18_Regular_expressions.md)

**Python In 30 Days**

- [📘 Day 17](#-day-17)
  - [Exception Handling](#exception-handling)
    - [Try and Except](#try-and-except)
    - [Handling Specific Exceptions](#handling-specific-exceptions)
    - [else and finally](#else-and-finally)
    - [Raising Exceptions](#raising-exceptions)
    - [Custom Exception Messages](#custom-exception-messages)
  - [Packing and Unpacking Arguments in Python](#packing-and-unpacking-arguments-in-python)
    - [Unpacking](#unpacking)
      - [Unpacking Lists](#unpacking-lists)
      - [Unpacking Dictionaries](#unpacking-dictionaries)
    - [Packing](#packing)
      - [Packing Lists](#packing-lists)
      - [Packing Dictionaries](#packing-dictionaries)
  - [Spreading in Python](#spreading-in-python)
  - [Enumerate](#enumerate)
  - [Zip](#zip)
  - [Practical Data Engineering Example](#practical-data-engineering-example)
  - [Exercises: Day 17](#exercises-day-17)

# 📘 Day 17

## Exception Handling

Python uses `try` and `except` to handle exceptions gracefully.

An exception is an event that interrupts the normal execution of a program. Exceptions can happen because of incorrect input, invalid calculations, missing files, incorrect data types, unavailable resources, or many other conditions.

Instead of allowing the entire application to stop unexpectedly, we can catch appropriate exceptions and decide how the program should respond.

### Try and Except

Basic syntax:

```py
try:
    # code that may raise an exception
except:
    # code that runs if an exception occurs
```

Example:

```py
try:
    print(10 + '5')
except:
    print('Something went wrong')
```

Output:

```text
Something went wrong
```

The expression raises a `TypeError` because Python cannot add an integer and a string.

### Handling Specific Exceptions

It is usually better to catch the specific exception you expect instead of using a bare `except`.

```py
try:
    number = int(input('Enter a number: '))
    print(100 / number)
except ValueError:
    print('Please enter a valid number.')
except ZeroDivisionError:
    print('The number cannot be zero.')
```

This makes the program's error handling more precise.

### Example with User Input

```py
try:
    name = input('Enter your name: ')
    year_born = int(input('Year you were born: '))

    age = 2026 - year_born

    print(f'You are {name}. Your age is approximately {age}.')
except ValueError:
    print('Year of birth must be a valid number.')
```

Example:

```text
Enter your name: Amit
Year you were born: 2000
You are Amit. Your age is approximately 26.
```

The exact age depends on the current date and whether the person's birthday has occurred yet.

### Handling the Exception Object

We can store the exception in a variable using `as`.

```py
try:
    number = int('abc')
except ValueError as error:
    print('Error:', error)
```

Output:

```text
Error: invalid literal for int() with base 10: 'abc'
```

This is useful when logging or debugging an exception.

---

## `else` and `finally`

Python provides `else` and `finally` blocks for more control over exception handling.

```py
try:
    # code that may fail
except:
    # runs when an exception occurs
else:
    # runs when no exception occurs
finally:
    # always runs
```

Example:

```py
try:
    number = int(input('Enter a number: '))
    result = 100 / number
except ValueError:
    print('Please enter a valid number.')
except ZeroDivisionError:
    print('Zero is not allowed.')
else:
    print('Result:', result)
finally:
    print('Execution completed.')
```

### How They Work

- `try` contains code that may raise an exception.
- `except` handles an exception.
- `else` runs only when no exception occurred.
- `finally` runs whether an exception occurred or not.

`finally` is commonly used for cleanup operations such as closing resources.

---

## Raising Exceptions

We can intentionally raise an exception using the `raise` statement.

```py
age = -5

if age < 0:
    raise ValueError('Age cannot be negative.')
```

Output:

```text
ValueError: Age cannot be negative.
```

Raising exceptions is useful when a function receives invalid data.

Example:

```py
def calculate_square_root(number):
    if number < 0:
        raise ValueError('Number must not be negative.')

    return number ** 0.5

print(calculate_square_root(25))
```

---

## Custom Exception Messages

A function can validate its input and provide a meaningful error message.

```py
def withdraw(balance, amount):
    if amount <= 0:
        raise ValueError('Withdrawal amount must be greater than zero.')

    if amount > balance:
        raise ValueError('Insufficient balance.')

    return balance - amount

try:
    balance = withdraw(1000, 1200)
    print(balance)
except ValueError as error:
    print(error)
```

Output:

```text
Insufficient balance.
```

Good exception messages make debugging much easier.

---

# Packing and Unpacking Arguments in Python

Python uses two important operators for packing and unpacking:

- `*` for positional arguments
- `**` for keyword arguments

These operators are useful when passing a collection of values to a function or collecting an unknown number of arguments.

## Unpacking

### Unpacking Lists

Suppose a function expects five separate arguments:

```py
def sum_of_five_nums(a, b, c, d, e):
    return a + b + c + d + e
```

Passing a list directly does not work:

```py
lst = [1, 2, 3, 4, 5]

print(sum_of_five_nums(lst))
```

This raises a `TypeError` because the function expects five positional arguments.

Use `*` to unpack the list:

```py
lst = [1, 2, 3, 4, 5]

print(sum_of_five_nums(*lst))
```

Output:

```text
15
```

The list:

```py
[1, 2, 3, 4, 5]
```

is unpacked as if we had written:

```py
sum_of_five_nums(1, 2, 3, 4, 5)
```

### Unpacking with `range()`

```py
args = [2, 7]

numbers = range(*args)

print(list(numbers))
```

Output:

```text
[2, 3, 4, 5, 6]
```

### Extended Iterable Unpacking

A list or tuple can be unpacked into individual variables.

```py
countries = [
    'India',
    'Japan',
    'Nepal',
    'Sri Lanka',
    'Bhutan'
]

first, second, third, *rest = countries

print(first)
print(second)
print(third)
print(rest)
```

Output:

```text
India
Japan
Nepal
['Sri Lanka', 'Bhutan']
```

Another example:

```py
numbers = [1, 2, 3, 4, 5, 6, 7]

first, *middle, last = numbers

print(first)
print(middle)
print(last)
```

Output:

```text
1
[2, 3, 4, 5, 6]
7
```

---

### Unpacking Dictionaries

Use `**` to unpack a dictionary into keyword arguments.

```py
def unpacking_person_info(name, country, city, age):
    return (
        f'{name} lives in {country}, {city}. '
        f'He is {age} years old.'
    )

person = {
    'name': 'Amit',
    'country': 'India',
    'city': 'Mumbai',
    'age': 26
}

print(unpacking_person_info(**person))
```

Output:

```text
Amit lives in India, Mumbai. He is 26 years old.
```

The dictionary keys must match the function parameter names.

---

## Packing

Packing is the opposite of unpacking.

When a function does not know how many positional or keyword arguments it will receive, `*args` and `**kwargs` can collect them.

### Packing Lists

```py
def sum_all(*args):
    total = 0

    for number in args:
        total += number

    return total

print(sum_all(1, 2, 3))
# 6

print(sum_all(1, 2, 3, 4, 5, 6, 7))
# 28
```

Inside the function, `args` is a tuple:

```py
def show_args(*args):
    print(type(args))
    print(args)

show_args(10, 20, 30)
```

Output:

```text
<class 'tuple'>
(10, 20, 30)
```

### Packing Dictionaries

`**kwargs` collects keyword arguments into a dictionary.

```py
def packing_person_info(**kwargs):
    for key, value in kwargs.items():
        print(f'{key} = {value}')

    return kwargs

print(
    packing_person_info(
        name='Amit',
        country='India',
        city='Mumbai',
        age=26
    )
)
```

Output:

```text
name = Amit
country = India
city = Mumbai
age = 26
{'name': 'Amit', 'country': 'India', 'city': 'Mumbai', 'age': 26}
```

Inside the function, `kwargs` is a dictionary.

---

# Spreading in Python

Python allows iterable unpacking when creating new collections or passing arguments.

For example:

```py
lst_one = [1, 2, 3]
lst_two = [4, 5, 6, 7]

lst = [0, *lst_one, *lst_two]

print(lst)
```

Output:

```text
[0, 1, 2, 3, 4, 5, 6, 7]
```

Another example:

```py
india_cities = ['Mumbai', 'Delhi', 'Pune']
other_cities = ['Bengaluru', 'Chennai']

cities = [*india_cities, *other_cities]

print(cities)
```

Output:

```text
['Mumbai', 'Delhi', 'Pune', 'Bengaluru', 'Chennai']
```

Dictionary unpacking can be used with `**`:

```py
employee = {
    'name': 'Amit',
    'department': 'Data Engineering'
}

location = {
    'city': 'Mumbai',
    'country': 'India'
}

employee_details = {
    **employee,
    **location
}

print(employee_details)
```

Output:

```text
{
    'name': 'Amit',
    'department': 'Data Engineering',
    'city': 'Mumbai',
    'country': 'India'
}
```

If duplicate dictionary keys are unpacked, the later value replaces the earlier value.

```py
first = {'name': 'Amit', 'age': 25}
second = {'age': 26}

result = {**first, **second}

print(result)
# {'name': 'Amit', 'age': 26}
```

---

# Enumerate

If we need both the index and the item while iterating, we can use `enumerate()`.

```py
countries = ['India', 'Japan', 'Nepal']

for index, country in enumerate(countries):
    print(index, country)
```

Output:

```text
0 India
1 Japan
2 Nepal
```

We can choose a different starting index:

```py
for index, country in enumerate(countries, start=1):
    print(index, country)
```

Output:

```text
1 India
2 Japan
3 Nepal
```

Practical example:

```py
countries = ['India', 'Japan', 'Nepal', 'Bhutan']

for index, country in enumerate(countries):
    if country == 'India':
        print(
            f'The country {country} '
            f'has been found at index {index}.'
        )
```

Output:

```text
The country India has been found at index 0.
```

---

# Zip

`zip()` allows us to iterate over multiple iterables at the same time.

```py
fruits = ['banana', 'orange', 'mango', 'lemon', 'lime']
vegetables = ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']

fruits_and_vegetables = []

for fruit, vegetable in zip(fruits, vegetables):
    fruits_and_vegetables.append({
        'fruit': fruit,
        'vegetable': vegetable
    })

print(fruits_and_vegetables)
```

Output:

```text
[
    {'fruit': 'banana', 'vegetable': 'Tomato'},
    {'fruit': 'orange', 'vegetable': 'Potato'},
    {'fruit': 'mango', 'vegetable': 'Cabbage'},
    {'fruit': 'lemon', 'vegetable': 'Onion'},
    {'fruit': 'lime', 'vegetable': 'Carrot'}
]
```

### Important

By default, `zip()` stops when the shortest iterable is exhausted.

```py
numbers = [1, 2, 3]
letters = ['A', 'B']

print(list(zip(numbers, letters)))
```

Output:

```text
[(1, 'A'), (2, 'B')]
```

---

# Practical Data Engineering Example

Packing, unpacking, `enumerate()`, and `zip()` are useful when processing structured data.

Suppose we have employee IDs and employee names:

```py
employee_ids = [101, 102, 103]
employee_names = ['Amit', 'Priya', 'Rahul']

employees = []

for employee_id, name in zip(employee_ids, employee_names):
    employees.append({
        'employee_id': employee_id,
        'name': name
    })

print(employees)
```

Output:

```text
[
    {'employee_id': 101, 'name': 'Amit'},
    {'employee_id': 102, 'name': 'Priya'},
    {'employee_id': 103, 'name': 'Rahul'}
]
```

We can use `enumerate()` to add a processing sequence:

```py
for sequence, employee in enumerate(employees, start=1):
    employee['sequence'] = sequence

print(employees)
```

Dictionary unpacking can be used to combine record data:

```py
base_record = {
    'source': 'employee_system',
    'country': 'India'
}

employee = {
    'employee_id': 101,
    'name': 'Amit'
}

final_record = {
    **base_record,
    **employee
}

print(final_record)
```

These techniques are useful in ETL and data-processing code when transforming rows or combining related data structures.

---

## Common Mistakes

### Mistake 1: Forgetting `*`

Incorrect:

```py
numbers = [1, 2, 3]

def add(a, b, c):
    return a + b + c

print(add(numbers))
```

Correct:

```py
print(add(*numbers))
```

### Mistake 2: Forgetting `**`

Incorrect:

```py
person = {
    'name': 'Amit',
    'country': 'India'
}

def introduce(name, country):
    return f'{name} lives in {country}.'

print(introduce(person))
```

Correct:

```py
print(introduce(**person))
```

### Mistake 3: Assuming `zip()` fills missing values

```py
a = [1, 2, 3]
b = ['A', 'B']

print(list(zip(a, b)))
```

Only two pairs are produced because the shortest iterable has two items.

---

🌕 You have completed Day 17. You now know how to handle exceptions, unpack and pack arguments, combine collections, and work with indexes and parallel iterables.

## Exercises: Day 17

### Level 1

1. Write a program that safely converts user input to an integer. Handle `ValueError`.
2. Write a program that divides two numbers and handles `ZeroDivisionError`.
3. Create a list and safely access an index supplied by the user. Handle `IndexError`.
4. Create a dictionary and safely access a key supplied by the user. Handle `KeyError`.
5. Write a function that accepts any number of positional arguments using `*args` and returns their sum.
6. Write a function that accepts any number of keyword arguments using `**kwargs` and prints each key-value pair.

### Level 2

7. `countries = ['India', 'Japan', 'Nepal', 'Bhutan', 'Sri Lanka']`. Unpack the first two countries into separate variables and store the remaining countries in `rest`.
8. Create a dictionary containing employee information and unpack it into a function using `**`.
9. Combine two lists using `*` unpacking.
10. Combine two dictionaries using `**` unpacking.
11. Use `enumerate()` to print the index and value of every item in a list.
12. Use `zip()` to combine employee names and salaries into a list of dictionaries.
13. Write a program using `try`, `except`, `else`, and `finally`.

### Level 3

14. Create a function that accepts a required employee ID, any number of positional values using `*args`, and optional keyword values using `**kwargs`.
15. Write a function that validates an employee record and raises `ValueError` when required fields are missing.
16. Use `zip()` to combine three lists: employee IDs, names, and departments.
17. Use `enumerate()` to create a sequence number for each record.
18. Build a small ETL-style example that:
    - Reads a list of employee records.
    - Handles invalid records with exceptions.
    - Adds a sequence number with `enumerate()`.
    - Combines related lists with `zip()`.
    - Creates the final records using dictionary unpacking.
19. Write a function that catches an exception, logs its message, and always performs cleanup in `finally`.

🎉 CONGRATULATIONS! 🎉

[<< Day 16](../Day_16_Python_date_time/16_Python_date_time.md) | [Day 18 >>](../Day_18_Regular_expressions/18_Regular_expressions.md)
