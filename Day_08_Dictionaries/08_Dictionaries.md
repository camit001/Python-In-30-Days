<div align="center">
  <h1>Python In 30 Days: Day 8 - Dictionaries</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 7](../Day_07_Sets/07_Sets.md) | [Day 9 >>](../Day_09_Conditionals/09_Conditionals.md)

**Python In 30 Days**

- [📘 Day 8](#-day-8)
  - [Dictionaries](#dictionaries)
    - [Creating a Dictionary](#creating-a-dictionary)
    - [Dictionary Length](#dictionary-length)
    - [Accessing Dictionary Items](#accessing-dictionary-items)
    - [Adding Items to a Dictionary](#adding-items-to-a-dictionary)
    - [Modifying Items in a Dictionary](#modifying-items-in-a-dictionary)
    - [Checking Keys in a Dictionary](#checking-keys-in-a-dictionary)
    - [Removing Key-Value Pairs](#removing-key-value-pairs)
    - [Changing Dictionary to a List of Items](#changing-dictionary-to-a-list-of-items)
    - [Clearing a Dictionary](#clearing-a-dictionary)
    - [Deleting a Dictionary](#deleting-a-dictionary)
    - [Copying a Dictionary](#copying-a-dictionary)
    - [Getting Dictionary Keys](#getting-dictionary-keys)
    - [Getting Dictionary Values](#getting-dictionary-values)
    - [Practical Dictionary Basics](#practical-dictionary-basics)
    - [Common Dictionary Methods](#common-dictionary-methods)
  - [💻 Exercises: Day 8](#-exercises-day-8)

# 📘 Day 8

## Dictionaries

A dictionary is a mutable collection of **key-value pairs**.

Each key identifies its corresponding value. Keys must be unique within a dictionary, while values can be of different data types, including strings, numbers, booleans, lists, tuples, sets, and other dictionaries.

In modern Python, dictionaries preserve insertion order, but values are accessed primarily by key rather than numeric index.

### Creating a Dictionary

To create a dictionary, use curly brackets `{}` or the `dict()` built-in function.

```py
# Empty dictionary
empty_dict = {}

# Dictionary with data values
dct = {
    'key1': 'value1',
    'key2': 'value2',
    'key3': 'value3',
    'key4': 'value4'
}
```

**Example:**

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

A dictionary value can itself be another dictionary. This is called a **nested dictionary**.

### Dictionary Length

The built-in `len()` function returns the number of key-value pairs.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3', 'key4': 'value4'}

print(len(dct))  # 4
```

**Example:**

```py
person = {
    'first_name': 'Amit',
    'last_name': 'Kumar',
    'age': 25,
    'country': 'India',
    'is_married': False,
    'skills': ['Python', 'SQL', 'PySpark', 'Databricks'],
    'address': {'city': 'Mumbai', 'zipcode': '400001'}
}

print(len(person))  # 7
```

### Accessing Dictionary Items

Access a dictionary value by referring to its key.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3', 'key4': 'value4'}

print(dct['key1'])  # value1
print(dct['key4'])  # value4
```

**Example:**

```py
person = {
    'first_name': 'Amit',
    'last_name': 'Kumar',
    'age': 25,
    'country': 'India',
    'is_married': False,
    'skills': ['Python', 'SQL', 'PySpark', 'Databricks'],
    'address': {'city': 'Mumbai', 'zipcode': '400001'}
}

print(person['first_name'])       # Amit
print(person['country'])          # India
print(person['skills'])           # ['Python', 'SQL', 'PySpark', 'Databricks']
print(person['skills'][0])        # Python
print(person['address']['city'])  # Mumbai
```

Using square brackets with a missing key raises a `KeyError`:

```py
# print(person['city'])
# KeyError: 'city'
```

If the key may not exist, use `get()`:

```py
print(person.get('first_name'))  # Amit
print(person.get('country'))     # India
print(person.get('skills'))      # ['Python', 'SQL', 'PySpark', 'Databricks']
print(person.get('city'))        # None
print(person.get('city', 'Unknown'))  # Unknown
```

### Adding Items to a Dictionary

Add a new key-value pair by assigning a value to a new key.

```py
dct = {'key1': 'value1', 'key2': 'value2'}

dct['key3'] = 'value3'

print(dct)
```

If the key already exists, assignment modifies its value instead of creating a duplicate key.

### Modifying Items in a Dictionary

```py
dct = {'key1': 'value1', 'key2': 'value2'}

dct['key1'] = 'new-value'

print(dct)
```

**Example:**

```py
person = {
    'first_name': 'Amit',
    'last_name': 'Kumar',
    'age': 25,
    'country': 'India'
}

person['age'] = 26
person['city'] = 'Mumbai'

print(person)
```

### Checking Keys in a Dictionary

Use the `in` operator to check whether a key exists.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}

print('key2' in dct)  # True
print('key5' in dct)  # False
```

By default, `in` checks keys, not values:

```py
person = {'name': 'Amit', 'city': 'Mumbai'}

print('name' in person)              # True
print('Amit' in person)              # False
print('Amit' in person.values())     # True
```

### Removing Key-Value Pairs

- `pop(key)`: removes and returns the value for the specified key.
- `popitem()`: removes and returns the last inserted key-value pair.
- `del`: removes a specified key-value pair.
- `clear()`: removes all key-value pairs.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}

removed_value = dct.pop('key1')
print(removed_value)  # value1

dct.popitem()
del dct['key2']
```

### Changing Dictionary to a List of Items

The `items()` method returns a view containing key-value pairs.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}

print(dct.items())
# dict_items([('key1', 'value1'), ('key2', 'value2'), ('key3', 'value3')])
```

If you specifically need a list:

```py
items_list = list(dct.items())
print(items_list)
```

### Clearing a Dictionary

Use `clear()` to remove all key-value pairs while keeping the dictionary object.

```py
dct = {'key1': 'value1', 'key2': 'value2'}

result = dct.clear()

print(dct)     # {}
print(result)  # None
```

### Deleting a Dictionary

Use `del` to delete the dictionary variable completely.

```py
dct = {'key1': 'value1', 'key2': 'value2'}

del dct

# print(dct)
# NameError: name 'dct' is not defined
```

### Copying a Dictionary

Use `copy()` to create a shallow copy.

```py
dct = {'key1': 'value1', 'key2': 'value2'}

dct_copy = dct.copy()

print(dct_copy)
```

Avoid `dct_copy = dct` when you need a separate dictionary because both variables then refer to the same object.

### Getting Dictionary Keys

The `keys()` method returns a view containing all keys.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}

keys = dct.keys()
print(keys)
# dict_keys(['key1', 'key2', 'key3'])

keys_list = list(dct.keys())
print(keys_list)
```

### Getting Dictionary Values

The `values()` method returns a view containing all values.

```py
dct = {'key1': 'value1', 'key2': 'value2', 'key3': 'value3'}

values = dct.values()
print(values)
# dict_values(['value1', 'value2', 'value3'])

values_list = list(dct.values())
print(values_list)
```

## Practical Dictionary Basics

Dictionaries are useful whenever you need to associate one piece of information with another.

```py
employee = {
    'employee_id': 101,
    'name': 'Amit Kumar',
    'department': 'Data Engineering',
    'skills': ['Python', 'SQL', 'PySpark'],
    'location': 'Mumbai'
}

print(employee['name'])
print(employee['skills'])
```

Dictionaries are also useful for counting values:

```py
fruits = ['apple', 'banana', 'apple', 'orange', 'banana', 'apple']

counts = {}

for fruit in fruits:
    counts[fruit] = counts.get(fruit, 0) + 1

print(counts)
# {'apple': 3, 'banana': 2, 'orange': 1}
```

This counting pattern is useful when processing real-world data.

### Common Dictionary Methods

| Method | Purpose | Example |
|---|---|---|
| `get()` | Safely retrieves a value | `data.get('name')` |
| `keys()` | Returns dictionary keys | `data.keys()` |
| `values()` | Returns dictionary values | `data.values()` |
| `items()` | Returns key-value pairs | `data.items()` |
| `update()` | Adds or updates multiple pairs | `data.update({'age': 26})` |
| `pop()` | Removes a specified key | `data.pop('age')` |
| `popitem()` | Removes the last inserted pair | `data.popitem()` |
| `clear()` | Removes all pairs | `data.clear()` |
| `copy()` | Creates a shallow copy | `new = data.copy()` |

### Iterating Through a Dictionary

Use `items()` when you need both keys and values:

```py
person = {
    'name': 'Amit',
    'city': 'Mumbai',
    'country': 'India'
}

for key, value in person.items():
    print(key, ':', value)
```

You can also iterate over only keys or values:

```py
for key in person.keys():
    print(key)

for value in person.values():
    print(value)
```

### Nested Dictionaries

A dictionary can contain another dictionary as a value.

```py
employee = {
    'name': 'Amit Kumar',
    'address': {
        'city': 'Mumbai',
        'country': 'India'
    }
}

print(employee['address']['city'])  # Mumbai
```

This structure is common when working with JSON data and APIs.

## Personal Example

```py
personal_info = {
    'name': 'Amit Kumar',
    'country': 'India',
    'city': 'Mumbai',
    'role': 'Data Engineer'
}

print(personal_info['name'])
print(personal_info['country'])
print(personal_info['city'])
print(personal_info['role'])
```

This example demonstrates how a dictionary can store related information using descriptive keys.

🌕 You have completed Day 8 and learned how dictionaries store and manage key-value data. Now practice the exercises below.

## 💻 Exercises: Day 8

1. Create an empty dictionary called `dog`.
2. Add `name`, `color`, `breed`, `legs`, and `age` to the `dog` dictionary.
3. Create a `student` dictionary and add `first_name`, `last_name`, `gender`, `age`, `marital_status`, `skills`, `country`, `city`, and `address` as keys.
4. Get the length of the `student` dictionary.
5. Get the value of `skills` and check its data type. It should be a list.
6. Modify the `skills` value by adding one or two skills.
7. Get the dictionary keys as a list.
8. Get the dictionary values as a list.
9. Convert the dictionary to a list of tuples using the `items()` method.
10. Delete one of the items in the dictionary.
11. Delete one of the dictionaries.

### Extra Practice

12. Use `get()` to safely retrieve a key that does not exist.
13. Create a dictionary containing employee IDs and names.
14. Iterate through the dictionary using `items()`.
15. Create a dictionary that counts the frequency of words in a list.
16. Create a nested dictionary representing an employee and their address.
17. Use `update()` to add multiple key-value pairs to a dictionary.
18. Explain the difference between `pop()`, `popitem()`, `del`, and `clear()`.

🎉 CONGRATULATIONS! 🎉

[<< Day 7](../Day_07_Sets/07_Sets.md) | [Day 9 >>](../Day_09_Conditionals/09_Conditionals.md)
