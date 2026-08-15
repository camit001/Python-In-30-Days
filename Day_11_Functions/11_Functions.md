<div align="center">
  <h1> Python In 30 Days: Day 11 - Functions</h1>
 

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 10](../Day_10_Loops/10_Loops.md) | [Day 12 >>](../Day_12_Modules/12_Modules.md)

**Python In 30 Days**

- [📘 Day 11](#-day-11)
  - [Functions](#functions)
    - [Defining a Function](#defining-a-function)
    - [Declaring and Calling a Function](#declaring-and-calling-a-function)
    - [Function without Parameters](#function-without-parameters)
    - [Function Returning a Value - Part 1](#function-returning-a-value---part-1)
    - [Function with Parameters](#function-with-parameters)
    - [Passing Arguments with Key and Value](#passing-arguments-with-key-and-value)
    - [Function Returning a Value - Part 2](#function-returning-a-value---part-2)
    - [Function with Default Parameters](#function-with-default-parameters)
    - [Arbitrary Number of Arguments](#arbitrary-number-of-arguments)
    - [Default and Arbitrary Number of Parameters in Functions](#default-and-arbitrary-number-of-parameters-in-functions)
    - [Function as a Parameter of Another Function](#function-as-a-parameter-of-another-function)
  - [💻 Exercises: Day 11](#-exercises-day-11)
    - [Exercises: Level 1](#exercises-level-1)
    - [Exercises: Level 2](#exercises-level-2)
    - [Exercises: Level 3](#exercises-level-3)

# 📘 Day 11

## Functions

So far we have seen many built-in Python functions. In this section, we will focus on custom functions. What is a function? Before we start making functions, let us learn what a function is and why we need them?

### Why Use Functions?

Functions are useful because they let us:

- Reuse code instead of copying it.
- Break a large program into smaller, understandable pieces.
- Give meaningful names to operations.
- Test individual pieces of logic more easily.
- Return results that can be used elsewhere in a program.

A simple function has four important parts:

```py
def function_name(parameter):
    # function body
    return value
```

- `def` starts the function definition.
- `function_name` is the name used to call the function.
- `parameter` receives input from the caller.
- `return` sends a result back to the caller.

### Defining a Function

A function is a reusable block of code designed to perform a specific task. Functions help us organize code, avoid repetition, and make programs easier to test and maintain. To define or declare a function, Python provides the _def_ keyword. The following is the syntax for defining a function. The function body is not executed when the function is defined. It runs when the function is called.

### Declaring and Calling a Function

When we create a function using `def`, we define the function. When we use its name followed by parentheses, we call or invoke the function. When we start using it, we call it _calling_ or _invoking_ a function. Functions can be declared with or without parameters.

```py
# syntax
# Declaring a function
def function_name():
    codes
    codes
# Calling a function
function_name()
```

### Function without Parameters

Function can be declared without parameters.

**Example:**

```py
def generate_full_name():
    first_name = 'Amit'
    last_name = 'Kumar'
    space = ' '
    full_name = first_name + space + last_name
    print(full_name)
generate_full_name () # calling a function

def add_two_numbers():
    num_one = 2
    num_two = 3
    total = num_one + num_two
    print(total)
add_two_numbers()
```

### Function Returning a Value - Part 1

Functions return values using the _return_ statement. If a function has no return statement, it returns None. Let us rewrite the above functions using return. From now on, we get a value from a function when we call the function and print it.

```py
def generate_full_name():
    first_name = 'Amit'
    last_name = 'Kumar'
    space = ' '
    full_name = first_name + space + last_name
    return full_name
print(generate_full_name())

def add_two_numbers():
    num_one = 2
    num_two = 3
    total = num_one + num_two
    return total
print(add_two_numbers())
```

### Function with Parameters

In a function we can pass different data types (number, string, boolean, list, tuple, dictionary or set) as parameters.

- Single Parameter: If our function takes a parameter we should call our function with an argument

```py
  # syntax
  # Declaring a function
  def function_name(parameter):
    codes
    codes
  # Calling function
  print(function_name(argument))
```

**Example:**

```py
def greetings(name):
    message = name + ', welcome to Python for Everyone!'
    return message

print(greetings('Amit'))

def add_ten(num):
    ten = 10
    return num + ten
print(add_ten(90))

def square_number(x):
    return x * x
print(square_number(2))

def area_of_circle (r):
    PI = 3.14
    area = PI * r ** 2
    return area
print(area_of_circle(10))

def sum_of_numbers(n):
    total = 0
    for i in range(n+1):
        total += i
    return total
print(sum_of_numbers(10)) # 55
print(sum_of_numbers(100)) # 5050
```

- Two Parameter: A function may or may not have a parameter or parameters. A function may also have two or more parameters. If our function takes parameters we should call it with arguments. Let us check a function with two parameters:

```py
  # syntax
  # Declaring a function
  def function_name(para1, para2):
    codes
    codes
  # Calling function
  print(function_name(arg1, arg2))
```

**Example:**

```py
def generate_full_name(first_name, last_name):
    space = ' '
      full_name = first_name + space + last_name
      return full_name
print('Full Name: ', generate_full_name('Amit','Kumar'))

def sum_two_numbers (num_one, num_two):
    sum = num_one + num_two
    return sum
print('Sum of two numbers: ', sum_two_numbers(1, 9))

def calculate_age(current_year, birth_year):
    age = current_year - birth_year
    return age 

print('Age: ', calculate_age(2021, 1819))

def weight_of_object(mass, gravity):
    weight = str(mass * gravity)+ ' N' # the value has to be changed to a string first
    return weight
print('Weight of an object in Newtons: ', weight_of_object(100, 9.81))
```

### Passing Arguments with Key and Value

If we pass the arguments with key and value, the order of the arguments does not matter.

```py
# syntax
# Declaring a function
def function_name(para1, para2):
    codes
    codes
# Calling function
print(function_name(para1 = 'John', para2 = 'Doe')) # the order of arguments does not matter here
```

**Example:**

```py
def print_fullname(firstname, lastname):
    space = ' '
    full_name = firstname  + space + lastname
    print(full_name)
print_fullname(firstname = 'Amit', lastname = 'Kumar')

def add_two_numbers(num1, num2):
    total = num1 + num2
    return total
print(add_two_numbers(num2 = 3, num1 = 2)) # Order does not matter 
```

### Function Returning a Value - Part 2

If a function reaches the end without executing a `return` statement, Python returns `None` automatically. To return a value with a function we use the keyword _return_ followed by the variable we are returning. We can return any kind of data types from a function.

- Returning a string:
**Example:**

```py
def print_name(firstname):
    return firstname
print_name('Amit') # Amit

def print_full_name(firstname, lastname):
    space = ' '
    full_name = firstname  + space + lastname
    return full_name
print_full_name(firstname='Amit', lastname='Kumar')
```

- Returning a number:

**Example:**

```py
def add_two_numbers(num1, num2):
    total = num1 + num2
    return total
print(add_two_numbers(2, 3))

def calculate_age(current_year, birth_year):
    age = current_year - birth_year
    return age
print('Age: ', calculate_age(2019, 1819))
```

- Returning a boolean:
  **Example:**

```py
def is_even(n):
    if n % 2 == 0:
        return True    # return stops further execution of the function, similar to break 
    return False
print(is_even(10)) # True
print(is_even(7)) # False
```

- Returning a list:
  **Example:**

```py
def find_even_numbers(n):
    evens = []
    for i in range(n + 1):
        if i % 2 == 0:
            evens.append(i)
    return evens
print(find_even_numbers(10))
```

### Local Variables and Scope

Variables created inside a function are usually **local variables**. They can be used inside that function but are not automatically available outside it.

```py
def calculate_total():
    price = 100
    tax = 10
    return price + tax

print(calculate_total())
# print(price)  # NameError
```

A variable defined outside a function belongs to the surrounding/global scope:

```py
tax_rate = 0.10

def calculate_tax(amount):
    return amount * tax_rate

print(calculate_tax(100))
```

As a beginner, prefer passing required values as parameters and returning results instead of depending heavily on global variables.

### Function with Default Parameters

Sometimes we pass default values to parameters, when we invoke the function. If we do not pass arguments when calling the function, their default values will be used.

```py
# syntax
# Declaring a function
def function_name(param = value):
    codes
    codes
# Calling function
function_name()
function_name(arg)
```

**Example:**

```py
def greetings(name = 'Peter'):
    message = name + ', welcome to Python for Everyone!'
    return message
print(greetings())
print(greetings('Amit'))

def generate_full_name(first_name = 'Amit', last_name = 'Kumar'):
    space = ' '
    full_name = first_name + space + last_name
    return full_name

print(generate_full_name())
print(generate_full_name('David','Smith'))

def calculate_age(birth_year,current_year = 2021):
    age = current_year - birth_year
    return age 
print('Age: ', calculate_age(1821))

def weight_of_object(mass, gravity = 9.81):
    weight = str(mass * gravity)+ ' N' # the value has to be changed to string first
    return weight
print('Weight of an object in Newtons: ', weight_of_object(100)) # 9.81 - average gravity on Earth's surface
print('Weight of an object in Newtons: ', weight_of_object(100, 1.62)) # gravity on the surface of the Moon
```

### Positional vs Keyword Arguments

Arguments can be passed by position:

```py
def introduce(name, city):
    return f'{name} lives in {city}.'

print(introduce('Amit', 'Mumbai'))
```

Or by keyword:

```py
print(introduce(city='Mumbai', name='Amit'))
```

Keyword arguments make calls easier to read and their order does not matter when the parameter names are supplied correctly.

### Arbitrary Number of Arguments

If we do not know the number of arguments we pass to our function, we can create a function that can take arbitrary number of arguments by adding \* before the parameter name.

```py
# syntax
# Declaring a function
def function_name(*args):
    codes
    codes
# Calling function
function_name(param1, param2, param3,..)
```

**Example:**

```py
def sum_all_nums(*nums):
    total = 0
    for num in nums:
        total += num     # same as total = total + num 
    return total
print(sum_all_nums(2, 3, 5)) # 10
```

### Default and Arbitrary Number of Parameters in Functions

```py
def generate_groups (team,*args):
    print(team)
    for i in args:
        print(i) 
generate_groups('Team-1','Amit','Brook','David','Eyob')
```
### Keyword Argument Unpacking with `**`

You can call a function that has named arguments using a dictionary with matching key names. You do so using ``**``.

```py
# Define a function that takes two arguments: 'name' and 'location'
def greet(name, location):
    # Print a greeting message using the provided arguments
    print("Hi there", name, "how is the weather in", location)

# Call the function using keyword arguments
greet(name="Alice", location="New York")  
# Output: Hi there Alice how is the weather in New York

# Create a dictionary with keys matching the function's parameter names
my_dict = {"name": "Alice", "location": "New York"}

# Call the function using dictionary unpacking
greet(**my_dict)  
# The ** operator unpacks the dictionary, passing its key-value pairs 
# as keyword arguments to the function.
# Output: Hi there Alice how is the weather in New York
```

### `*args` and `**kwargs`

`*args` collects extra positional arguments into a tuple:

```py
def show_numbers(*args):
    print(args)

show_numbers(10, 20, 30)
# (10, 20, 30)
```

`**kwargs` collects extra keyword arguments into a dictionary:

```py
def show_details(**kwargs):
    print(kwargs)

show_details(name='Amit', city='Mumbai')
# {'name': 'Amit', 'city': 'Mumbai'}
```

A function can use both:

```py
def example(required, *args, **kwargs):
    print(required)
    print(args)
    print(kwargs)
```

Use these features when the function genuinely needs a variable number of arguments. For normal functions, explicit parameters are usually clearer.

### Arbitrary Number of Named Arguments

You can also define a function to accept an arbitrary number of named arguments.

```py
def arbitrary_named_args(**args):
    print("I received an arbitrary number of arguments, totaling", len(args))
    print("They are provided as a dictionary in my function:", type(args))
    print("Let's print them:")
    for k, v in args.items():
        print(" * key:", k, "value:", v)
```

Generally avoid this unless required as it makes it harder to understand what the function accepts and does.

### Function as a Parameter of Another Function

```py
#You can pass functions around as parameters
def square_number(n):
    return n ** 2
def do_something(f, x):
    return f(x)
print(do_something(square_number, 3)) # 27
```

## Lambda Functions

A `lambda` is a small anonymous function. It can contain one expression and automatically returns the result.

```py
square = lambda x: x ** 2

print(square(5))
# 25
```

Lambdas are often useful for short operations passed to functions such as `sorted()`:

```py
employees = [
    {'name': 'Amit', 'salary': 70000},
    {'name': 'Rahul', 'salary': 50000},
    {'name': 'Priya', 'salary': 90000}
]

employees.sort(key=lambda employee: employee['salary'])

print(employees)
```

For complex logic, use a normal `def` function because it is easier to read and document.

## Docstrings

A function can document what it does using a docstring:

```py
def add_two_numbers(a, b):
    """Return the sum of two numbers."""
    return a + b

print(add_two_numbers.__doc__)
```

Docstrings are useful for explaining a function's purpose, inputs, and returned result.

## Type Hints

Type hints make the expected input and output types clearer:

```py
def add_two_numbers(a: int, b: int) -> int:
    return a + b

print(add_two_numbers(10, 20))
```

Type hints do not automatically enforce the types at runtime. They mainly improve readability, editor support, and static analysis.

## Practical Data Engineering Example

Functions are especially useful when the same transformation must be applied to many records.

```py
def clean_name(name):
    return name.strip().title()

names = [' amit ', 'RAHUL', ' priya']

cleaned_names = []

for name in names:
    cleaned_names.append(clean_name(name))

print(cleaned_names)
# ['Amit', 'Rahul', 'Priya']
```

A reusable validation function can also keep pipeline logic clean:

```py
def is_valid_employee(employee):
    return (
        employee.get('employee_id') is not None
        and employee.get('name')
        and employee.get('department')
    )

employee = {
    'employee_id': 101,
    'name': 'Amit',
    'department': 'Data Engineering'
}

print(is_valid_employee(employee))
# True
```

This pattern is useful in ETL and data-processing code because validation or transformation logic can be defined once and reused.


🌕 You achieved quite a lot so far.  Keep going! You have just completed day 11 challenges and you are 11 steps ahead in your way to greatness. Now do some exercises for your brain and muscles.


## 💻 Exercises: Day 11

### Exercises: Level 1

1. Declare a function _add_two_numbers_. It takes two parameters and it returns a sum.
2. Area of a circle is calculated as follows: area = π x r x r. Write a function that calculates _area_of_circle_.
3. Write a function called add_all_nums which takes arbitrary number of arguments and sums all the arguments. Check if all the list items are number types. If not do give a reasonable feedback.
4. Temperature in °C can be converted to °F using this formula: °F = (°C x 9/5) + 32. Write a function that converts °C to °F, _convert_celsius_to_fahrenheit_.
5. Write a function called check_season, it takes a month parameter and returns the season: Autumn, Winter, Spring or Summer.
6. Write a function called calculate_slope which return the slope of a linear equation
7. Quadratic equation is calculated as follows: ax² + bx + c = 0. Write a function that calculates solution set of a quadratic equation, _solve_quadratic_eqn_.
8. Declare a function named print_list. It takes a list as a parameter and it prints out each element of the list.
9. Declare a function named reverse_list. It takes an array as a parameter and it returns the reverse of the array (use loops).

```py
print(reverse_list([1, 2, 3, 4, 5]))
# [5, 4, 3, 2, 1]
print(reverse_list(["A", "B", "C"])) 
# ["C", "B", "A"]
```

10. Declare a function named capitalize_list_items. It takes a list as a parameter and it returns a capitalized list of items
11. Declare a function named add_item. It takes a list and an item parameters. It returns a list with the item added at the end.

```py
food_stuff = ['Potato', 'Tomato', 'Mango', 'Milk'];
print(add_item(food_stuff, 'Meat'))     # ['Potato', 'Tomato', 'Mango', 'Milk','Meat'];
numbers = [2, 3, 7, 9];
print(add_item(numbers, 5))      # [2, 3, 7, 9, 5]

```

12. Declare a function named remove_item. It takes a list and an item parameters. It returns a list with the item removed from it.

```py
food_stuff = ['Potato', 'Tomato', 'Mango', 'Milk']
print(remove_item(food_stuff, 'Mango'))  # ['Potato', 'Tomato', 'Milk'];
numbers = [2, 3, 7, 9]
print(remove_item(numbers, 3))  # [2, 7, 9]
```

13. Declare a function named sum_of_numbers. It takes a number parameter and it adds all the numbers in that range.

```py
print(sum_of_numbers(5))  # 15
print(sum_of_numbers(10)) # 55
print(sum_of_numbers(100)) # 5050
```

14. Declare a function named sum_of_odds. It takes a number parameter and it adds all the odd numbers in that range.
15. Declare a function named sum_of_even. It takes a number parameter and it adds all the even numbers in that - range.

### Exercises: Level 2

1. Declare a function named evens_and_odds . It takes a positive integer as parameter and it counts number of evens and odds in the number.

```py
    print(evens_and_odds(100))
    # The number of odds are 50.
    # The number of evens are 51.
```

1. Call your function factorial, it takes a whole number as a parameter and it return a factorial of the number
1. Call your function _is_empty_, it takes a parameter and it checks if it is empty or not
1. Write different functions which take lists. They should calculate_mean, calculate_median, calculate_mode, calculate_range, calculate_variance, calculate_std (standard deviation).
1. Write a function called _greet_ which takes a default argument, _name_. If no argument is supplied it should print "Hello, Guest!", otherwise it should greet the person by name.

```py
    greet()
    # "Hello, Guest!
    greet("Alice")
    # "Hello, Alice!"
```
1. Create a function called _show_args_ to take an arbitrary number of named arguments and print their names and values.
   ```py
   show_args(name="Alice", age=30, city="New York")
   # Received: name: Alice, age: 30, city: New York
   show_args(name="Bob", pet="Fluffy, the bunny")
   # Received: name: Bob, pet: Fluffy, the bunny
   ```


### Exercises: Level 3

1. Write a function called is_prime, which checks if a number is prime.
1. Write a functions which checks if all items are unique in the list.
1. Write a function that checks if all the items of the list are of the same data type.
1. Write a function that check if provided variable is a valid python variable
1. Go to the data folder and access the countries-data.py file.

- Create a function called the most_spoken_languages in the world. It should return 10 or 20 most spoken languages in the world in descending order
- Create a function called the most_populated_countries. It should return 10 or 20 most populated countries in descending order.


### Extra Practice

1. Write a function that accepts a list of numbers and returns the largest number.
2. Write a function that accepts a list of strings and returns only strings longer than five characters.
3. Write a function that counts how many times each value appears in a list.
4. Write a function that removes duplicate values from a list while preserving their order.
5. Write a function that validates an employee dictionary and returns `True` or `False`.
6. Write a function that converts a list of Celsius temperatures into Fahrenheit temperatures.
7. Write a function that accepts `*args` and returns the average of all numeric arguments.
8. Write a function that accepts `**kwargs` and prints each key-value pair.
9. Write a function with a docstring and type hints.
10. Write a function and pass it as an argument to another function.

🎉 CONGRATULATIONS! 🎉

[<< Day 10](../Day_10_Loops/10_Loops.md) | [Day 12 >>](../Day_12_Modules/12_Modules.md)
