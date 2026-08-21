# Python Data Structures — Complete Notes
### List, Tuple, Set, Dictionary, DataFrame — Operations & Conversions

---

## 1. LIST — Ordered, Mutable, Allows Duplicates

### Creation
```python
lst = [1, 2, 3, 4]
lst2 = list((1, 2, 3))          # from tuple
lst3 = list(range(5))           # [0,1,2,3,4]
lst4 = [x**2 for x in range(5)] # list comprehension
```

### Core Operations
```python
lst.append(5)          # add single item at end
lst.extend([6, 7])      # add multiple items
lst.insert(1, 99)       # insert at index
lst.remove(99)          # remove first occurrence (by value)
lst.pop()                # remove & return last item
lst.pop(0)               # remove & return item at index
lst.clear()               # empty the list
lst.index(3)              # index of first occurrence
lst.count(3)               # count occurrences
lst.sort()                  # sort ascending in-place
lst.sort(reverse=True)       # sort descending
lst.reverse()                 # reverse in-place
lst.copy()                     # shallow copy
sorted(lst)                     # returns new sorted list
len(lst)                          # length
lst[0], lst[-1]                    # indexing
lst[1:3]                            # slicing
lst[::-1]                            # reversed slice
3 in lst                              # membership check
lst + [8, 9]                           # concatenation
lst * 2                                 # repetition
min(lst), max(lst), sum(lst)             # aggregate functions
```

### Conversions FROM List
```python
list_to_tuple = tuple(lst)
list_to_set   = set(lst)                      # removes duplicates, unordered
list_to_dict  = dict(enumerate(lst))          # index:value pairs
list_to_dict2 = {k: v for k, v in zip(keys_list, lst)}  # if you have a keys list
list_to_df    = pd.DataFrame(lst, columns=['col'])
list_to_df2   = pd.DataFrame({'col': lst})
```

---

## 2. TUPLE — Ordered, Immutable, Allows Duplicates

### Creation
```python
tup = (1, 2, 3)
tup2 = tuple([1, 2, 3])      # from list
single = (1,)                 # single-element tuple needs comma
```

### Core Operations
```python
tup.count(2)          # count occurrences
tup.index(2)           # index of first occurrence
len(tup)                 # length
tup[0], tup[-1]            # indexing
tup[1:3]                    # slicing
a, b, c = tup                # unpacking
a, *rest = tup                 # extended unpacking
tup + (4, 5)                     # concatenation
tup * 2                            # repetition
3 in tup                             # membership
# Tuples are immutable: no append/remove/sort/insert directly
```

### Conversions FROM Tuple
```python
tuple_to_list = list(tup)
tuple_to_set  = set(tup)                     # duplicates removed
tuple_to_dict = dict(enumerate(tup))         # or dict of key-value pairs
                # if tuple contains pairs: dict((('a',1), ('b',2)))
tuple_to_df   = pd.DataFrame([tup], columns=['a','b','c'])
tuple_to_df2  = pd.DataFrame(list_of_tuples, columns=[...])  # common for row-wise data
```

---

## 3. SET — Unordered, Mutable, No Duplicates

### Creation
```python
s = {1, 2, 3}
s2 = set([1, 2, 2, 3])        # from list, duplicates removed
s3 = set()                      # empty set (NOT {} — that's a dict)
frozen = frozenset([1, 2, 3])     # immutable set
```

### Core Operations
```python
s.add(4)                  # add single element
s.update([5, 6])           # add multiple elements
s.remove(4)                  # remove element (KeyError if missing)
s.discard(4)                   # remove element (no error if missing)
s.pop()                          # remove & return arbitrary element
s.clear()                          # empty the set

# Set algebra
a | b   or  a.union(b)                    # union
a & b   or  a.intersection(b)              # intersection
a - b   or  a.difference(b)                 # difference
a ^ b   or  a.symmetric_difference(b)        # elements in either, not both

a.issubset(b)          # is a subset of b
a.issuperset(b)          # is a superset of b
a.isdisjoint(b)             # no common elements

3 in s                         # membership
len(s)                           # length
```

### Conversions FROM Set
```python
set_to_list  = list(s)
set_to_tuple = tuple(s)
set_to_dict  = dict(enumerate(s))            # index:value (order not guaranteed)
set_to_df    = pd.DataFrame(list(s), columns=['col'])
```

---

## 4. DICTIONARY — Key-Value Pairs, Mutable, Ordered (Python 3.7+)

### Creation
```python
d = {'a': 1, 'b': 2}
d2 = dict(a=1, b=2)
d3 = dict([('a', 1), ('b', 2)])       # from list of tuples
d4 = dict(zip(keys_list, values_list))  # from two lists
d5 = {k: v**2 for k, v in d.items()}    # dict comprehension
```

### Core Operations
```python
d['a']                      # access value by key
d.get('a')                    # safe access (returns None if missing)
d.get('z', 0)                   # safe access with default
d['c'] = 3                        # add / update key
d.update({'d': 4, 'e': 5})          # merge/update multiple keys
d.pop('a')                            # remove key & return value
d.popitem()                             # remove & return last inserted (key,value)
d.setdefault('f', 10)                     # get value, or set if missing
del d['b']                                  # delete key
d.clear()                                     # empty dict

d.keys()                # view of all keys
d.values()                # view of all values
d.items()                   # view of (key, value) pairs

'a' in d                      # membership check (checks keys)
len(d)                          # number of key-value pairs

for k, v in d.items():            # iterate
    print(k, v)
```

