<div align="center">
  <h1> Python In 30 Days: Day 19 - File Handling </h1>
  
<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>
</div>

[<< Day 18](../Day_18_Regular_expressions/18_Regular_expressions.md) | [Day 20 >>](../Day_20_Python_package_manager/20_Python_package_manager.md)

**Python In 30 Days**

- [📘 Day 19](#-day-19)
  - [File Handling](#file-handling)
    - [Opening Files for Reading](#opening-files-for-reading)
    - [Opening Files for Writing and Updating](#opening-files-for-writing-and-updating)
    - [Deleting Files](#deleting-files)
  - [File Types](#file-types)
    - [File with txt Extension](#file-with-txt-extension)
    - [File with json Extension](#file-with-json-extension)
    - [Changing JSON to Dictionary](#changing-json-to-dictionary)
    - [Changing Dictionary to JSON](#changing-dictionary-to-json)
    - [Saving as JSON File](#saving-as-json-file)
    - [File with csv Extension](#file-with-csv-extension)
    - [File with xlsx Extension](#file-with-xlsx-extension)
    - [File with xml Extension](#file-with-xml-extension)
  - [💻 Exercises: Day 19](#-exercises-day-19)
    - [Exercises: Level 1](#exercises-level-1)
    - [Exercises: Level 2](#exercises-level-2)
    - [Exercises: Level 3](#exercises-level-3)

# 📘 Day 19

## File Handling

So far we have seen different Python data types. We usually store our data in different file formats. In addition to handling files, we will also see different file formats(.txt, .json, .xml, .csv, .tsv, .excel) in this section. First, let us get familiar with handling files with common file format(.txt).

File handling is an important part of programming which allows us to create, read, update and delete files. In Python to handle data we use _open()_ built-in function.

```py
# Syntax
open('filename', mode) # mode(r, a, w, x, t,b)  could be to read, write, update
```

- "r" - Read - Default value. Opens a file for reading, it returns an error if the file does not exist
- "a" - Append - Opens a file for appending, creates the file if it does not exist
- "w" - Write - Opens a file for writing, creates the file if it does not exist
- "x" - Create - Creates the specified file, returns an error if the file exists
- "t" - Text - Default value. Text mode
- "b" - Binary - Binary mode (e.g. images)

### Opening Files for Reading

The default mode of _open_ is reading, so we do not have to specify 'r' or 'rt'. I have created and saved a file named reading_file_example.txt in the files directory. Let us see how it is done:

```py
f = open('./files/reading_file_example.txt')
print(f) # <_io.TextIOWrapper name='./files/reading_file_example.txt' mode='r' encoding='UTF-8'>
```

As you can see in the example above, I printed the opened file and it gave  some information about it. Opened file has different reading methods: _read()_, _readline_, _readlines_. An opened file has to be closed with _close()_ method.

- _read()_: read the whole text as string. If we want to limit the number of characters we want to read, we can limit it by passing int value to the *read(number)* method.

```py
f = open('./files/reading_file_example.txt')
txt = f.read()
print(type(txt))
print(txt)
f.close()
```

```sh
# output
<class 'str'>
This is an example to show how to open a file and read.
This is the second line of the text.
```

Instead of printing all the text, let us print the first 10 characters of the text file.

```py
f = open('./files/reading_file_example.txt')
txt = f.read(10)
print(type(txt))
print(txt)
f.close()
```

```sh
# output
<class 'str'>
This is an
```

- _readline()_: read only the first line

```py
f = open('./files/reading_file_example.txt')
line = f.readline()
print(type(line))
print(line)
f.close()
```

```sh
# output
<class 'str'>
This is an example to show how to open a file and read.
```

- _readlines()_: read all the text line by line and returns a list of lines

```py
f = open('./files/reading_file_example.txt')
lines = f.readlines()
print(type(lines))
print(lines)
f.close()
```

```sh
# output
<class 'list'>
['This is an example to show how to open a file and read.\n', 'This is the second line of the text.']
```

Another way to get all the lines as a list is using _splitlines()_:

```py
f = open('./files/reading_file_example.txt')
lines = f.read().splitlines()
print(type(lines))
print(lines)
f.close()
```

```sh
# output
<class 'list'>
['This is an example to show how to open a file and read.', 'This is the second line of the text.']
```

After we open a file, we should close it. There is a high tendency of forgetting to close them. There is a new way of opening files using _with_ - closes the files by itself. Let us rewrite the previous example with the _with_ method:

```py
with open('./files/reading_file_example.txt') as f:
    lines = f.read().splitlines()
    print(type(lines))
    print(lines)
```

```sh
# output
<class 'list'>
['This is an example to show how to open a file and read.', 'This is the second line of the text.']
```

### Opening Files for Writing and Updating

To write to an existing file, we must add a mode as parameter to the _open()_ function:

- "a" - append - will append to the end of the file, if the file does not exist it creates a new file.
- "w" - write - will overwrite any existing content, if the file does not exist it creates.

Let us append some text to the file we have been reading:

```py
with open('./files/reading_file_example.txt','a') as f:
    f.write('This text has to be appended at the end')
```

The method below creates a new file, if the file does not exist:

```py
with open('./files/writing_file_example.txt','w') as f:
    f.write('This text will be written in a newly created file')
```

### Deleting Files

We have seen in previous section, how to make and remove a directory using _os_ module. Again now, if we want to remove a file we use _os_ module.

```py
import os
os.remove('./files/example.txt')

```

If the file does not exist, the remove method will raise an error, so it is good to use a condition like this:

```py
import os
if os.path.exists('./files/example.txt'):
    os.remove('./files/example.txt')
else:
    print('The file does not exist')
```


## Best Practice: `with open()`

The recommended way to work with files is to use `with open(...)`. It automatically closes the file, even if an exception occurs.

```py
with open("./files/reading_file_example.txt", "r", encoding="utf-8") as f:
    content = f.read()

print(content)
```

### File Modes: Quick Reference

| Mode | Meaning | Creates File | Overwrites Existing Content |
|---|---|---:|---:|
| `r` | Read | No | No |
| `w` | Write | Yes | Yes |
| `a` | Append | Yes | No |
| `x` | Create only | Yes | No |
| `r+` | Read and write | No | Can modify |
| `w+` | Write and read | Yes | Yes |
| `a+` | Append and read | Yes | No |

For binary files, add `b`, such as `rb` or `wb`.

### Using `pathlib`

`pathlib` provides a modern and readable way to work with files and directories.

```py
from pathlib import Path

file_path = Path("./files/example.txt")

file_path.write_text("Hello Amit", encoding="utf-8")

content = file_path.read_text(encoding="utf-8")
print(content)

print(file_path.name)
print(file_path.suffix)
print(file_path.exists())
```

### Reading a Large File Line by Line

For large files, process one line at a time instead of loading the entire file into memory.

```py
with open("./files/reading_file_example.txt", "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())
```

### File Position: `tell()` and `seek()`

```py
with open("./files/reading_file_example.txt", "r", encoding="utf-8") as f:
    print(f.tell())

    print(f.read(10))

    print(f.tell())

    f.seek(0)
    print(f.read(10))
```

- `tell()` returns the current file position.
- `seek()` moves the file pointer.

### Handling File Errors

```py
try:
    with open("./files/example.txt", "r", encoding="utf-8") as f:
        print(f.read())
except FileNotFoundError:
    print("The file was not found.")
except PermissionError:
    print("You do not have permission to read this file.")
```

### CSV with `DictReader`

```py
import csv

with open("./files/employees.csv", "r", encoding="utf-8", newline="") as f:
    reader = csv.DictReader(f)

    for row in reader:
        print(row["name"], row["city"])
```

### CSV with `DictWriter`

```py
import csv

employees = [
    {"name": "Amit", "city": "Mumbai"},
    {"name": "Priya", "city": "Pune"},
]

with open("./files/employees.csv", "w", encoding="utf-8", newline="") as f:
    fieldnames = ["name", "city"]

    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(employees)
```

## Practical Data Engineering Example

File handling is important in data engineering because data frequently arrives as CSV, JSON, XML, or text files before being loaded into a database or data lake.

```text
Source File
    ↓
Read File
    ↓
Validate Data
    ↓
Clean / Transform
    ↓
Write Output
    ↓
Load into Database / Data Lake
```

### Process Multiple CSV Files

```py
from pathlib import Path

data_folder = Path("./data")

for file_path in data_folder.glob("*.csv"):
    print("Processing:", file_path.name)
```

### Archive a Processed File

```py
from pathlib import Path
import shutil

source = Path("./data/input.csv")
archive = Path("./data/archive/input.csv")

archive.parent.mkdir(parents=True, exist_ok=True)
shutil.move(source, archive)
```

This is a common pattern after successfully processing an incoming file.

## File Types

### File with txt Extension

File with _txt_ extension is a very common form of data and we have covered it in the previous section. Let us move to the JSON file

### File with json Extension

JSON stands for JavaScriptt Object Notation. Actually, it is a stringified JavaScriptt object or Python dictionary.

_Example:_

```py
# dictionary
person_dct= {
    "name":"Amit",
    "country":"Finland",
    "city":"Helsinki",
    "skills":["JavaScript", "React","Python"]
}
# JSON: A string form a dictionary
person_json = "{'name': 'Amit', 'country': 'Finland', 'city': 'Helsinki', 'skills': ['JavaScript', 'React', 'Python']}"

# we use three quotes and make it multiple line to make it more readable
person_json = '''{
    "name":"Amit",
    "country":"Finland",
    "city":"Helsinki",
    "skills":["JavaScript", "React","Python"]
}'''
```

### Changing JSON to Dictionary

To change a JSON to a dictionary, first we import the json module and then we use _loads_ method.

```py
import json
# JSON
person_json = '''{
    "name": "Amit",
    "country": "Finland",
    "city": "Helsinki",
    "skills": ["JavaScript", "React", "Python"]
}'''
# let's change JSON to dictionary
person_dct = json.loads(person_json)
print(type(person_dct))
print(person_dct)
print(person_dct['name'])
```

```sh
# output
<class 'dict'>
{'name': 'Amit', 'country': 'Finland', 'city': 'Helsinki', 'skills': ['JavaScript', 'React', 'Python']}
Amit
```

### Changing Dictionary to JSON

To change a dictionary to a JSON we use _dumps_ method from the json module.

```py
import json
# python dictionary
person = {
    "name": "Amit",
    "country": "Finland",
    "city": "Helsinki",
    "skills": ["JavaScript", "React", "Python"]
}
# let's convert it to  json
person_json = json.dumps(person, indent=4) # indent could be 2, 4, 8. It beautifies the json
print(type(person_json))
print(person_json)
```

```sh
# output
# when you print it, it does not have the quote, but actually it is a string
# JSON does not have type, it is a string type.
<class 'str'>
{
    "name": "Amit",
    "country": "Finland",
    "city": "Helsinki",
    "skills": [
        "JavaScript",
        "React",
        "Python"
    ]
}
```

### Saving as JSON File

We can also save our data as a json file. Let us save it as a json file using the following steps. For writing a json file, we use the json.dump() method, it can take dictionary, output file, ensure_ascii and indent.

```py
import json
# python dictionary
person = {
    "name": "Amit",
    "country": "Finland",
    "city": "Helsinki",
    "skills": ["JavaScript", "React", "Python"]
}
with open('./files/json_example.json', 'w', encoding='utf-8') as f:
    json.dump(person, f, ensure_ascii=False, indent=4)
```

In the code above, we use encoding and indentation. Indentation makes the json file easy to read.

### File with csv Extension

CSV stands for comma separated values. CSV is a simple file format used to store tabular data, such as a spreadsheet or database. CSV is a very common data format in data science.

**Example:**

```csv
"name","country","city","skills"
"Amit","Finland","Helsinki","JavaScriptt"
```

**Example:**

```py
import csv
with open('./files/csv_example.csv') as f:
    csv_reader = csv.reader(f, delimiter=',') # we use, reader method to read csv
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            print(f'Column names are :{", ".join(row)}')
            line_count += 1
        else:
            print(
                f'\t{row[0]} is a teacher. He lives in {row[1]}, {row[2]}.')
            line_count += 1
    print(f'Number of lines:  {line_count}')
```

```sh
# output:
Column names are :name, country, city, skills
Number of lines:  1
        Amit is a teacher. He lives in Finland, Helsinki.
Number of lines:  2
```

### File with xlsx Extension

To read excel files we need to install _xlrd_ package. We will cover this after we cover package installing using pip.

```py
import xlrd
excel_book = xlrd.open_workbook('sample.xls')
print(excel_book.nsheets)
print(excel_book.sheet_names)
```

### File with xml Extension

XML is another structured data format which looks like HTML. In XML the tags are not predefined. The first line is an XML declaration. The person tag is the root of the XML. The person has a gender attribute.
**Example:XML**

```xml
<?xml version="1.0"?>
<person gender="female">
  <name>Amit</name>
  <country>Finland</country>
  <city>Helsinki</city>
  <skills>
    <skill>JavaScript</skill>
    <skill>React</skill>
    <skill>Python</skill>
  </skills>
</person>
```

For more information on how to read an XML file check the [documentation](https://docs.python.org/3/library/xml.etree.elementtree.html)

```py
import xml.etree.ElementTree as ET
tree = ET.parse('./files/xml_example.xml')
root = tree.getroot()
print('Root tag:', root.tag)
print('Attribute:', root.attrib)
for child in root:
    print('field: ', child.tag)
```

```sh
# output
Root tag: person
Attribute: {'gender': 'male'}
field: name
field: country
field: city
field: skills
```

🌕 You are making a big progress. Maintain your momentum, keep the good work. Now do some exercises for your brain and muscles.

## 💻 Exercises: Day 19

### Exercises: Level 1

1. Write a function which count number of lines and number of words in a text. All the files are in the data folder:
   1) Read obama_speech.txt file and count number of lines and words
   2) Read michelle_obama_speech.txt file and count number of lines and words
   3) Read donald_speech.txt file and count number of lines and words
   4) Read melania_trump_speech.txt file and count number of lines and words
2. Read the countries_data.json data file in data directory, create a function that finds the ten most spoken languages

   ```py
   # Your output should look like this
   print(most_spoken_languages(filename='./data/countries_data.json', 10))
   [(91, 'English'),
   (45, 'French'),
   (25, 'Arabic'),
   (24, 'Spanish'),
   (9, 'Russian'),
   (9, 'Portuguese'),
   (8, 'Dutch'),
   (7, 'German'),
   (5, 'Chinese'),
   (4, 'Swahili'),
   (4, 'Serbian')]

   # Your output should look like this
   print(most_spoken_languages(filename='./data/countries_data.json', 3))
   [(91, 'English'),
   (45, 'French'),
   (25, 'Arabic')]
   ```

3. Read the countries_data.json data file in data directory, create a function that creates a list of the ten most populated countries

   ```py
   # Your output should look like this
   print(most_populated_countries(filename='./data/countries_data.json', 10))

   [
   {'country': 'China', 'population': 1377422166},
   {'country': 'India', 'population': 1295210000},
   {'country': 'United States of America', 'population': 323947000},
   {'country': 'Indonesia', 'population': 258705000},
   {'country': 'Brazil', 'population': 206135893},
   {'country': 'Pakistan', 'population': 194125062},
   {'country': 'Nigeria', 'population': 186988000},
   {'country': 'Bangladesh', 'population': 161006790},
   {'country': 'Russian Federation', 'population': 146599183},
   {'country': 'Japan', 'population': 126960000}
   ]

   # Your output should look like this

   print(most_populated_countries(filename='./data/countries_data.json', 3))
   [
   {'country': 'China', 'population': 1377422166},
   {'country': 'India', 'population': 1295210000},
   {'country': 'United States of America', 'population': 323947000}
   ]
   ```

### Exercises: Level 2

1. Extract all incoming email addresses as a list from the email_exchange_big.txt file.
2. Find the most common words in the English language. Call the name of your function find_most_common_words, it will take two parameters - a string or a file and a positive integer, indicating the number of words. Your function will return an array of tuples in descending order. Check the output

```py
    # Your output should look like this
    print(find_most_common_words('sample.txt', 10))
    [(10, 'the'),
    (8, 'be'),
    (6, 'to'),
    (6, 'of'),
    (5, 'and'),
    (4, 'a'),
    (4, 'in'),
    (3, 'that'),
    (2, 'have'),
    (2, 'I')]

    # Your output should look like this
    print(find_most_common_words('sample.txt', 5))

    [(10, 'the'),
    (8, 'be'),
    (6, 'to'),
    (6, 'of'),
    (5, 'and')]
```

3. Use the function, find_most_frequent_words to find:
   1) The ten most frequent words used in [Obama's speech](https://github.com/Amit/30-Days-Of-Python/blob/master/data/obama_speech.txt)
   2) The ten most frequent words used in [Michelle's speech](https://github.com/Amit/30-Days-Of-Python/blob/master/data/michelle_obama_speech.txt)
   3) The ten most frequent words used in [Trump's speech](https://github.com/Amit/30-Days-Of-Python/blob/master/data/donald_speech.txt)
   4) The ten most frequent words used in [Melania's speech](https://github.com/Amit/30-Days-Of-Python/blob/master/data/melania_trump_speech.txt)
4. Write a python application that checks similarity between two texts. It takes a file or a string as a parameter and it will evaluate the similarity of the two texts. For instance check the similarity between the transcripts of [Michelle's](https://github.com/Amit/30-Days-Of-Python/blob/master/data/michelle_obama_speech.txt) and [Melania's](https://github.com/Amit/30-Days-Of-Python/blob/master/data/melania_trump_speech.txt) speech. You may need a couple of functions, function to clean the text(clean_text), function to remove support words(remove_support_words) and finally to check the similarity(check_text_similarity). List of [stop words](https://github.com/Amit/30-Days-Of-Python/blob/master/data/stop_words.py) are in the data directory
5. Find the 10 most repeated words in the romeo_and_juliet.txt
6. Read the [hacker news csv](https://github.com/Amit/30-Days-Of-Python/blob/master/data/hacker_news.csv) file and find out:
   1) Count the number of lines containing python or Python
   2) Count the number lines containing JavaScriptt, javascript or Javascript
   3) Count the number lines containing Java and not JavaScriptt


### Exercises: Level 4 - Practical File Handling

1. Create a text file and write five employee names to it.
2. Read the file and print each employee name on a separate line.
3. Append a new employee without deleting existing data.
4. Count the number of lines and words in the file.
5. Read a CSV file using `csv.DictReader()` and print employees from Mumbai.
6. Write a list of dictionaries to a CSV file using `csv.DictWriter()`.
7. Read a JSON file using `json.load()` and print the employee names.
8. Create a JSON file containing an employee's name, city, skills, and experience.
9. Use `pathlib` to find every `.csv` file inside a folder.
10. Build a small file-processing program that reads incoming CSV files, validates them, writes cleaned files to an output folder, and moves successfully processed files to an archive folder.

🎉 CONGRATULATIONS ! 🎉

[<< Day 18](../Day_18_Regular_expressions/18_Regular_expressions.md) | [Day 20 >>](../Day_20_Python_package_manager/20_Python_package_manager.md)
