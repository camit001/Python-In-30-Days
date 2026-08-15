<div align="center">
  <h1>Python In 30 Days: Day 23 - Virtual Environment</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>
</div>

[<< Day 22](../Day_22_Web_scraping/22_Web_scraping.md) | [Day 24 >>](../Day_24_Statistics (NumPy)/24_Statistics (NumPy).md)

**Python In 30 Days**

- [📘 Day 23](#-day-23)
  - [Setting up Virtual Environments](#setting-up-virtual-environments)
    - [What is a Virtual Environment](#what-is-a-virtual-environment)
    - [Creating a Virtual Environment](#creating-a-virtual-environment)
    - [Activating the Virtual Environment](#activating-the-virtual-environment)
    - [Installing Packages](#installing-packages)
    - [Checking Installed Packages](#checking-installed-packages)
    - [Creating requirements.txt](#creating-requirementstxt)
    - [Installing from requirements.txt](#installing-from-requirementstxt)
    - [Deactivating the Virtual Environment](#deactivating-the-virtual-environment)
    - [Deleting a Virtual Environment](#deleting-a-virtual-environment)
    - [Using .gitignore](#using-gitignore)
    - [Practical Project Structure](#practical-project-structure)
    - [Troubleshooting](#troubleshooting)
  - [💻 Exercises: Day 23](#-exercises-day-23)

# 📘 Day 23

## Setting up Virtual Environments

### What is a Virtual Environment

A virtual environment is an isolated Python environment for a project. It allows each project to have its own Python packages and package versions without interfering with other projects.

For example:

```text
Project A
   └── .venv
       ├── requests
       └── pandas

Project B
   └── .venv
       ├── requests
       └── numpy
```

This isolation helps prevent dependency conflicts between projects.

A virtual environment is usually created inside the project directory and is commonly named `.venv` or `venv`.

---

### Creating a Virtual Environment

Python includes the `venv` module, so an additional `virtualenv` installation is usually not required for a basic environment.

Create a project directory:

```sh
mkdir flask_project
cd flask_project
```

Create a virtual environment:

```sh
python -m venv .venv
```

On some systems, you may need:

```sh
python3 -m venv .venv
```

The resulting structure will look similar to:

```text
flask_project/
└── .venv/
```

You can name the environment `venv` instead:

```sh
python -m venv venv
```

---

## Activating the Virtual Environment

### Windows Command Prompt

```sh
.venv\Scripts\activate
```

### Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

### macOS / Linux

```sh
source .venv/bin/activate
```

After activation, your terminal usually displays the environment name:

```text
(.venv) C:\Users\Amit\Documents\flask_project>
```

or:

```text
(.venv) amit@computer:~/flask_project$
```

The exact prompt depends on your operating system and shell.

---

## Installing Packages

Once the environment is active, install packages into that environment.

For example:

```sh
python -m pip install Flask
```

Install multiple packages:

```sh
python -m pip install Flask requests
```

For a data engineering project:

```sh
python -m pip install pandas numpy requests
```

Using `python -m pip` makes it clearer that pip belongs to the Python interpreter associated with the current environment.

---

## Checking Installed Packages

Use:

```sh
python -m pip list
```

You can also inspect a specific package:

```sh
python -m pip show Flask
```

To see the exact installed dependency versions:

```sh
python -m pip freeze
```

Example:

```text
Flask==3.x.x
requests==2.x.x
```

Package versions will depend on when you install them.

---

## Creating `requirements.txt`

A `requirements.txt` file records the dependencies required by a project.

Create it from the active environment:

```sh
python -m pip freeze > requirements.txt
```

Example:

```text
Flask==3.x.x
requests==2.x.x
```

A typical project can therefore contain:

```text
flask_project/
│
├── .venv/
├── app.py
├── requirements.txt
└── .gitignore
```

The `.venv` folder contains the environment, while `requirements.txt` describes the packages needed to recreate it.

---

## Installing from `requirements.txt`

When another developer gets the project, they can create a new environment:

```sh
python -m venv .venv
```

Activate it and install the dependencies:

```sh
python -m pip install -r requirements.txt
```

This makes it much easier to reproduce the project's Python dependencies.

---

## Deactivating the Virtual Environment

When you finish working, deactivate the environment:

```sh
deactivate
```

The `(.venv)` prefix will disappear from the terminal.

You do not need to delete the environment after deactivating it.

---

## Deleting a Virtual Environment

A virtual environment is just a directory.

First deactivate it:

```sh
deactivate
```

Then delete the `.venv` folder.

### Windows Command Prompt

```sh
rmdir /s /q .venv
```

### macOS / Linux

```sh
rm -rf .venv
```

Be careful with deletion commands. Computers are extremely literal about destroying things.

---

## Using `.gitignore`

You normally should **not commit `.venv` to Git** because it can contain many generated files and platform-specific binaries.

Create a `.gitignore` file:

```gitignore
.venv/
venv/
__pycache__/
*.pyc
.env
```

Commit:

```text
requirements.txt
```

instead of:

```text
.venv/
```

The repository can then be recreated using:

```sh
python -m venv .venv
python -m pip install -r requirements.txt
```

---

## Practical Project Structure

A small Python project might look like this:

```text
employee-data-project/
│
├── .venv/
├── data/
│   ├── input/
│   └── output/
├── src/
│   ├── extract.py
│   ├── transform.py
│   └── load.py
├── tests/
│   └── test_transform.py
├── .gitignore
├── requirements.txt
└── README.md
```

For a Data Engineering project:

```text
Source Files / API
        ↓
     Extract
        ↓
    Transform
        ↓
      Load
        ↓
Database / Data Lake
```

The virtual environment isolates the Python dependencies used by the extraction, transformation, testing, and loading code.

---

## Using Different Python Versions

A virtual environment is created from a particular Python interpreter.

Check your Python version:

```sh
python --version
```

You can create an environment using a specific Python executable when multiple versions are installed.

For example:

```sh
py -3.13 -m venv .venv
```

On systems where `python3.13` is available:

```sh
python3.13 -m venv .venv
```

Then verify:

```sh
python --version
```

The environment will use the interpreter with which it was created.

---

## Upgrading pip

Inside the activated environment:

```sh
python -m pip install --upgrade pip
```

Then verify:

```sh
python -m pip --version
```

---

## Troubleshooting

### `python` is not recognized

On Windows, try:

```sh
py --version
```

Then:

```sh
py -m venv .venv
```

### PowerShell blocks activation

If PowerShell prevents the activation script from running, you can use another shell such as Command Prompt, or configure PowerShell execution policy according to your organization's security requirements.

You can also invoke the environment's Python directly without activating it:

```powershell
.venv\Scripts\python.exe --version
```

### Package installed globally instead of in the environment

Check which Python is being used:

```sh
python --version
python -m pip --version
```

Make sure the terminal shows `(.venv)` before installing packages.

---

## Virtual Environment Workflow

A typical workflow is:

```text
Create Project
      ↓
Create .venv
      ↓
Activate .venv
      ↓
Install Packages
      ↓
Develop / Test
      ↓
Freeze Dependencies
      ↓
Save requirements.txt
      ↓
Deactivate
```

For a new machine:

```text
Clone Project
      ↓
Create .venv
      ↓
Activate .venv
      ↓
Install requirements.txt
      ↓
Run Project
```

---

## Practical Data Engineering Example

Suppose you are creating a Python ETL project that reads CSV files, transforms the data with pandas, and sends the result to an API.

Create the environment:

```sh
python -m venv .venv
```

Activate it:

```sh
.venv\Scripts\activate
```

Install dependencies:

```sh
python -m pip install pandas requests
```

Create the project:

```text
employee-etl/
│
├── .venv/
├── data/
│   └── employees.csv
├── src/
│   ├── extract.py
│   ├── transform.py
│   └── load.py
├── requirements.txt
└── .gitignore
```

Export dependencies:

```sh
python -m pip freeze > requirements.txt
```

Now another developer can reproduce the environment with:

```sh
python -m venv .venv
python -m pip install -r requirements.txt
```

This is a basic example of dependency isolation and reproducibility, which becomes particularly important when Python code is eventually moved into scheduled pipelines, CI/CD, or cloud environments.

---

## 💻 Exercises: Day 23

### Exercises: Level 1

1. Create a project directory called `python_project`.
2. Create a virtual environment named `.venv`.
3. Activate the environment.
4. Check the Python version.
5. Check the pip version.
6. Install `requests`.
7. Install `pandas`.
8. Display the installed packages using `python -m pip list`.
9. Display the details of `pandas` using `python -m pip show pandas`.
10. Deactivate the virtual environment.

### Exercises: Level 2

1. Create a `requirements.txt` file from your environment.
2. Create a second virtual environment.
3. Install all packages from `requirements.txt`.
4. Verify that the required packages are installed.
5. Create a `.gitignore` file that ignores `.venv/`.
6. Delete the second virtual environment.
7. Recreate it from scratch.
8. Upgrade pip inside the environment.
9. Install a specific version of a package.
10. Check for outdated packages.

### Exercises: Level 3 - Data Engineering

1. Create an `employee-etl` project with the following structure:

```text
employee-etl/
├── .venv/
├── data/
│   ├── input/
│   └── output/
├── src/
│   ├── extract.py
│   ├── transform.py
│   └── load.py
├── requirements.txt
└── .gitignore
```

2. Create the virtual environment.
3. Install `pandas` and `requests`.
4. Create `requirements.txt`.
5. Write a Python program that reads a CSV file using pandas.
6. Transform one column.
7. Save the transformed data to the output folder.
8. Add the virtual environment to `.gitignore`.
9. Explain why `.venv` should not normally be committed to Git.
10. Explain how another developer can recreate your environment using `requirements.txt`.

### Exercises: Level 4 - Practical Project

Build a small Python ETL project that:

```text
CSV / API
   ↓
Extract
   ↓
Validate
   ↓
Transform
   ↓
Save Output
```

Requirements:

1. Use a virtual environment.
2. Use `pandas`.
3. Use `requests`.
4. Store dependencies in `requirements.txt`.
5. Add `.venv/` to `.gitignore`.
6. Separate the code into `extract.py`, `transform.py`, and `load.py`.
7. Add basic exception handling.
8. Document the setup commands in `README.md`.

🎉 CONGRATULATIONS! 🎉

[<< Day 22](../Day_22_Web_scraping/22_Web_scraping.md) | [Day 24 >>](../Day_24_Statistics Day_24_Statistics (NumPy)/24_Statistics (NumPy).md/24_Statistics (NumPy).md)
