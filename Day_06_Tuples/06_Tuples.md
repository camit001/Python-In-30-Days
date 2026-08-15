<div align="center">
  <h1>Python In 30 Days: Day 6 - Tuples</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>

</div>

[<< Day 5](../Day_05_Lists/05_Lists.md) | [Day 7 >>](../Day_07_Sets/07_Sets.md)

**Python In 30 Days**

- [Day 6](#day-6)
  - [Tuples](#tuples)
    - [Creating a Tuple](#creating-a-tuple)
    - [Tuple Length](#tuple-length)
    - [Accessing Tuple Items](#accessing-tuple-items)
    - [Slicing Tuples](#slicing-tuples)
    - [Changing Tuples to Lists](#changing-tuples-to-lists)
    - [Checking an Item in a Tuple](#checking-an-item-in-a-tuple)
    - [Joining Tuples](#joining-tuples)
    - [Deleting Tuples](#deleting-tuples)
    - [Tuple Methods](#tuple-methods)
    - [When to Use Tuples](#when-to-use-tuples)
  - [💻 Exercises: Day 6](#-exercises-day-6)
    - [Exercises: Level 1](#exercises-level-1)
    - [Exercises: Level 2](#exercises-level-2)

# Day 6

## Tuples

A tuple is an ordered, immutable collection that can contain values of different data types. Tuples are commonly written using parentheses `()`.

Once a tuple is created, its items cannot be changed, added, or removed. This makes tuples useful when a group of values should remain unchanged.

Tuples support fewer methods than lists. The most commonly used tuple operations and methods are:

- `tuple()`: creates a tuple
- `count()`: counts how many times an item occurs
- `index()`: finds the index of the first occurrence of an item
- `+`: joins two or more tuples and creates a new tuple

### Creating a Tuple

- Empty tuple:

```py
empty_tuple = ()

# Or using the tuple constructor
empty_tuple = tuple()

print(empty_tuple)
```

- Tuple with initial values:

```py
fruits = ('banana', 'orange', 'mango', 'lemon')
print(fruits)
```

### Important: A One-Item Tuple

A tuple containing one item needs a trailing comma.

```py
not_a_tuple = ('Python')
print(type(not_a_tuple))     # <class 'str'>

one_item_tuple = ('Python',)
print(type(one_item_tuple))  # <class 'tuple'>
```

The comma creates the tuple. Parentheses alone do not.

### Tuple Length

We use the built-in `len()` function to get the number of items in a tuple.

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

print(len(fruits))  # 4
```

### Accessing Tuple Items

Like lists, tuples use positive and negative indexing.

#### Positive Indexing

Tuple indexes start from `0`.

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

first_fruit = fruits[0]
second_fruit = fruits[1]
last_fruit = fruits[-1]

print(first_fruit)   # banana
print(second_fruit)  # orange
print(last_fruit)    # lemon
```

You can also calculate the last index:

```py
last_index = len(fruits) - 1
print(fruits[last_index])  # lemon
```

#### Negative Indexing

Negative indexing starts from the end:

- `-1` → last item
- `-2` → second-last item
- `-3` → third-last item

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

print(fruits[-4])  # banana
print(fruits[-3])  # orange
print(fruits[-2])  # mango
print(fruits[-1])  # lemon
```

### Slicing Tuples

We can create a new tuple containing a selected range of items using slicing.

The syntax is:

```py
tuple[start:stop:step]
```

The `stop` index is not included.

#### Positive Indexes

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

print(fruits[0:4])  # ('banana', 'orange', 'mango', 'lemon')
print(fruits[:])    # ('banana', 'orange', 'mango', 'lemon')
print(fruits[1:3])  # ('orange', 'mango')
print(fruits[1:])   # ('orange', 'mango', 'lemon')
```

#### Negative Indexes

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

print(fruits[-4:])    # ('banana', 'orange', 'mango', 'lemon')
print(fruits[-3:-1])  # ('orange', 'mango')
print(fruits[-3:])    # ('orange', 'mango', 'lemon')
```

#### Reversing a Tuple

A tuple can be reversed using slicing:

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

reverse_fruits = fruits[::-1]
print(reverse_fruits)  # ('lemon', 'mango', 'orange', 'banana')
```

### Changing Tuples to Lists

Tuples are immutable, so we cannot directly modify their items.

If we need to modify the data, we can:

1. Convert the tuple to a list.
2. Modify the list.
3. Convert the list back to a tuple.

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

fruits = list(fruits)
fruits[0] = 'apple'

print(fruits)
# ['apple', 'orange', 'mango', 'lemon']

fruits = tuple(fruits)
print(fruits)
# ('apple', 'orange', 'mango', 'lemon')
```

### Checking an Item in a Tuple

Use the `in` operator to check whether an item exists in a tuple.

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

print('orange' in fruits)  # True
print('apple' in fruits)   # False
```

Trying to modify a tuple directly raises a `TypeError`:

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

# fruits[0] = 'apple'
# TypeError: 'tuple' object does not support item assignment
```

### Joining Tuples

We can join two or more tuples using the `+` operator.

```py
tpl1 = ('item1', 'item2', 'item3')
tpl2 = ('item4', 'item5', 'item6')

tpl3 = tpl1 + tpl2

print(tpl3)
# ('item1', 'item2', 'item3', 'item4', 'item5', 'item6')
```

Practical example:

```py
fruits = ('banana', 'orange', 'mango', 'lemon')
vegetables = ('Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot')

fruits_and_vegetables = fruits + vegetables

print(fruits_and_vegetables)
```

### Deleting Tuples

We cannot delete a single item from a tuple, but we can delete the entire tuple using `del`.

```py
fruits = ('banana', 'orange', 'mango', 'lemon')

del fruits

# print(fruits)
# NameError: name 'fruits' is not defined
```

## Tuple Methods

Tuples have two commonly used methods:

### `count()`

`count()` returns the number of times an item appears in a tuple.

```py
numbers = (1, 2, 2, 3, 2, 4)

print(numbers.count(2))  # 3
```

### `index()`

`index()` returns the index of the first occurrence of an item.

```py
fruits = ('banana', 'orange', 'mango', 'orange')

print(fruits.index('orange'))  # 1
```

If the item does not exist, `index()` raises a `ValueError`.

## When to Use Tuples

Use a tuple when the values represent a fixed collection that should not normally be changed.

For example:

```py
coordinates = (19.0760, 72.8777)
database_config = ('localhost', 5432, 'sales_db')
```

A list is generally better when the collection needs to change:

```py
skills = ['Python', 'SQL']
skills.append('PySpark')
```

### List vs Tuple

| Feature | List | Tuple |
|---|---|---|
| Syntax | `[]` | `()` |
| Ordered | Yes | Yes |
| Mutable | Yes | No |
| Allows duplicates | Yes | Yes |
| Supports `append()` | Yes | No |
| Supports `count()` | Yes | Yes |
| Supports `index()` | Yes | Yes |

**Practical tip:** Do not choose a tuple just because it may be slightly more memory-efficient. Choose it primarily when the data represents a fixed collection and immutability is useful.

## Personal Example

```py
personal_info = ("Amit Kumar", "India", "Mumbai")

print("Name:", personal_info[0])
print("Country:", personal_info[1])
print("City:", personal_info[2])
```

This example demonstrates how a tuple can store related values that should not be changed after creation.

🌕 You have completed Day 6 and learned how tuples store ordered, immutable data. Now practice the exercises below to strengthen your understanding.

## 💻 Exercises: Day 6

### Exercises: Level 1

1. Create an empty tuple.
2. Create a tuple containing names of your sisters and your brothers. Imaginary siblings are fine.
3. Join the brothers and sisters tuples and assign the result to `siblings`.
4. Find the number of siblings.
5. Modify the `siblings` tuple by adding the name of your father and mother, then assign the result to `family_members`.

### Exercises: Level 2

1. Unpack the siblings and parents from `family_members`.
2. Create `fruits`, `vegetables`, and `animal_products` tuples. Join the three tuples and assign the result to `food_stuff_tp`.
3. Convert `food_stuff_tp` to a list called `food_stuff_lt`.
4. Slice out the middle item or items from `food_stuff_tp` or `food_stuff_lt`.
5. Slice out the first three items and the last three items from `food_stuff_lt`.
6. Delete the `food_stuff_tp` tuple completely.
7. Check whether the following countries are Nordic countries:

```py
nordic_countries = ('Denmark', 'Finland', 'Iceland', 'Norway', 'Sweden')

print('Estonia' in nordic_countries)  # False
print('Iceland' in nordic_countries)  # True
```

### Extra Practice

8. Create a tuple containing five Python data types and print each item.
9. Create a one-item tuple and verify its type using `type()`.
10. Create a tuple of numbers and use `count()` and `index()` on it.
11. Create a tuple of three coordinates and print each coordinate using indexing.
12. Reverse a tuple using slicing without using `reverse()`.

🎉 CONGRATULATIONS! 🎉

[<< Day 5](../Day_05_Lists/05_Lists.md) | [Day 7 >>](../Day_07_Sets/07_Sets.md)
