
<div align="center">
  <h1> Python In 30 Days: Day 2 - Variables and Built-in Functions</h1>
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

**[<< Day 1](../Day_01_Introduction/01_Introduction.md) | [Day 3 >>](../Day_03_Operators/03_Operators.md)**

Python In 30 Days

- [📘 Day 2](#-day-2)
  - [Built in functions](#built-in-functions)
  - [Variables](#variables)
    - [Declaring Multiple Variable in a Line](#declaring-multiple-variable-in-a-line)
  - [Data Types](#data-types)
  - [Checking Data types and Casting](#checking-data-types-and-casting)
  - [Numbers](#numbers)
  - [💻 Exercises - Day 2](#-exercises---day-2)
    - [Exercises: Level 1](#exercises-level-1)
    - [Exercises: Level 2](#exercises-level-2)

# 📘 Day 2

## Built-in Functions

In Python we have lots of built-in functions. Built-in functions are globally available for your use that mean you can make use of the built-in functions without importing or configuring. Some of the most commonly used Python built-in functions are the following: _print()_, _len()_, _type()_, _int()_, _float()_, _str()_, _input()_, _list()_, _dict()_, _min()_, _max()_, _sum()_, _sorted()_, _open()_, _file()_, _help()_, and _dir()_. In the following table you will see an exhaustive list of Python built-in functions taken from [python documentation](https://docs.python.org/3/library/functions.html).


## Variables

Variables store data in a computer memory. Mnemonic variables are recommended to use in many programming languages. A mnemonic variable is a variable name that can be easily remembered and associated. A variable refers to a memory address in which data is stored.
A variable name cannot start with a number and cannot contain spaces, hyphens, or most special characters. A variable can have a short name (like x, y, z), but a more descriptive name (first_name, last_name, age, country) is recommended.

Python Variable Name Rules

- A variable name must start with a letter or the underscore character
- A variable name cannot start with a number
- A variable name can only contain letters, numbers, and underscores (A-Z, a-z, 0-9, and `_`)
- Variable names are case-sensitive (firstname, Firstname, FirstName and FIRSTNAME) are different variables)

Here are some example of valid variable names:

```shell
firstname
lastname
age
country
city
first_name
last_name
capital_city
_if # if we want to use reserved word as a variable
year_2026
year2026
current_year_2026
birth_year
num1
num2
```

Invalid variables names

```shell
first-name
first@name
first$name
num-1
1num
```

We will use standard Python variable naming style which has been adopted by many Python developers. Python developers commonly use the snake_case naming convention. We use underscore character after each word for a variable containing more than one word(eg. first_name, last_name, engine_rotation_speed).  The examples below follow the standard naming convention. An underscore separates words when a variable name contains more than one word.

When we assign a value to a variable, it is called variable assignment. For instance in the example below my first name is assigned to a variable first_name. The equal sign (`=`) is the assignment operator. Assignment means storing a value in a variable. The equal sign in Python is not equality as in Mathematics.

_Example:_

```py
# Variables in Python
first_name = 'Amit'
last_name = 'Kumar'
country = 'India'
city = 'Mumbai'
age = 25
is_married = True
skills = ['HTML', 'CSS', 'JS', 'React', 'Python']
person_info = {
   'firstname':'Amit',
   'lastname':'Kumar',
   'country':'India',
   'city':'Mumbai'
   }
```

Let us use the _print()_ and _len()_ built-in functions. Print function takes unlimited number of arguments. An argument is a value which we can be passed or put inside the function parenthesis, see the example below.

**Example:**

```py
print('Hello, World!') # The text Hello, World! is an argument
print('Hello',',', 'World','!') # it can take multiple arguments, four arguments have been passed
print(len('Hello, World!')) # it takes only one argument
```

Let us print and also find the length of the variables declared at the top:

**Example:**

```py
# Printing the values stored in the variables

print('First name:', first_name)
print('First name length:', len(first_name))
print('Last name: ', last_name)
print('Last name length: ', len(last_name))
print('Country: ', country)
print('City: ', city)
print('Age: ', age)
print('Married: ', is_married)
print('Skills: ', skills)
print('Person information: ', person_info)
```

### Declaring Multiple Variables in One Line

Multiple variables can also be declared in one line:

**Example:**

```py
first_name, last_name, country, age, is_married = 'Amit', 'Kumar', 'India', 250, True

print(first_name, last_name, country, age, is_married)
print('First name:', first_name)
print('Last name: ', last_name)
print('Country: ', country)
print('Age: ', age)
print('Married: ', is_married)
```

Getting user input using the _input()_ built-in function. Let us assign the data we get from a user into first_name and age variables.
**Example:**

```py
first_name = input('What is your name: ')
age = input('How old are you? ')

print(first_name)
print(age)
```

## Data Types

There are several data types in Python. To identify the data type we use the _type_ built-in function. I would like to ask you to focus on understanding different data types very well. When it comes to programming, it is all about data types. I introduced data types at the very beginning and it comes again, because every topic is related to data types. We will cover data types in more detail in their respective sections.

## Checking Data types and Casting

- Check Data types: To check the data type of certain data/variable we use the _type_
  **Examples:**

```py
# Different python data types
# Let's declare variables with various data types

first_name = 'Amit'     # str
last_name = 'Kumar'       # str
country = 'India'         # str
city= 'Mumbai'            # str
age = 25                   # int, it is an example age

# Printing out types
print(type('Amit'))          # str
print(type(first_name))          # str
print(type(10))                  # int
print(type(3.14))                # float
print(type(1 + 1j))              # complex
print(type(True))                # bool
print(type([1, 2, 3, 4]))        # list
print(type({'name':'Amit'})) # dict
print(type((1,2)))               # tuple
print(type(zip([1,2],[3,4])))    # zip
```

- Casting: Converting one data type to another data type. We use `int()`, `float()`, `str()`, `list()`, and `set()`
  When performing arithmetic operations, strings containing numbers should first be converted to `int` or `float`; otherwise, Python may raise a `TypeError`. If we concatenate a number with a string, the number should first be converted to a string. We will talk about concatenation in String section.

  **Examples:**

```py
# int to float
num_int = 10
print('num_int',num_int)         # 10
num_float = float(num_int)
print('num_float:', num_float)   # 10.0

# float to int
gravity = 9.81
print(int(gravity))             # 9

# int to str
num_int = 10
print(num_int)                  # 10
num_str = str(num_int)
print(num_str)                  # '10'

# str to int or float
num_str = '10.6'
num_float = float(num_str)  # Convert the string to a float first
num_int = int(num_float)    # Then convert the float to an integer
print('num_int', int(num_str))      # 10
print('num_float', float(num_str))  # 10.6
num_int = int(num_float)
print('num_int', int(num_int))      # 10

# str to list
first_name = 'Amit'
print(first_name)               # 'Amit'
first_name_to_list = list(first_name)
print(first_name_to_list)            # ['A', 'm', 'i', 't']
```

## Numbers

Number data types in Python:

1. Integers: Integer(negative, zero and positive) numbers
   Example:
   ... -3, -2, -1, 0, 1, 2, 3 ...

2. Floating Point Numbers(Decimal numbers)
   Example:
   ... -3.5, -2.25, -1.0, 0.0, 1.1, 2.2, 3.5 ...

3. Complex Numbers
   Example:
   1 + j, 2 + 4j, 1 - 1j

🌕 You have completed Day 2. Now practice the exercises below to strengthen your Python fundamentals.

## 💻 Exercises - Day 2

### Exercises: Level 1

1. Inside Python In 30 Days create a folder called `Day_02_Variables_builtin_functions`. Inside this folder create a file named `variables.py`.
2. Write a python comment saying 'Day 2: Python In 30 Days programming'
3. Declare a `first_name` variable and assign a value to it
4. Declare a `last_name` variable and assign a value to it
5. Declare a `full_name` variable and assign a value to it
6. Declare a `country` variable and assign the value 'India' to it
7. Declare a `city` variable and assign the value 'Mumbai' to it
8. Declare an `age` variable and assign a value to it
9. Declare a `year` variable and assign a value to it
10. Declare a variable `is_married` and assign a value to it
11. Declare a variable `is_true` and assign a value to it
12. Declare a variable `is_light_on` and assign a value to it
13. Declare multiple variables on one line

### Exercises: Level 2

1. Check the data type of all your variables using the `type()` built-in function
2. Using the `len()` built-in function, find the length of your first name
3. Compare the length of your first name and your last name
4. Declare 5 as num_one and 4 as num_two
5. Add num_one and num_two and assign the value to a variable total
6. Subtract num_two from num_one and assign the value to a variable diff
7. Multiply num_two and num_one and assign the value to a variable product
8. Divide num_one by num_two and assign the value to a variable division
9. Use modulus division to find num_two divided by num_one and assign the value to a variable remainder
10. Calculate num_one to the power of num_two and assign the value to a variable exp
11. Find floor division of num_one by num_two and assign the value to a variable floor_division
12. The radius of a circle is 30 meters.
    1. Calculate the area of a circle and assign the value to a variable name of _area_of_circle_
    2. Calculate the circumference of a circle and assign the value to a variable name of _circum_of_circle_
    3. Take radius as user input and calculate the area.
13. Use the built-in input function to get first name, last name, country and age from a user and store the value to their corresponding variable names
14. Run help('keywords') in Python shell or in your file to check for the Python reserved words or keywords

🎉 CONGRATULATIONS! 🎉

[<< Day 1](../Day_01_Introduction/01_Introduction.md) | [Day 3 >>](../Day_03_Operators/03_Operators.md)
