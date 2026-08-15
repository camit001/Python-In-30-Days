<div align="center">
  <h1>Python In 30 Days: Day 10 - Loops</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 9](../Day_09_Conditionals/09_Conditionals.md) | [Day 11 >>](../Day_11_Functions/11_Functions.md)

**Python In 30 Days**

- [📘 Day 10](#-day-10)
  - [Loops](#loops)
    - [While Loop](#while-loop)
    - [Break and Continue - Part 1](#break-and-continue---part-1)
    - [For Loop](#for-loop)
    - [Break and Continue - Part 2](#break-and-continue---part-2)
    - [The Range Function](#the-range-function)
    - [Nested For Loop](#nested-for-loop)
    - [For Else](#for-else)
    - [Pass](#pass)
    - [While True Loop](#while-true-loop)
    - [Enumerate](#enumerate)
    - [Zip](#zip)
    - [Reversed Iteration](#reversed-iteration)
    - [Looping Through Dictionary Items](#looping-through-dictionary-items)
    - [Looping With Conditions](#looping-with-conditions)
    - [Comprehensions](#comprehensions)
    - [Choosing the Right Loop](#choosing-the-right-loop)
  - [💻 Exercises: Day 10](#-exercises-day-10)

# 📘 Day 10

## Loops

Programs often need to repeat an operation multiple times. Python provides two primary loop statements:

1. `while` loop
2. `for` loop

Python does not have a separate `do...while` loop. When that behavior is needed, it can be created with `while True` and a `break` condition.

---

### While Loop

A `while` loop repeatedly executes a block of code while its condition is `True`.

```py
# syntax
while condition:
    code
```

**Example:**

```py
count = 0

while count < 5:
    print(count)
    count += 1

# 0
# 1
# 2
# 3
# 4
```

The condition becomes false when `count` reaches `5`, so the loop stops.

#### While Else

A `while` loop can have an `else` block. The `else` block runs when the loop finishes normally, but not when the loop is terminated by `break`.

```py
count = 0

while count < 5:
    print(count)
    count += 1
else:
    print('Loop completed')
```

---

### Break and Continue - Part 1

#### `break`

`break` immediately stops the current loop.

```py
count = 0

while count < 5:
    print(count)
    count += 1

    if count == 3:
        break
```

Output:

```text
0
1
2
```

#### `continue`

`continue` skips the rest of the current iteration and moves to the next iteration.

```py
count = 0

while count < 5:
    if count == 3:
        count += 1
        continue

    print(count)
    count += 1
```

Output:

```text
0
1
2
4
```

**Important:** When using `continue` in a `while` loop, make sure the loop variable is still updated. Otherwise, you may accidentally create an infinite loop.

---

### For Loop

A `for` loop iterates over an iterable such as a list, tuple, set, dictionary, string, or `range()` object.

```py
# syntax
for item in iterable:
    code
```

#### For Loop With a List

```py
numbers = [0, 1, 2, 3, 4, 5]

for number in numbers:
    print(number)
```

#### For Loop With a String

```py
language = 'Python'

for letter in language:
    print(letter)
```

You can also access characters by index:

```py
for i in range(len(language)):
    print(language[i])
```

#### For Loop With a Tuple

```py
numbers = (0, 1, 2, 3, 4, 5)

for number in numbers:
    print(number)
```

#### For Loop With a Set

```py
it_companies = {
    'Facebook',
    'Google',
    'Microsoft',
    'Apple',
    'IBM',
    'Oracle',
    'Amazon'
}

for company in it_companies:
    print(company)
```

Because sets are unordered, do not rely on the order in which their items are printed.

#### For Loop With a Dictionary

Looping directly through a dictionary gives its keys.

```py
person = {
    'first_name': 'Amit',
    'last_name': 'Kumar',
    'age': 25,
    'country': 'India',
    'skills': ['Python', 'SQL', 'PySpark'],
    'address': {
        'city': 'Mumbai',
        'zipcode': '400001'
    }
}

for key in person:
    print(key)
```

To get both keys and values:

```py
for key, value in person.items():
    print(key, value)
```

---

### Break and Continue - Part 2

#### `break` With a `for` Loop

```py
numbers = (0, 1, 2, 3, 4, 5)

for number in numbers:
    print(number)

    if number == 3:
        break
```

The loop stops as soon as `number` reaches `3`.

#### `continue` With a `for` Loop

```py
numbers = (0, 1, 2, 3, 4, 5)

for number in numbers:
    if number == 3:
        continue

    print(number)
```

Output:

```text
0
1
2
4
5
```

---

### The Range Function

The `range()` function generates a sequence of integers.

Its syntax is:

```py
range(start, stop, step)
```

- `start` is optional and defaults to `0`.
- `stop` is required and is **not included**.
- `step` is optional and defaults to `1`.

```py
print(list(range(5)))
# [0, 1, 2, 3, 4]

print(list(range(2, 7)))
# [2, 3, 4, 5, 6]

print(list(range(0, 11, 2)))
# [0, 2, 4, 6, 8, 10]

print(list(range(10, 0, -2)))
# [10, 8, 6, 4, 2]
```

`range()` returns a range object, not a list. Convert it to a list when you specifically need a list.

```py
for number in range(11):
    print(number)
```

This prints `0` through `10`.

---

### Nested For Loop

A loop can be placed inside another loop.

```py
for row in range(3):
    for column in range(3):
        print(row, column)
```

Nested loops are useful for working with grids, combinations, and nested data structures.

**Example:**

```py
person = {
    'name': 'Amit',
    'skills': ['Python', 'SQL', 'PySpark']
}

for key in person:
    if key == 'skills':
        for skill in person['skills']:
            print(skill)
```

---

### For Else

A `for` loop can have an `else` block.

The `else` block runs when the loop finishes normally. It does **not** run if the loop exits through `break`.

```py
for number in range(5):
    print(number)
else:
    print('Loop completed')
```

A common practical use is searching:

```py
numbers = [10, 20, 30, 40]
target = 30

for number in numbers:
    if number == target:
        print('Found')
        break
else:
    print('Not found')
```

Because `30` was found and `break` was executed, the `else` block does not run.

---

### Pass

`pass` does nothing. It is useful as a placeholder when Python requires a statement but you are not ready to write the implementation.

```py
for number in range(6):
    pass
```

It can also be used while designing a function:

```py
def process_data():
    pass
```

---

## While True Loop

Python does not have a `do...while` loop. A common alternative is `while True` with a `break`.

```py
while True:
    value = input('Enter q to quit: ')

    if value == 'q':
        break

    print('You entered:', value)
```

This is useful when the number of iterations is unknown and the program should decide when to stop.

**Warning:** A `while True` loop must have a reachable exit condition when you want it to terminate. Otherwise, it will continue indefinitely.

---

## Enumerate

`enumerate()` is useful when you need both the index and the value while iterating.

Without `enumerate()`:

```py
skills = ['Python', 'SQL', 'PySpark']

for i in range(len(skills)):
    print(i, skills[i])
```

With `enumerate()`:

```py
skills = ['Python', 'SQL', 'PySpark']

for index, skill in enumerate(skills):
    print(index, skill)
```

Output:

```text
0 Python
1 SQL
2 PySpark
```

You can choose the starting index:

```py
for index, skill in enumerate(skills, start=1):
    print(index, skill)
```

---

## Zip

`zip()` allows you to iterate over multiple iterables at the same time.

```py
names = ['Amit', 'Rahul', 'Priya']
scores = [90, 85, 95]

for name, score in zip(names, scores):
    print(name, score)
```

Output:

```text
Amit 90
Rahul 85
Priya 95
```

`zip()` stops when the shortest iterable is exhausted.

This is especially useful when working with related columns or parallel lists.

---

## Reversed Iteration

Use `reversed()` when you want to iterate over an iterable from the end toward the beginning.

```py
numbers = [1, 2, 3, 4, 5]

for number in reversed(numbers):
    print(number)
```

Output:

```text
5
4
3
2
1
```

For a range, a negative step is often clearer:

```py
for number in range(5, 0, -1):
    print(number)
```

---

## Looping Through Dictionary Items

Dictionaries are commonly processed using `items()`, `keys()`, or `values()`.

```py
employee = {
    'name': 'Amit Kumar',
    'department': 'Data Engineering',
    'location': 'Mumbai'
}

for key, value in employee.items():
    print(f'{key}: {value}')
```

Only keys:

```py
for key in employee:
    print(key)
```

Only values:

```py
for value in employee.values():
    print(value)
```

---

## Looping With Conditions

A loop can contain an `if` statement to process only matching values.

```py
numbers = range(1, 11)

for number in numbers:
    if number % 2 == 0:
        print(number)
```

Output:

```text
2
4
6
8
10
```

You can combine filtering and processing:

```py
employees = [
    {'name': 'Amit', 'age': 25},
    {'name': 'Rahul', 'age': 17},
    {'name': 'Priya', 'age': 30}
]

for employee in employees:
    if employee['age'] >= 18:
        print(employee['name'])
```

---

## Comprehensions

List comprehensions are a compact way to create a new list from an iterable.

Normal loop:

```py
squares = []

for number in range(1, 6):
    squares.append(number ** 2)

print(squares)
```

List comprehension:

```py
squares = [number ** 2 for number in range(1, 6)]

print(squares)
# [1, 4, 9, 16, 25]
```

With a condition:

```py
even_numbers = [
    number
    for number in range(1, 11)
    if number % 2 == 0
]

print(even_numbers)
# [2, 4, 6, 8, 10]
```

Do not use comprehensions for complicated multi-step logic. A normal loop is often easier to read.

---

## Choosing the Right Loop

| Situation | Recommended approach |
|---|---|
| Repeat while a condition is true | `while` |
| Iterate over items in a collection | `for` |
| Repeat a known number of times | `for` + `range()` |
| Stop the loop early | `break` |
| Skip the current iteration | `continue` |
| Need index + value | `enumerate()` |
| Iterate over multiple collections together | `zip()` |
| Iterate backward | `reversed()` or `range(..., -1)` |
| Search and detect whether `break` occurred | `for ... else` |
| Build a simple transformed list | List comprehension |
| Placeholder for future code | `pass` |

### A Simple Mental Model

```text
for      -> "Go through these items"
while    -> "Keep going while this is true"
break    -> "Stop now"
continue -> "Skip this one"
range    -> "Generate a sequence of numbers"
enumerate -> "Give me the index and value"
zip      -> "Give me matching items together"
```

🌕 You have completed Day 10 and learned how Python repeats, skips, stops, and controls execution. These loop patterns are foundational for data processing and automation. Now practice the exercises below.

## 💻 Exercises: Day 10

### Exercises: Level 1

1. Iterate from `0` to `10` using a `for` loop. Do the same using a `while` loop.
2. Iterate from `10` to `0` using a `for` loop. Do the same using a `while` loop.
3. Write a loop that prints the following triangle:

```text
#
##
###
####
#####
######
#######
```

4. Use nested loops to create the following:

```text
# # # # # # # #
# # # # # # # #
# # # # # # # #
# # # # # # # #
# # # # # # # #
# # # # # # # #
# # # # # # # #
# # # # # # # #
```

5. Print:

```text
0 x 0 = 0
1 x 1 = 1
2 x 2 = 4
3 x 3 = 9
4 x 4 = 16
5 x 5 = 25
6 x 6 = 36
7 x 7 = 49
8 x 8 = 64
9 x 9 = 81
10 x 10 = 100
```

6. Iterate through:

```py
['Python', 'NumPy', 'Pandas', 'Django', 'Flask']
```

using a `for` loop and print each item.

7. Use a `for` loop to iterate from `0` to `100` and print only even numbers.
8. Use a `for` loop to iterate from `0` to `100` and print only odd numbers.

### Exercises: Level 2

1. Use a `for` loop to iterate from `0` to `100` and print the sum of all numbers.

```text
The sum of all numbers is 5050.
```

2. Use a `for` loop to iterate from `0` to `100` and print the sum of all evens and the sum of all odds.

```text
The sum of all evens is 2550. And the sum of all odds is 2500.
```

### Extra Practice

3. Use `enumerate()` to print the position and value of every item in a list.
4. Use `zip()` to combine a list of employee names with their salaries.
5. Use a `while True` loop to repeatedly ask the user for input until they enter `q`.
6. Use `for ... else` to search for a number in a list and print `Not found` when it does not exist.
7. Reverse a list using `reversed()` and a loop.
8. Create a list of squares from `1` to `10` using a list comprehension.
9. Create a list containing only numbers divisible by `3` from `1` to `100`.
10. Use nested loops to print a multiplication table from `1` to `5`.

🎉 CONGRATULATIONS! 🎉

[<< Day 9](../Day_09_Conditionals/09_Conditionals.md) | [Day 11 >>](../Day_11_Functions/11_Functions.md)
