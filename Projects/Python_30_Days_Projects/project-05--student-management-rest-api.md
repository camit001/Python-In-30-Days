# Project 05 - Student Management REST API

## Scenario

A college needs a backend service for managing student information.

Build a REST API using:

- Python
- FastAPI
- MongoDB
- PyMongo
- JSON
- REST/HTTP

## Business Requirements

The API must support:

1. Create student.
2. Read all students.
3. Read one student.
4. Update student.
5. Delete student.
6. Validate input.
7. Return meaningful HTTP status codes.
8. Provide API documentation.

## Sample Student

```json
{
    "student_id": "STU001",
    "name": "Amit Kumar",
    "email": "amit@example.com",
    "course": "MCA",
    "semester": 4,
    "skills": [
        "Python",
        "SQL",
        "PySpark"
    ],
    "marks": {
        "python": 85,
        "sql": 90,
        "data_engineering": 88
    }
}
```

## API Design

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/students` | Get all students |
| GET | `/students/{student_id}` | Get one student |
| POST | `/students` | Create student |
| PUT | `/students/{student_id}` | Update student |
| DELETE | `/students/{student_id}` | Delete student |

## Step 1 - Project Structure

```text
student_api/
├── app.py
├── requirements.txt
├── .env
└── .gitignore
```

## Step 2 - Create Virtual Environment

Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

Linux/macOS:

```bash
python -m venv venv
source venv/bin/activate
```

## Step 3 - Install Packages

```bash
pip install fastapi uvicorn pymongo python-dotenv
```

`requirements.txt`:

```text
fastapi
uvicorn
pymongo
python-dotenv
```

## Step 4 - MongoDB Connection

`.env`:

```text
MONGODB_URI=mongodb://localhost:27017/
```

`.gitignore`:

```text
venv/
.env
__pycache__/
```

Never commit credentials or connection secrets.

## Step 5 - Connect to MongoDB

```python
import os

from dotenv import load_dotenv
from pymongo import MongoClient

load_dotenv()

client = MongoClient(os.getenv("MONGODB_URI"))

db = client["student_db"]
students = db["students"]
```

## Step 6 - Create FastAPI App

```python
from fastapi import FastAPI

app = FastAPI(
    title="Student Management API"
)
```

## Step 7 - GET All Students

```python
@app.get("/students")
def get_students():

    return list(
        students.find(
            {},
            {"_id": 0}
        )
    )
```

## Step 8 - GET One Student

```python
from fastapi import HTTPException

@app.get("/students/{student_id}")
def get_student(student_id: str):

    student = students.find_one(
        {"student_id": student_id},
        {"_id": 0}
    )

    if not student:
        raise HTTPException(
            status_code=404,
            detail="Student not found"
        )

    return student
```

## Step 9 - POST Student

```python
from fastapi import status

@app.post(
    "/students",
    status_code=status.HTTP_201_CREATED
)
def create_student(student: dict):

    existing = students.find_one(
        {"student_id": student["student_id"]}
    )

    if existing:
        raise HTTPException(
            status_code=409,
            detail="Student already exists"
        )

    students.insert_one(student)

    return {
        "message": "Student created successfully"
    }
```

## Step 10 - PUT Student

```python
@app.put("/students/{student_id}")
def update_student(
    student_id: str,
    student: dict
):

    result = students.update_one(
        {"student_id": student_id},
        {"$set": student}
    )

    if result.matched_count == 0:
        raise HTTPException(
            status_code=404,
            detail="Student not found"
        )

    return {
        "message": "Student updated successfully"
    }
```

## Step 11 - DELETE Student

```python
@app.delete("/students/{student_id}")
def delete_student(student_id: str):

    result = students.delete_one(
        {"student_id": student_id}
    )

    if result.deleted_count == 0:
        raise HTTPException(
            status_code=404,
            detail="Student not found"
        )

    return {
        "message": "Student deleted successfully"
    }
```

## Complete Starter API

```python
import os

from dotenv import load_dotenv
from fastapi import FastAPI, HTTPException, status
from pymongo import MongoClient

load_dotenv()

client = MongoClient(
    os.getenv("MONGODB_URI")
)

db = client["student_db"]
students = db["students"]

app = FastAPI(
    title="Student Management API"
)


@app.get("/students")
def get_students():

    return list(
        students.find(
            {},
            {"_id": 0}
        )
    )


@app.get("/students/{student_id}")
def get_student(student_id: str):

    student = students.find_one(
        {"student_id": student_id},
        {"_id": 0}
    )

    if not student:
        raise HTTPException(
            status_code=404,
            detail="Student not found"
        )

    return student


@app.post(
    "/students",
    status_code=status.HTTP_201_CREATED
)
def create_student(student: dict):

    existing = students.find_one(
        {"student_id": student["student_id"]}
    )

    if existing:
        raise HTTPException(
            status_code=409,
            detail="Student already exists"
        )

    students.insert_one(student)

    return {
        "message": "Student created successfully"
    }


@app.put("/students/{student_id}")
def update_student(
    student_id: str,
    student: dict
):

    result = students.update_one(
        {"student_id": student_id},
        {"$set": student}
    )

    if result.matched_count == 0:
        raise HTTPException(
            status_code=404,
            detail="Student not found"
        )

    return {
        "message": "Student updated successfully"
    }


@app.delete("/students/{student_id}")
def delete_student(student_id: str):

    result = students.delete_one(
        {"student_id": student_id}
    )

    if result.deleted_count == 0:
        raise HTTPException(
            status_code=404,
            detail="Student not found"
        )

    return {
        "message": "Student deleted successfully"
    }
```

## Step 12 - Run the API

```bash
uvicorn app:app --reload
```

Open:

```text
http://127.0.0.1:8000/docs
```

FastAPI provides interactive API documentation.

## API Questions

### POST

What should happen if `STU001` already exists?

Expected:

```text
HTTP 409 Conflict
```

### GET

What should happen when the requested student does not exist?

Expected:

```text
HTTP 404 Not Found
```

### PUT

How can you update only selected fields rather than replacing the entire resource?

Investigate the difference between `PUT` and `PATCH`.

### DELETE

What should happen when the requested student does not exist?

Expected:

```text
HTTP 404 Not Found
```

## Extra Challenges

### Level 1

1. Add Pydantic models.
2. Validate email.
3. Validate semester.
4. Validate marks from 0 to 100.

### Level 2

1. Add PATCH.
2. Add search by name.
3. Add filtering by course.
4. Add pagination.
5. Add sorting.

### Level 3

1. Add authentication.
2. Add logging.
3. Add unit tests.
4. Add API versioning.
5. Add Docker.
6. Deploy the API.

## Data Engineering Connection

```text
REST API
 ↓
JSON
 ↓
Raw Storage
 ↓
Validation
 ↓
Transformation
 ↓
Database / Data Lake
 ↓
Analytics
```

Important concepts:

- API pagination
- Authentication
- Incremental extraction
- Watermarks
- Retry handling
- Rate limits
- JSON parsing
- Schema validation
- Data quality
- Logging
- Error handling
