<div align="center">
  <h1>30 Days Of Python: Day 12 - Modules</h1>
  <sub>Author:
  <a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
  </sub>
</div>

[<< Day 11](../11_Day_Functions/11_Day_Functions.md) | [Day 13 >>](../13_Day_List_comprehension/13_list_comprehension.md)

**[30DaysOfPython]**

- [Day 12](#-day-12)
  - [Modules](#modules)
    - [What is a Module](#what-is-a-module)
    - [Creating a Module](#creating-a-module)
    - [Importing a Module](#importing-a-module)
    - [Import Functions from a Module](#import-functions-from-a-module)
    - [Import Functions from a Module and Renaming](#import-functions-from-a-module-and-renaming)
  - [Import Built-in Modules](#import-built-in-modules)
    - [OS Module](#os-module)
    - [Sys Module](#sys-module)
    - [Statistics Module](#statistics-module)
    - [Math Module](#math-module)
    - [String Module](#string-module)
    - [Random Module](#random-module)
  - [Exercises: Day 12](#-exercises-day-12)

# 📘 Day 12

## Modules

### What is a Module

A module is a file containing a set of codes or a set of functions which can be included to an application. A module could be a file containing a single variable, a function or a big code base.

### Creating a Module

To create a module we write our codes in a Python script and save it as a `.py` file.

```py
# mymodule.py
def generate_full_name(firstname, lastname):
    return firstname + ' ' + lastname
```

### Importing a Module

To import the file we use the `import` keyword.

```py
# main.py
import mymodule

print(mymodule.generate_full_name('Amit', 'Kumar'))
```

### Import Functions from a Module

```py
from mymodule import generate_full_name, sum_two_nums, person, gravity

print(generate_full_name('Amit', 'Kumar'))
print(sum_two_nums(1, 9))

mass = 100
weight = mass * gravity
print(weight)
print(person['firstname'])
```

### Import Functions from a Module and Renaming

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

## Import Built-in Modules

Some common built-in modules are `math`, `datetime`, `os`, `sys`, `random`, `statistics`, `collections`, `json`, and `re`.

### OS Module

```py
import os

os.mkdir('directory_name')
os.chdir('path')
os.getcwd()
os.rmdir('directory_name')
```

### Sys Module

The `sys` module provides functions and variables used to manipulate the Python runtime environment.

```py
import sys

print(sys.argv[0])
print(sys.argv[1])
print(sys.argv[2])
```

Example:

```sh
python script.py Amit 30DaysOfPython
```

Output:

```text
Welcome Amit. Enjoy 30DaysOfPython challenge!
```

Useful commands:

```py
sys.exit()
sys.maxsize
sys.path
sys.version
```

### Statistics Module

```py
from statistics import mean, median, mode, stdev

ages = [20, 20, 4, 24, 25, 22, 26, 20, 23, 22, 26]

print(mean(ages))
print(median(ages))
print(mode(ages))
print(stdev(ages))
```

### Math Module

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

### String Module

```py
import string

print(string.ascii_letters)
print(string.digits)
print(string.punctuation)
```

### Random Module

```py
from random import random, randint

print(random())
print(randint(5, 20))
```

## Personal Example

This example uses a custom module containing personal information.

```py
# mymodule.py

def create_profile():
    return {
        "name": "Amit Kumar",
        "country": "India",
        "city": "Mumbai"
    }
```

Then import it from `main.py`:

```py
# main.py

import mymodule

profile = mymodule.create_profile()

print("Name:", profile["name"])
print("Country:", profile["country"])
print("City:", profile["city"])
```

Output:

```text
Name: Amit Kumar
Country: India
City: Mumbai
```

## 💻 Exercises: Day 12

### Exercises: Level 1

1. Write a function which generates a six digit/character `random_user_id`.
2. Modify the previous task. Declare a function named `user_id_gen_by_user`. It takes two inputs using `input()`: number of characters and number of IDs.
3. Write a function named `rgb_color_gen` which generates RGB colors with values ranging from 0 to 255.

### Exercises: Level 2

1. Write a function `list_of_hexa_colors` which returns any number of hexadecimal colors.
2. Write a function `list_of_rgb_colors` which returns any number of RGB colors.
3. Write a function `generate_colors` which can generate any number of hexadecimal or RGB colors.

```py
generate_colors('hexa', 3)
generate_colors('hexa', 1)
generate_colors('rgb', 3)
generate_colors('rgb', 1)
```

### Exercises: Level 3

1. Create a function `shuffle_list` that takes a list and returns a shuffled list.
2. Write a function which returns an array of seven unique random numbers in the range 0-9.

🎉 CONGRATULATIONS! 🎉

[<< Day 11](../11_Day_Functions/11_Day_Functions.md) | [Day 13 >>](../13_Day_List_comprehension/13_list_comprehension.md)