### Conversions FROM Dictionary
```python
dict_to_list_keys   = list(d.keys())
dict_to_list_values = list(d.values())
dict_to_list_items  = list(d.items())     # list of tuples
dict_to_tuple       = tuple(d.items())
dict_to_set_keys    = set(d.keys())
dict_to_df           = pd.DataFrame(list(d.items()), columns=['key','value'])
dict_to_df2          = pd.DataFrame([d])              # dict as a single row
dict_to_df3          = pd.DataFrame(d)                # if values are lists (columns)
dict_to_df4          = pd.DataFrame.from_dict(d, orient='index')  # keys as rows
```

---

## 5. DATAFRAME (pandas) — 2D Labeled, Mutable Table

```python
import pandas as pd
```

### Creation
```python
df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6]})   # from dict of lists
df2 = pd.DataFrame([[1, 4], [2, 5], [3, 6]], columns=['A', 'B'])  # from list of lists
df3 = pd.DataFrame(list_of_dicts)                       # from list of dicts (rows)
df4 = pd.read_csv('file.csv')                              # from CSV
df5 = pd.read_excel('file.xlsx')                              # from Excel
```

### Core Operations
```python
df.head(), df.tail()              # first/last rows
df.shape                            # (rows, cols)
df.columns, df.index                 # labels
df.dtypes                              # column data types
df.info(), df.describe()                 # summary info / stats

df['A']                     # select column (Series)
df[['A', 'B']]                # select multiple columns
df.loc[0]                       # select row by label
df.iloc[0]                        # select row by position
df.loc[0, 'A']                      # specific cell by label
df.iloc[0:2, 0:1]                     # slice by position

df[df['A'] > 1]                          # filter/boolean indexing
df.query('A > 1')                          # query-style filter

df['C'] = df['A'] + df['B']                  # create new column
df.drop('C', axis=1)                           # drop column
df.drop(0, axis=0)                               # drop row
df.rename(columns={'A': 'X'})                      # rename columns

df.sort_values('A')                     # sort by column
df.sort_values('A', ascending=False)      # descending
df.sort_index()                             # sort by index

df.groupby('A').sum()                # group & aggregate
df.groupby('A').agg({'B': 'mean'})     # custom aggregation

df.merge(df2, on='A', how='inner')       # join/merge (inner/left/right/outer)
pd.concat([df, df2])                       # stack/append dataframes

df.isna(), df.isnull()                # check missing values
df.dropna()                              # drop missing rows
df.fillna(0)                               # fill missing values

df.apply(lambda x: x*2)                # apply function to columns
df['A'].map(lambda x: x+1)               # apply function to a Series

df.reset_index(drop=True)                # reset row index
df.set_index('A')                          # set column as index

df.drop_duplicates()                         # remove duplicate rows
df['A'].unique()                               # unique values
df['A'].value_counts()                           # frequency count

df.to_csv('out.csv', index=False)      # export to CSV
df.to_excel('out.xlsx', index=False)     # export to Excel
```

### Conversions FROM DataFrame
```python
df_to_list          = df.values.tolist()          # list of lists (rows)
df_to_list_col       = df['A'].tolist()               # single column to list
df_to_dict           = df.to_dict()                      # {col: {index: value}}
df_to_dict_records    = df.to_dict('records')              # list of row-dicts
df_to_dict_list        = df.to_dict('list')                  # {col: [values]}
df_to_tuple             = list(df.itertuples(index=False))     # list of namedtuples
df_to_set_col             = set(df['A'])                          # unique values as a set
df_to_numpy                = df.to_numpy()                          # NumPy array
df_col_to_series             = df['A']                                 # pandas Series
```

---

## Quick Conversion Cheat-Sheet

| From \ To | List | Tuple | Set | Dict | DataFrame |
|---|---|---|---|---|---|
| **List** | – | `tuple(l)` | `set(l)` | `dict(enumerate(l))` | `pd.DataFrame(l)` |
| **Tuple** | `list(t)` | – | `set(t)` | `dict(enumerate(t))` | `pd.DataFrame([t])` |
| **Set** | `list(s)` | `tuple(s)` | – | `dict(enumerate(s))` | `pd.DataFrame(list(s))` |
| **Dict** | `list(d.items())` | `tuple(d.items())` | `set(d.keys())` | – | `pd.DataFrame(list(d.items()))` |
| **DataFrame** | `df.values.tolist()` | `list(df.itertuples())` | `set(df['col'])` | `df.to_dict()` | – |

---

## Key Characteristics Summary

| Type | Ordered | Mutable | Duplicates | Indexed | Syntax |
|---|---|---|---|---|---|
| List | Yes | Yes | Yes | Yes | `[ ]` |
| Tuple | Yes | No | Yes | Yes | `( )` |
| Set | No | Yes | No | No | `{ }` |
| Dict | Yes (3.7+) | Yes | Keys: No, Values: Yes | By key | `{key: value}` |
| DataFrame | Yes | Yes | Yes | Yes (label/position) | `pd.DataFrame()` |
