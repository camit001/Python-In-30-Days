<div align="center">
  <h1>Python In 30 Days: Day 12 - Modules</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 11](../Day_11_Functions/11_Functions.md) | [Day 13 >>](../Day_13_List_comprehension/13_List_comprehension.md)

**Python In 30 Days**

- [📘 Day 12](#-day-12)
  - [Modules](#modules)
    - [What is a Module](#what-is-a-module)
    - [Creating a Module](#creating-a-module)
    - [Importing a Module](#importing-a-module)
    - [Import Functions from a Module](#import-functions-from-a-module)
    - [Import Functions from a Module and Renaming](#import-functions-from-a-module-and-renaming)
    - [Using `if __name__ == "__main__"`](#using-if-__name__--__main__)
    - [Importing a Module with an Alias](#importing-a-module-with-an-alias)
  - [Import Built-in Modules](#import-built-in-modules)
    - [OS Module](#os-module)
    - [Sys Module](#sys-module)
    - [Statistics Module](#statistics-module)
    - [Math Module](#math-module)
    - [String Module](#string-module)
    - [Random Module](#random-module)
    - [Datetime Module](#datetime-module)
    - [JSON Module](#json-module)
    - [Collections Module](#collections-module)
    - [Regular Expression Module](#regular-expression-module)
  - [Installing Third-Party Packages](#installing-third-party-packages)
  - [Practical Module Structure](#practical-module-structure)
  - [Personal Example](#personal-example)
  - [💻 Exercises: Day 12](#-exercises-day-12)

# 📘 Day 12

## Modules

A module is a Python file containing reusable code such as functions, classes, variables, or constants.

Modules help us organize a large program into smaller files and reuse code across different programs.

A Python file becomes a module when another Python file imports it.

### What is a Module

A module can contain:

- Functions
- Variables
- Classes
- Constants
- Executable statements

For example:

```text
project/
├── main.py
└── mymodule.py
```

The `mymodule.py` file can contain reusable functions, and `main.py` can import and use them.

### Creating a Module

To create a module, write Python code in a `.py` file.

```py
# mymodule.py

def generate_full_name(firstname, lastname):
    return firstname + ' ' + lastname


def sum_two_nums(a, b):
    return a + b


gravity = 9.81

person = {
    'firstname': 'Amit',
    'lastname': 'Kumar'
}
```

### Importing a Module

Use the `import` keyword to import the complete module.

```py
# main.py

import mymodule

print(mymodule.generate_full_name('Amit', 'Kumar'))
print(mymodule.sum_two_nums(10, 20))
```

Using `mymodule.function_name()` makes it clear where the function came from.

### Import Functions from a Module

You can import only the functions or variables you need.

```py
from mymodule import generate_full_name, sum_two_nums, person, gravity

print(generate_full_name('Amit', 'Kumar'))
print(sum_two_nums(1, 9))

mass = 100
weight = mass * gravity

print(weight)
print(person['firstname'])
```

When importing specific names, you do not need to use the module name before them.

### Import Functions from a Module and Renaming

The `as` keyword allows you to give an imported name a different local name.

```py
from mymodule import (
    generate_full_name as fullname,
    sum_two_nums as total,
    person as p,
    gravity as g
)

print(fullname('Amit', 'Kumar'))
print(total(1, 9))

mass = 100
weight = mass * g

print(weight)
print(p)
print(p['firstname'])
```

Use aliases when a name is long, conflicts with another name, or is commonly abbreviated.

### Using `if __name__ == "__main__"`

A module can contain code that should run only when the file itself is executed, not when it is imported.

```py
# mymodule.py

def greet(name):
    return f'Hello, {name}!'


if __name__ == '__main__':
    print(greet('Amit'))
```

If you run:

```sh
python mymodule.py
```

the code inside the `if` block runs.

If another file imports `mymodule`:

```py
import mymodule
```

the code inside the `if __name__ == '__main__':` block does not run.

This pattern is very common in Python scripts and modules.

### Importing a Module with an Alias

You can give an entire module an alias:

```py
import mymodule as mm

print(mm.generate_full_name('Amit', 'Kumar'))
```

For standard libraries, aliases are also common:

```py
import math as m

print(m.sqrt(25))
```

Avoid unnecessary aliases because clear names make code easier to understand.

## Import Built-in Modules

Python provides many modules in its standard library. They can be imported without installing a separate package.

Common examples include:

- `math`
- `datetime`
- `os`
- `sys`
- `random`
- `statistics`
- `collections`
- `json`
- `re`

---

### OS Module

The `os` module provides functions for interacting with the operating system.

```py
import os

print(os.getcwd())
```

Create a directory:

```py
os.mkdir('directory_name')
```

Change the current working directory:

```py
os.chdir('path')
```

Remove an empty directory:

```py
os.rmdir('directory_name')
```

List files and directories:

```py
print(os.listdir())
```

Check whether a path exists:

```py
print(os.path.exists('directory_name'))
```

Join paths safely:

```py
file_path = os.path.join('data', 'employees.csv')
print(file_path)
```

**Practical tip:** `os.path` is useful when working with files and folders. For newer Python projects, `pathlib` is often an even cleaner option.

---

### Sys Module

The `sys` module provides access to variables and functionality related to the Python runtime.

```py
import sys

print(sys.version)
print(sys.maxsize)
print(sys.path)
```

Command-line arguments are available through `sys.argv`.

```py
import sys

print(sys.argv)
```

For example:

```sh
python script.py Amit 30
```

Then:

```py
# script.py

import sys

print(sys.argv[1])
print(sys.argv[2])
```

Output:

```text
Amit
30
```

Useful attributes and functions include:

```py
sys.version
sys.maxsize
sys.path
sys.argv
sys.exit()
```

**Warning:** Accessing `sys.argv[1]` when no argument was supplied raises an `IndexError`. Validate arguments when writing scripts intended for other users.

---

### Statistics Module

The `statistics` module provides common statistical calculations.

```py
from statistics import mean, median, mode, stdev

ages = [20, 20, 4, 24, 25, 22, 26, 20, 23, 22, 26]

print(mean(ages))
print(median(ages))
print(mode(ages))
print(stdev(ages))
```

These functions are useful for simple statistical calculations. For large-scale data processing, tools such as NumPy, pandas, or Spark may be more appropriate.

---

### Math Module

The `math` module provides mathematical functions and constants.

```py
import math

print(math.pi)
print(math.sqrt(2))
print(math.pow(2, 3))
print(math.floor(9.81))
print(math.ceil(9.81))
print(math.log10(100))
```

Specific functions can also be imported:

```py
from math import pi, sqrt, pow, floor, ceil, log10

print(pi)
print(sqrt(2))
print(pow(2, 3))
print(floor(9.81))
print(ceil(9.81))
print(log10(100))
```

Renaming is also possible:

```py
from math import pi as PI

print(PI)
```

---

### String Module

The `string` module provides useful string constants.

```py
import string

print(string.ascii_letters)
print(string.ascii_lowercase)
print(string.ascii_uppercase)
print(string.digits)
print(string.punctuation)
```

Example:

```py
import string

print('A' in string.ascii_uppercase)
print('5' in string.digits)
```

---

### Random Module

The `random` module generates pseudo-random values.

```py
from random import random, randint

print(random())
print(randint(5, 20))
```

Generate a random choice:

```py
import random

colors = ['red', 'green', 'blue']

print(random.choice(colors))
```

Shuffle a list:

```py
numbers = [1, 2, 3, 4, 5]

random.shuffle(numbers)

print(numbers)
```

For security-sensitive random values such as passwords or authentication tokens, use the `secrets` module instead of `random`.

---

### Datetime Module

The `datetime` module is used to work with dates and times.

```py
from datetime import datetime

now = datetime.now()

print(now)
print(now.year)
print(now.month)
print(now.day)
```

Create a specific date:

```py
from datetime import datetime

date = datetime(2026, 8, 15)

print(date)
```

Format a date:

```py
print(now.strftime('%Y-%m-%d'))
```

Common formatting codes:

```text
%Y -> four-digit year
%m -> two-digit month
%d -> two-digit day
%H -> hour
%M -> minute
%S -> second
```

---

### JSON Module

JSON is commonly used for exchanging structured data between applications.

```py
import json

employee = {
    'id': 101,
    'name': 'Amit Kumar',
    'department': 'Data Engineering'
}

json_data = json.dumps(employee)

print(json_data)
```

Convert JSON back into a Python object:

```py
python_data = json.loads(json_data)

print(python_data['name'])
```

Read JSON from a file:

```py
with open('employee.json', 'r') as file:
    employee = json.load(file)

print(employee)
```

Write JSON to a file:

```py
with open('employee.json', 'w') as file:
    json.dump(employee, file, indent=4)
```

JSON is especially important when working with REST APIs and data pipelines.

---

### Collections Module

The `collections` module provides specialized container types.

#### Counter

`Counter` is useful for counting values.

```py
from collections import Counter

fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']

counts = Counter(fruits)

print(counts)
print(counts['apple'])
```

#### defaultdict

`defaultdict` provides a default value for missing keys.

```py
from collections import defaultdict

groups = defaultdict(list)

groups['Data Engineering'].append('Amit')
groups['Data Engineering'].append('Priya')

print(groups)
```

#### deque

`deque` is useful when adding or removing items from both ends.

```py
from collections import deque

queue = deque(['A', 'B', 'C'])

queue.append('D')
queue.appendleft('Start')

print(queue)

queue.pop()
queue.popleft()

print(queue)
```

---

### Regular Expression Module

The `re` module provides regular-expression operations for searching and validating text.

```py
import re

text = 'Employee ID: 101'

match = re.search(r'\d+', text)

if match:
    print(match.group())
```

Output:

```text
101
```

Regular expressions are useful for tasks such as extracting patterns from text, validating simple formats, and cleaning data.

---

## Installing Third-Party Packages

Not every Python library is included in the standard library.

Third-party packages are commonly installed using `pip`:

```sh
pip install requests
```

Then import the package:

```py
import requests

response = requests.get('https://example.com')

print(response.status_code)
```

Check installed packages:

```sh
pip list
```

A project can record its dependencies in a `requirements.txt` file:

```text
requests
pandas
```

Then install them with:

```sh
pip install -r requirements.txt
```

**Important:** `pip` installs packages into a Python environment. Using a virtual environment is recommended for project-specific dependencies.

---

## Practical Module Structure

As projects grow, placing every function in one file becomes difficult to maintain.

A simple project can be organized like this:

```text
data_project/
│
├── main.py
├── utils.py
├── config.py
└── data/
    └── employees.json
```

For example:

```py
# utils.py

def clean_name(name):
    return name.strip().title()


def calculate_total(values):
    return sum(values)
```

Then use the functions from `main.py`:

```py
# main.py

from utils import clean_name, calculate_total

name = clean_name(' amit kumar ')
total = calculate_total([100, 200, 300])

print(name)
print(total)
```

This separation makes code easier to reuse, test, and maintain.

### Module vs Package

A **module** is usually a single `.py` file:

```text
utils.py
```

A **package** is a directory that organizes multiple Python modules.

```text
project/
├── main.py
└── utils/
    ├── __init__.py
    ├── strings.py
    └── numbers.py
```

Packages are useful when an application contains many related modules.

## Personal Example

This example uses a custom module containing personal information.

```py
# mymodule.py

def create_profile():
    return {
        'name': 'Amit Kumar',
        'country': 'India',
        'city': 'Mumbai'
    }
```

Then import it from `main.py`:

```py
# main.py

import mymodule

profile = mymodule.create_profile()

print('Name:', profile['name'])
print('Country:', profile['country'])
print('City:', profile['city'])
```

Output:

```text
Name: Amit Kumar
Country: India
City: Mumbai
```

## 💻 Exercises: Day 12

### Exercises: Level 1

1. Write a function that generates a six-character `random_user_id`.
2. Modify the previous task. Declare a function named `user_id_gen_by_user`. It takes two inputs using `input()`: the number of characters and the number of IDs.
3. Write a function named `rgb_color_gen` that generates RGB colors with values ranging from `0` to `255`.
4. Import the `math` module and use `sqrt`, `floor`, and `ceil` on different numbers.
5. Use the `datetime` module to print the current date and time.
6. Use the `os` module to print the current working directory and list the files in it.

### Exercises: Level 2

1. Write a function `list_of_hexa_colors` that returns any number of hexadecimal colors.
2. Write a function `list_of_rgb_colors` that returns any number of RGB colors.
3. Write a function `generate_colors` that can generate any number of hexadecimal or RGB colors.

```py
generate_colors('hexa', 3)
generate_colors('hexa', 1)
generate_colors('rgb', 3)
generate_colors('rgb', 1)
```

4. Create a JSON object containing employee information and convert it between Python and JSON using `json.dumps()` and `json.loads()`.
5. Use `Counter` to find the frequency of each item in a list.
6. Create a custom module named `utils.py` and import at least two functions from it into `main.py`.

### Exercises: Level 3

1. Create a function `shuffle_list` that takes a list and returns a shuffled list.
2. Write a function that returns an array of seven unique random numbers in the range `0-9`.
3. Create a custom module containing functions for cleaning and validating employee data. Import and use those functions from another Python file.
4. Write a small command-line program that reads a name and age from `sys.argv` and prints a formatted message.
5. Create a JSON file containing several employees. Write a Python program that reads the file, processes the records, and prints employees belonging to a selected department.
6. Use `re` to extract all numbers from a string.

🎉 CONGRATULATIONS! 🎉

[<< Day 11](../Day_11_Functions/11_Functions.md) | [Day 13 >>](../Day_13_List_comprehension/13_List_comprehension.md)
