# Project 06 - Final Python Data Pipeline

## Scenario

A company receives data from multiple sources:

- CSV files
- REST APIs
- JSON files

The data must be ingested, validated, transformed, and written to a clean output layer.

This is the capstone project for the Python learning path.

## Architecture

```text
CSV Files       REST API       JSON Files
    |              |               |
    +--------------+---------------+
                   |
                   v
             Python Ingestion
                   |
                   v
             Raw Data Layer
                   |
                   v
            Data Validation
                   |
                   v
             Transformation
                   |
                   v
             Clean Data
                   |
                   v
          Analytics / Reporting
```

## Scenario Questions

1. How will you identify duplicate records?
2. How will you handle missing values?
3. How will you validate data types?
4. How will you handle invalid records?
5. How will you log failures?
6. How will you process only new records?
7. How will you handle API pagination?
8. How will you retry a failed API request?
9. How will you store raw data separately from cleaned data?
10. How would this solution scale beyond a local Python script?

## Suggested Folder Structure

```text
python_data_pipeline/
│
├── data/
│   ├── raw/
│   └── clean/
│
├── src/
│   ├── ingestion.py
│   ├── validation.py
│   ├── transformation.py
│   └── main.py
│
├── logs/
│
├── requirements.txt
├── .env
└── README.md
```

## Step 1 - Ingestion

```python
import csv


def read_csv(file_path):
    with open(file_path, "r") as file:
        return list(csv.DictReader(file))
```

## Step 2 - Validation

```python
def validate_student(student):
    required_fields = [
        "student_id",
        "name",
        "email"
    ]

    for field in required_fields:
        if not student.get(field):
            return False

    return True
```

## Step 3 - Remove Invalid Records

```python
valid_records = []
invalid_records = []

for student in students:
    if validate_student(student):
        valid_records.append(student)
    else:
        invalid_records.append(student)
```

## Step 4 - Remove Duplicates

```python
unique_records = {}

for student in valid_records:
    student_id = student["student_id"]
    unique_records[student_id] = student

valid_records = list(unique_records.values())
```

## Step 5 - Transformation

```python
for student in valid_records:
    student["name"] = student["name"].strip()
    student["email"] = student["email"].lower()
```

## Step 6 - Write Clean Data

```python
import json

with open("data/clean/students.json", "w") as file:
    json.dump(valid_records, file, indent=4)
```

## Step 7 - Add Logging

```python
import logging

logging.basicConfig(
    filename="logs/pipeline.log",
    level=logging.INFO
)

logging.info("Pipeline started")
logging.info("Records processed: %s", len(valid_records))
logging.info("Pipeline completed")
```

## Step 8 - Add Error Handling

```python
try:
    students = read_csv("data/raw/students.csv")
except FileNotFoundError:
    logging.exception("Input file was not found")
```

## Step 9 - Incremental Processing

Add a field such as:

```text
updated_at
```

Then process records after the previous successful timestamp.

Conceptually:

```text
Previous Watermark
        |
        v
Read Source
        |
        v
Filter updated_at > watermark
        |
        v
Process New Records
        |
        v
Save New Watermark
```

## Step 10 - Final Pipeline

```python
import csv
import json
import logging


logging.basicConfig(
    filename="pipeline.log",
    level=logging.INFO
)


def read_csv(file_path):
    with open(file_path, "r") as file:
        return list(csv.DictReader(file))


def validate(record):
    return all(
        record.get(field)
        for field in ["student_id", "name", "email"]
    )


def transform(record):
    record["name"] = record["name"].strip()
    record["email"] = record["email"].lower()
    return record


def run_pipeline():

    logging.info("Pipeline started")

    students = read_csv("students.csv")

    valid = []
    invalid = []

    for student in students:

        if validate(student):
            valid.append(transform(student))
        else:
            invalid.append(student)

    unique = {}

    for student in valid:
        unique[student["student_id"]] = student

    valid = list(unique.values())

    with open(
        "clean_students.json",
        "w"
    ) as file:

        json.dump(
            valid,
            file,
            indent=4
        )

    logging.info(
        "Valid records: %s",
        len(valid)
    )

    logging.info(
        "Invalid records: %s",
        len(invalid)
    )

    logging.info("Pipeline completed")


run_pipeline()
```

## Final Challenges

### Beginner

1. Add more validation rules.
2. Create an error CSV.
3. Add summary statistics.
4. Add command-line arguments.

### Intermediate

1. Consume a REST API.
2. Add pagination.
3. Add retries.
4. Add incremental loading.
5. Add configuration through `.env`.

### Advanced

1. Replace CSV processing with Pandas.
2. Store raw data in a database.
3. Store transformed data in PostgreSQL.
4. Schedule the pipeline.
5. Containerize with Docker.
6. Add automated tests.
7. Add CI/CD.
8. Rebuild the pipeline using Azure Data Factory and Databricks.

## Data Engineering Mapping

| Python Concept | Data Engineering Equivalent |
|---|---|
| Function | Reusable pipeline component |
| CSV | Source system |
| JSON | Semi-structured source |
| API | External source |
| Validation | Data quality |
| Transformation | ETL/ELT |
| Logging | Pipeline monitoring |
| Exception handling | Failure handling |
| Watermark | Incremental loading |
| Pandas | Data transformation |
| Database | Target system |
| Scheduler | Orchestration |

## Final Interview Questions

1. How would you design an incremental API ingestion pipeline?
2. How would you handle API rate limits?
3. How would you make the pipeline restartable?
4. How would you prevent duplicate records?
5. How would you implement idempotency?
6. How would you handle schema changes?
7. How would you monitor the pipeline?
8. How would you process millions of records?
9. When would you use Pandas versus PySpark?
10. How would you move this local Python pipeline to Azure?

## Final Architecture

```text
                  SOURCE SYSTEMS
                       |
          +------------+------------+
          |            |            |
         CSV          API          JSON
          |            |            |
          +------------+------------+
                       |
                       v
               INGESTION LAYER
                       |
                       v
                 RAW STORAGE
                       |
                       v
              VALIDATION / DQ
                       |
                       v
                TRANSFORMATION
                       |
                       v
                CLEAN STORAGE
                       |
          +------------+------------+
          |                         |
          v                         v
      DATABASE                 ANALYTICS
          |                         |
          +------------+------------+
                       |
                       v
                   REPORTING
```
