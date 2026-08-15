<div align="center">
  <h1> Python In 30 Days: Day 5 - Lists</h1>
  

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>
</sub>

</div>

[<< Day 4](../Day_04_Strings/04_Strings.md) | [Day 6 >>](../Day_06_Tuples/06_Tuples.md)

**Python In 30 Days**

- [Day 5](#day-5)
  - [Lists](#lists)
    - [How to Create a List](#how-to-create-a-list)
    - [Accessing List Items Using Positive Indexing](#accessing-list-items-using-positive-indexing)
    - [Accessing List Items Using Negative Indexing](#accessing-list-items-using-negative-indexing)
    - [Unpacking List Items](#unpacking-list-items)
    - [Slicing Items from a List](#slicing-items-from-a-list)
    - [Modifying Lists](#modifying-lists)
    - [Checking Items in a List](#checking-items-in-a-list)
    - [Adding Items to a List](#adding-items-to-a-list)
    - [Inserting Items into a List](#inserting-items-into-a-list)
    - [Removing Items from a List](#removing-items-from-a-list)
    - [Removing Items Using Pop](#removing-items-using-pop)
    - [Removing Items Using Del](#removing-items-using-del)
    - [Clearing List Items](#clearing-list-items)
    - [Copying a List](#copying-a-list)
    - [Joining Lists](#joining-lists)
    - [Counting Items in a List](#counting-items-in-a-list)
    - [Finding Index of an Item](#finding-index-of-an-item)
    - [Reversing a List](#reversing-a-list)
    - [Sorting List Items](#sorting-list-items)
  - [💻 Exercises: Day 5](#-exercises-day-5)
    - [Exercises: Level 1](#exercises-level-1)
    - [Exercises: Level 2](#exercises-level-2)

# Day 5

## Lists

## Personal Example

```python
name = "Amit Kumar"
country = "India"
city = "Mumbai"

personal_info = [name, country, city]

print(personal_info)
print("Name:", personal_info[0])
print("Country:", personal_info[1])
print("City:", personal_info[2])
```


Python has four commonly used built-in collection data types:

- List: an ordered, mutable collection that allows duplicate items.
- Tuple: an ordered, immutable collection that allows duplicate items.
- Set: an unordered collection of unique items. Sets are mutable, so items can be added or removed.
- Dictionary: a mutable collection of key-value pairs. Keys must be unique.

A list is an ordered and mutable collection that can contain values of different data types. A list can be empty or it may have different data type items.

### How to Create a List

In Python we can create lists in two ways:

- Using list built-in function

```py
# syntax
lst = list()
```

```py
empty_list = list() # this is an empty list, no item in the list
print(len(empty_list)) # 0
```

- Using square brackets, []

```py
# syntax
lst = []
```

```py
empty_list = [] # this is an empty list, no item in the list
print(len(empty_list)) # 0
```

Lists with initial values. We use _len()_ to find the length of a list.

```py
fruits = ['banana', 'orange', 'mango', 'lemon']                     # list of fruits
vegetables = ['Tomato', 'Potato', 'Cabbage','Onion', 'Carrot']      # list of vegetables
animal_products = ['milk', 'meat', 'butter', 'yoghurt']             # list of animal products
web_techs = ['HTML', 'CSS', 'JavaScript', 'React','Redux', 'Node', 'MongoDB'] # list of web technologies
countries = ['Finland', 'Estonia', 'Denmark', 'Sweden', 'Norway'] 

# Print the lists and its length
print('Fruits:', fruits)
print('Number of fruits:', len(fruits))
print('Vegetables:', vegetables)
print('Number of vegetables:', len(vegetables))
print('Animal products:',animal_products)
print('Number of animal products:', len(animal_products))
print('Web technologies:', web_techs)
print('Number of web technologies:', len(web_techs))
print('Countries:', countries)
print('Number of countries:', len(countries))
```

```sh
output
Fruits: ['banana', 'orange', 'mango', 'lemon']
Number of fruits: 4
Vegetables: ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
Number of vegetables: 5
Animal products: ['milk', 'meat', 'butter', 'yoghurt']
Number of animal products: 4
Web technologies: ['HTML', 'CSS', 'JavaScript', 'React', 'Redux', 'Node', 'MongoDB']
Number of web technologies: 7
Countries: ['Finland', 'Estonia', 'Denmark', 'Sweden', 'Norway']
Number of countries: 5
```

- Lists can have items of different data types

```py
 lst = ['Amit Kumar', 250, True, {'country':'India', 'city':'Mumbai'}] # list containing different data types
```

### Accessing List Items Using Positive Indexing

We access each item in a list using their index. A list index starts from 0. The picture below shows clearly where the index starts
**[List index]**

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
first_fruit = fruits[0] # we are accessing the first item using its index
print(first_fruit)      # banana
second_fruit = fruits[1]
print(second_fruit)     # orange
last_fruit = fruits[3]
print(last_fruit) # lemon
# Last index
last_index = len(fruits) - 1
last_fruit = fruits[last_index]
```

### Accessing List Items Using Negative Indexing

Negative indexing means beginning from the end, -1 refers to the last item, -2 refers to the second last item.

**[List negative indexing]**

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
first_fruit = fruits[-4]
last_fruit = fruits[-1]
second_last = fruits[-2]
print(first_fruit)      # banana
print(last_fruit)       # lemon
print(second_last)      # mango
```

### Unpacking List Items

```py
lst = ['item1','item2','item3', 'item4', 'item5']
first_item, second_item, third_item, *rest = lst
print(first_item)     # item1
print(second_item)    # item2
print(third_item)     # item3
print(rest)           # ['item4', 'item5']

```

```py
# First Example
fruits = ['banana', 'orange', 'mango', 'lemon','lime','apple']
first_fruit, second_fruit, third_fruit, *rest = fruits 
print(first_fruit)     # banana
print(second_fruit)    # orange
print(third_fruit)     # mango
print(rest)           # ['lemon','lime','apple']
# Second Example about unpacking list
first, second, third,*rest, tenth = [1,2,3,4,5,6,7,8,9,10]
print(first)          # 1
print(second)         # 2
print(third)          # 3
print(rest)           # [4,5,6,7,8,9]
print(tenth)          # 10
# Third Example about unpacking list
countries = ['Germany', 'France','Belgium','Sweden','Denmark','Finland','Norway','Iceland','Estonia']
gr, fr, bg, sw, *scandic, es = countries
print(gr) 
print(fr)
print(bg)
print(sw)
print(scandic)
print(es)
```

### Slicing Items from a List

- Positive Indexing: We can specify a range of positive indexes by specifying the start, end and step, the return value will be a new list. (default values for start = 0, end = len(lst) - 1 (last item), step = 1)

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
all_fruits = fruits[0:4] # it returns all the fruits
# this will also give the same result as the one above
all_fruits = fruits[0:] # if we don't set where to stop it takes all the rest
orange_and_mango = fruits[1:3] # it does not include the first index
orange_mango_lemon = fruits[1:]
orange_and_lemon = fruits[::2]  # step=2 selects every second item - ['banana', 'mango']
```

- Negative Indexing: We can specify a range of negative indexes by specifying the start, end and step, the return value will be a new list.

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
all_fruits = fruits[-4:] # it returns all the fruits
orange_and_mango = fruits[-3:-1] # it does not include the last index,['orange', 'mango']
orange_mango_lemon = fruits[-3:] # this will give starting from -3 to the end,['orange', 'mango', 'lemon']
reverse_fruits = fruits[::-1] # a negative step will take the list in reverse order,['lemon', 'mango', 'orange', 'banana']
```

### Practical List Basics

Lists are one of the most important Python data structures because they let you store multiple values in one ordered, mutable collection.

A useful way to think about a list is:

```text
Index:    0        1        2
Value:  Python    SQL    PySpark
```

```py
skills = ['Python', 'SQL', 'PySpark']

print(skills[0])       # Python
print(skills[-1])      # PySpark
print(skills[0:2])     # ['Python', 'SQL']
```

**Important:** list methods such as `append()`, `insert()`, `remove()`, `sort()`, and `reverse()` modify the existing list.

```py
skills = ['Python', 'SQL']

skills.append('PySpark')
print(skills)           # ['Python', 'SQL', 'PySpark']
```

A common beginner mistake is expecting `append()` or `sort()` to return the modified list:

```py
skills = ['Python', 'SQL']
result = skills.append('PySpark')

print(result)           # None
print(skills)           # ['Python', 'SQL', 'PySpark']
```

**Practical tip:** use `sorted(my_list)` when you want a new sorted list and `my_list.sort()` when you intentionally want to modify the original list.

### Modifying Lists

List is a mutable or modifiable ordered collection of items. Lets modify the fruit list.

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits[0] = 'avocado'
print(fruits)       #  ['avocado', 'orange', 'mango', 'lemon']
fruits[1] = 'apple'
print(fruits)       #  ['avocado', 'apple', 'mango', 'lemon']
last_index = len(fruits) - 1
fruits[last_index] = 'lime'
print(fruits)        #  ['avocado', 'apple', 'mango', 'lime']
```

### Checking Items in a List

To check whether an item exists in a list, use the `in` operator. See the example below.

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
does_exist = 'banana' in fruits
print(does_exist)  # True
does_exist = 'lime' in fruits
print(does_exist)  # False
```

### Adding Items to a List

To add an item to the end of a list, use the `append()` method.

```py
# syntax
lst = list()
lst.append(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.append('apple')
print(fruits)           # ['banana', 'orange', 'mango', 'lemon', 'apple']
fruits.append('lime')   # ['banana', 'orange', 'mango', 'lemon', 'apple', 'lime']
print(fruits)
```

### Inserting Items into a List

We can use the `insert()` method to insert a single item at a specified index in a list. Note that other items are shifted to the right. The `insert()` method takes two arguments: the index and the item to insert.

```py
# syntax
lst = ['item1', 'item2']
lst.insert(index, item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.insert(2, 'apple') # insert apple between orange and mango
print(fruits)           # ['banana', 'orange', 'apple', 'mango', 'lemon']
fruits.insert(3, 'lime')   # ['banana', 'orange', 'apple', 'lime', 'mango', 'lemon']
print(fruits)
```

### Removing Items from a List

The `remove()` method removes the first occurrence of a specified item from a list.

```py
# syntax
lst = ['item1', 'item2']
lst.remove(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon', 'banana']
fruits.remove('banana')
print(fruits)  # ['orange', 'mango', 'lemon', 'banana'] - this method removes the first occurrence of the item in the list
fruits.remove('lemon')
print(fruits)  # ['orange', 'mango', 'banana']
```

### Removing Items Using Pop

The `pop()` method removes and returns an item at the specified index, or the last item if no index is specified.

```py
# syntax
lst = ['item1', 'item2']
lst.pop()       # last item
lst.pop(index)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.pop()
print(fruits)       # ['banana', 'orange', 'mango']

fruits.pop(0)
print(fruits)       # ['orange', 'mango']
```

### Removing Items Using Del

The `del` keyword can remove an item at a specified index and it can also be used to delete items within index range. It can also delete the list completely

```py
# syntax
lst = ['item1', 'item2']
del lst[index] # only a single item
del lst        # to delete the list completely
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon', 'kiwi', 'lime']
del fruits[0]
print(fruits)       # ['orange', 'mango', 'lemon', 'kiwi', 'lime']
del fruits[1]
print(fruits)       # ['orange', 'lemon', 'kiwi', 'lime']
del fruits[1:3]     # deletes indexes 1 and 2; index 3 is not included
print(fruits)       # ['orange', 'lime']
del fruits
print(fruits)       # This should give: NameError: name 'fruits' is not defined
```

### Clearing List Items

The *clear()* method empties the list:

```py
# syntax
lst = ['item1', 'item2']
lst.clear()
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.clear()
print(fruits)       # []
```

### Copying a List

Assigning `list2 = list1` does not create a new list. Both variables refer to the same list. Now, list2 is a reference of list1, any changes we make in list2 will also modify the original, list1. If you need an independent shallow copy, use `copy()`.

```py
# syntax
lst = ['item1', 'item2']
lst_copy = lst.copy()
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits_copy = fruits.copy()
print(fruits_copy)       # ['banana', 'orange', 'mango', 'lemon']
```

### Joining Lists

There are several ways to join, or concatenate, two or more lists in Python.

- Plus Operator (+)

```py
# syntax
list3 = list1 + list2
```

```py
positive_numbers = [1, 2, 3, 4, 5]
zero = [0]
negative_numbers = [-5,-4,-3,-2,-1]
integers = negative_numbers + zero + positive_numbers
print(integers) # [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
fruits = ['banana', 'orange', 'mango', 'lemon']
vegetables = ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
fruits_and_vegetables = fruits + vegetables
print(fruits_and_vegetables ) # ['banana', 'orange', 'mango', 'lemon', 'Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
```

- Joining using extend() method
  The `extend()` method adds each item from another iterable to the end of the list. See the example below.

```py
# syntax
list1 = ['item1', 'item2']
list2 = ['item3', 'item4', 'item5']
list1.extend(list2) # ['item1', 'item2', 'item3', 'item4', 'item5']
```

```py
num1 = [0, 1, 2, 3]
num2= [4, 5, 6]
num1.extend(num2)
print('Numbers:', num1) # Numbers: [0, 1, 2, 3, 4, 5, 6]
negative_numbers = [-5,-4,-3,-2,-1]
positive_numbers = [1, 2, 3,4,5]
zero = [0]

negative_numbers.extend(zero)
negative_numbers.extend(positive_numbers)
print('Integers:', negative_numbers) # Integers: [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
fruits = ['banana', 'orange', 'mango', 'lemon']
vegetables = ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
fruits.extend(vegetables)
print('Fruits and vegetables:', fruits ) # Fruits and vegetables: ['banana', 'orange', 'mango', 'lemon', 'Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
```

### Counting Items in a List

The *count()* method returns the number of times an item appears in a list:

```py
# syntax
lst = ['item1', 'item2']
lst.count(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
print(fruits.count('orange'))   # 1
ages = [22, 19, 24, 25, 26, 24, 25, 24]
print(ages.count(24))           # 3
```

### Finding Index of an Item

The *index()* method returns the index of an item in the list:

```py
# syntax
lst = ['item1', 'item2']
lst.index(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
print(fruits.index('orange'))   # 1
ages = [22, 19, 24, 25, 26, 24, 25, 24]
print(ages.index(24))           # 2, the first occurrence
```

### Reversing a List

The *reverse()* method reverses the order of a list.

```py
# syntax
lst = ['item1', 'item2']
lst.reverse()

```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.reverse()
print(fruits) # ['lemon', 'mango', 'orange', 'banana']
ages = [22, 19, 24, 25, 26, 24, 25, 24]
ages.reverse()
print(ages) # [24, 25, 24, 26, 25, 24, 19, 22]
```

### Sorting List Items

To sort lists, we can use the `sort()` method or the built-in `sorted()` function. The `sort()` method reorders the items and modifies the original list. If the `reverse` argument of `sort()` is `True`, it will arrange the list in descending order.

- sort(): this method modifies the original list

  ```py
  # syntax
  lst = ['item1', 'item2']
  lst.sort()                # ascending
  lst.sort(reverse=True)    # descending
  ```

  **Example:**

  ```py
  fruits = ['banana', 'orange', 'mango', 'lemon']
  fruits.sort()
  print(fruits)             # sorted in alphabetical order, ['banana', 'lemon', 'mango', 'orange']
  fruits.sort(reverse=True)
  print(fruits) # ['orange', 'mango', 'lemon', 'banana']
  ages = [22, 19, 24, 25, 26, 24, 25, 24]
  ages.sort()
  print(ages) #  [19, 22, 24, 24, 24, 25, 25, 26]
 
  ages.sort(reverse=True)
  print(ages) #  [26, 25, 25, 24, 24, 24, 22, 19]
  ```

  `sorted()` returns a new sorted list without modifying the original list.
  **Example:**

  ```py
  fruits = ['banana', 'orange', 'mango', 'lemon']
  print(sorted(fruits))   # ['banana', 'lemon', 'mango', 'orange']
  # Reverse order
  fruits = ['banana', 'orange', 'mango', 'lemon']
  fruits = sorted(fruits,reverse=True)
  print(fruits)     # ['orange', 'mango', 'lemon', 'banana']
  ```

🌕 You have completed Day 5 and covered the core operations you need to work confidently with Python lists. Now practice the exercises below.

### Quick List Method Reference

| Method / Function | Purpose | Example |
|---|---|---|
| `append()` | Adds one item to the end | `items.append('Python')` |
| `insert()` | Adds an item at an index | `items.insert(1, 'SQL')` |
| `remove()` | Removes the first matching item | `items.remove('SQL')` |
| `pop()` | Removes and returns an item | `items.pop()` |
| `clear()` | Removes all items | `items.clear()` |
| `copy()` | Creates a shallow copy | `new = items.copy()` |
| `count()` | Counts an item's occurrences | `items.count('Python')` |
| `index()` | Finds the first matching index | `items.index('Python')` |
| `reverse()` | Reverses the original list | `items.reverse()` |
| `sort()` | Sorts the original list | `items.sort()` |
| `sorted()` | Returns a new sorted list | `sorted(items)` |

## 💻 Exercises: Day 5

### Exercises: Level 1

1. Declare an empty list
2. Declare a list with more than 5 items
3. Find the length of your list
4. Get the first item, the middle item and the last item of the list
5. Declare a list called mixed_data_types, put your(name, age, height, marital status, address)
6. Declare a list variable named it_companies and assign initial values Facebook, Google, Microsoft, Apple, IBM, Oracle and Amazon.
7. Print the list using _print()_
8. Print the number of companies in the list
9. Print the first, middle and last company
10. Print the list after modifying one of the companies
11. Add an IT company to it_companies
12. Insert an IT company in the middle of the companies list
13. Change one of the it_companies names to uppercase (IBM excluded!)
14. Join the it_companies with a string '#;&nbsp; '
15. Check if a certain company exists in the it_companies list.
16. Sort the list using sort() method
17. Reverse the list in descending order using reverse() method
18. Slice out the first 3 companies from the list
19. Slice out the last 3 companies from the list
20. Slice out the middle IT company or companies from the list
21. Remove the first IT company from the list
22. Remove the middle IT company or companies from the list
23. Remove the last IT company from the list
24. Remove all IT companies from the list
25. Destroy the IT companies list
26. Join the following lists:

    ```py
    front_end = ['HTML', 'CSS', 'JavaScript', 'React', 'Redux']
    back_end = ['Node','Express', 'MongoDB']
    ```

27. After joining the lists in question 26. Copy the joined list and assign it to a variable full_stack, then insert Python and SQL after Redux.

### Exercises: Level 2

1. The following is a list of 10 students ages:

```sh
ages = [19, 22, 19, 24, 20, 25, 26, 24, 25, 24]
```

- Sort the list and find the min and max age
- Add the min age and the max age again to the list
- Find the median age (one middle item or two middle items divided by two)
- Find the average age (sum of all items divided by their number )
- Find the range of the ages (max minus min)
- Compare the value of (min - average) and (max - average), use _abs()_ method


🎉 CONGRATULATIONS! 🎉

[<< Day 4](../Day_04_Strings/04_Strings.md) | [Day 6 >>](../Day_06_Tuples/06_Tuples.md)
