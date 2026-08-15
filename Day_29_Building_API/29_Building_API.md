
<div align="center">
  <h1> Python In 30 Days: Day 29 - Building an API </h1>
  

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>

</div>

[<< Day 28](../Day_28_API/28_API.md) | [Day 30 >>](../Day_30_Conclusions/30_Conclusions.md)

**[Python In 30 Days]**

- [Day 29](#day-29)
- [Building API](#building-api)
  - [Structure of an API](#structure-of-an-api)
  - [Retrieving data using get](#retrieving-data-using-get)
  - [Getting a document by id](#getting-a-document-by-id)
  - [Creating data using POST](#creating-data-using-post)
  - [Updating using PUT](#updating-using-put)
  - [Deleting a document using Delete](#deleting-a-document-using-delete)
- [💻 Exercises: Day 29](#-exercises-day-29)

## Day 29

## Building API


In this section, we will cove a RESTful API that uses HTTP request methods to GET, PUT, POST and DELETE data.

RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. In the previous sections, we have learned about python, flask and mongoDB. We will use the knowledge we acquire to develop a RESTful API using python flask and mongoDB. Every application which has CRUD(Create, Read, Update, Delete) operation has an API to create data, to get data, to update data or to delete data from database.

The browser can handle only get request. Therefore, we have to have a tool which can help us to handle all request methods(GET, POST, PUT, DELETE).

Examples of API

- Countries API: https://restcountries.com/
- Cats breed API: https://api.thecatapi.com/v1/breeds

[Postman](https://www.postman.com/) is a very popular tool when it comes to API development. So, if you like to do this section you need to [download postman](https://www.postman.com/). An alternative of Postman is [Insomnia](https://insomnia.rest/download).

**[Postman]**

### Structure of an API

An API end point is a URL which can help to retrieve, create, update or delete a resource. The structure looks like this:
Example:
https://api.twitter.com/1.1/lists/members.json
Returns the members of the specified list. Private list members will only be shown if the authenticated user owns the specified list.
The name of the company name followed by version followed by the purpose of the API.
The methods:
HTTP methods & URLs

The API uses the following HTTP methods for object manipulation:

```sh
GET        Used for object retrieval
POST       Used for object creation and object actions
PUT        Used for object update
DELETE     Used for object deletion
```

Let us build an API which collects information about Python In 30 Days students. We will collect the name, country, city, date of birth, skills and bio.

To implement this API, we will use:

- Postman
- Python
- Flask
- MongoDB

### Retrieving data using GET

First, create a simple Flask API using in-memory data. This lets us understand the API structure before introducing MongoDB.

```py
from flask import Flask, jsonify

app = Flask(__name__)

students = [
    {
        "id": 1,
        "name": "Amit Kumar",
        "country": "India",
        "city": "Mumbai",
        "skills": ["Python", "SQL", "PySpark"]
    },
    {
        "id": 2,
        "name": "Rahul Sharma",
        "country": "India",
        "city": "Pune",
        "skills": ["Python", "Flask", "MongoDB"]
    },
    {
        "id": 3,
        "name": "Priya Patel",
        "country": "India",
        "city": "Ahmedabad",
        "skills": ["Java", "SQL", "REST API"]
    }
]


@app.get("/api/v1/students")
def get_students():
    return jsonify(students)


if __name__ == "__main__":
    app.run(debug=True)
```

Run:

```sh
python app.py
```

Then open:

```text
http://127.0.0.1:5000/api/v1/students
```

### Getting a document by ID

We can add a path parameter to retrieve one student.

```py
@app.get("/api/v1/students/<int:student_id>")
def get_student(student_id):
    for student in students:
        if student["id"] == student_id:
            return jsonify(student)

    return jsonify({"error": "Student not found"}), 404
```

Example:

```text
GET /api/v1/students/1
```

### Connecting Flask with MongoDB

For a real application, data should normally be stored in a database instead of an in-memory list.

Install the required packages:

```sh
pip install Flask pymongo
```

Use an environment variable for the MongoDB connection string. Never hard-code database credentials in source code.

```py
import os
from flask import Flask, jsonify
from pymongo import MongoClient

app = Flask(__name__)

MONGODB_URI = os.environ["MONGODB_URI"]

client = MongoClient(MONGODB_URI)
db = client["python_api"]
students_collection = db["students"]
```

For local MongoDB:

```text
mongodb://localhost:27017/
```

For MongoDB Atlas, use the connection string supplied by your Atlas deployment and keep it in an environment variable.

### Retrieving MongoDB documents

MongoDB uses an `ObjectId` for the default `_id` field. Convert it to a string before returning JSON.

```py
@app.get("/api/v1/students")
def get_students():
    students = list(students_collection.find())

    for student in students:
        student["_id"] = str(student["_id"])

    return jsonify(students)
```

### Creating data using POST

We use `POST` to create a new student.

```py
from flask import request

@app.post("/api/v1/students")
def create_student():
    data = request.get_json()

    if not data:
        return jsonify({"error": "JSON body is required"}), 400

    required_fields = ["name", "country", "city", "skills"]

    for field in required_fields:
        if field not in data:
            return jsonify({"error": f"{field} is required"}), 400

    result = students_collection.insert_one(data)

    return jsonify({
        "message": "Student created successfully",
        "id": str(result.inserted_id)
    }), 201
```

Example JSON:

```json
{
    "name": "Neha Singh",
    "country": "India",
    "city": "Delhi",
    "skills": ["Python", "SQL", "Databricks"]
}
```

`201 Created` is the appropriate response for successful creation.

### Updating using PUT

`PUT` is commonly used to replace the current representation of a resource.

```py
from bson import ObjectId
from bson.errors import InvalidId

@app.put("/api/v1/students/<student_id>")
def update_student(student_id):
    try:
        object_id = ObjectId(student_id)
    except InvalidId:
        return jsonify({"error": "Invalid student ID"}), 400

    data = request.get_json()

    if not data:
        return jsonify({"error": "JSON body is required"}), 400

    result = students_collection.replace_one(
        {"_id": object_id},
        data
    )

    if result.matched_count == 0:
        return jsonify({"error": "Student not found"}), 404

    return jsonify({
        "message": "Student updated successfully"
    }), 200
```

### Partial updates using PATCH

`PATCH` is useful when only selected fields need to be changed.

```py
@app.patch("/api/v1/students/<student_id>")
def patch_student(student_id):
    try:
        object_id = ObjectId(student_id)
    except InvalidId:
        return jsonify({"error": "Invalid student ID"}), 400

    data = request.get_json()

    if not data:
        return jsonify({"error": "JSON body is required"}), 400

    result = students_collection.update_one(
        {"_id": object_id},
        {"$set": data}
    )

    if result.matched_count == 0:
        return jsonify({"error": "Student not found"}), 404

    return jsonify({
        "message": "Student partially updated successfully"
    }), 200
```

Example body:

```json
{
    "city": "Bengaluru"
}
```

### Deleting a document using DELETE

```py
@app.delete("/api/v1/students/<student_id>")
def delete_student(student_id):
    try:
        object_id = ObjectId(student_id)
    except InvalidId:
        return jsonify({"error": "Invalid student ID"}), 400

    result = students_collection.delete_one({
        "_id": object_id
    })

    if result.deleted_count == 0:
        return jsonify({"error": "Student not found"}), 404

    return "", 204
```

### Complete CRUD API structure

```text
GET     /api/v1/students
GET     /api/v1/students/<id>
POST    /api/v1/students
PUT     /api/v1/students/<id>
PATCH   /api/v1/students/<id>
DELETE  /api/v1/students/<id>
```

CRUD means:

```text
Create -> POST
Read   -> GET
Update -> PUT / PATCH
Delete -> DELETE
```

### Testing the API with Postman

Use Postman to test each endpoint.

#### GET

```text
GET http://127.0.0.1:5000/api/v1/students
```

#### POST

```text
POST http://127.0.0.1:5000/api/v1/students
```

Select:

```text
Body -> raw -> JSON
```

Then send:

```json
{
    "name": "Neha Singh",
    "country": "India",
    "city": "Delhi",
    "skills": ["Python", "SQL", "PySpark"]
}
```

#### PUT

```text
PUT http://127.0.0.1:5000/api/v1/students/<id>
```

#### PATCH

```text
PATCH http://127.0.0.1:5000/api/v1/students/<id>
```

#### DELETE

```text
DELETE http://127.0.0.1:5000/api/v1/students/<id>
```

### API Validation and Error Handling

A production API should validate input and return meaningful status codes.

```py
if not data.get("name"):
    return jsonify({
        "error": "name is required"
    }), 400
```

Common responses:

```text
200 OK
201 Created
204 No Content
400 Bad Request
404 Not Found
500 Internal Server Error
```

### API Security Basics

Avoid:

```py
MONGODB_URI = "mongodb+srv://username:password@..."
```

Prefer:

```py
import os

MONGODB_URI = os.environ["MONGODB_URI"]
```

For production applications, also consider:

- Authentication
- Authorization
- HTTPS
- Input validation
- Rate limiting
- Secure secret management
- Logging and monitoring
- CORS configuration where required

## Data Engineering Connection

APIs are commonly used in data engineering pipelines.

```text
External API
     |
     | GET /sales
     v
Azure Data Factory
     |
     v
ADLS Gen2
     |
     v
Databricks / PySpark
     |
     v
Delta Lake
     |
     v
Analytics / Reporting
```

A data engineer may consume REST APIs, handle pagination, authenticate with tokens, process JSON responses, and load the data into a data lake or warehouse.

Example:

```py
import requests

url = "https://api.example.com/sales"

response = requests.get(url, timeout=30)
response.raise_for_status()

data = response.json()

for record in data:
    print(record)
```

This is where API concepts connect directly with ETL and data engineering work.

## Personal Example

```py
student = {
    "name": "Amit Kumar",
    "country": "India",
    "city": "Mumbai",
    "skills": ["Python", "SQL", "PySpark"]
}

print(student)
```

This structured data can be exposed through a REST API and consumed by applications or data pipelines.

## 💻 Exercises: Day 29

### Exercises: Level 1

1. Implement `GET /api/v1/students` using Flask.
2. Add `GET /api/v1/students/<id>`.
3. Return `404` when a student does not exist.
4. Test both endpoints using Postman.
5. Use Indian sample names such as Amit Kumar, Rahul Sharma, Priya Patel, and Neha Singh.

### Exercises: Level 2

1. Connect the Flask application to MongoDB.
2. Create a `students` collection.
3. Implement `POST /api/v1/students`.
4. Implement `PUT /api/v1/students/<id>`.
5. Implement `PATCH /api/v1/students/<id>`.
6. Implement `DELETE /api/v1/students/<id>`.
7. Return appropriate HTTP status codes.
8. Validate required fields before inserting or updating data.

### Exercises: Level 3

Build a complete Student REST API:

```text
GET     /api/v1/students
GET     /api/v1/students/<id>
POST    /api/v1/students
PUT     /api/v1/students/<id>
PATCH   /api/v1/students/<id>
DELETE  /api/v1/students/<id>
```

Add:

- JSON request and response bodies
- MongoDB persistence
- Input validation
- Error handling
- Proper HTTP status codes
- Postman testing

### Exercises: Level 4 - Data Engineering Practice

Create an **Employee API** using Flask and MongoDB.

Example employee:

```json
{
    "name": "Amit Kumar",
    "department": "Data Engineering",
    "city": "Mumbai",
    "skills": ["SQL", "Python", "PySpark"],
    "experience": 4
}
```

Implement:

```text
GET     /api/v1/employees
GET     /api/v1/employees/<id>
POST    /api/v1/employees
PUT     /api/v1/employees/<id>
PATCH   /api/v1/employees/<id>
DELETE  /api/v1/employees/<id>
```

Then add:

1. Filter employees by department.
2. Filter employees by city.
3. Add pagination using `limit` and `offset`.
4. Add sorting by experience.
5. Return consistent JSON responses.
6. Test every endpoint using Postman.
7. Create a Python script that consumes your API using `requests`.
8. Save the API response as JSON.
9. Design a simple pipeline that loads API data into a data lake.

Example:

```text
REST API
   |
   v
Python / ADF
   |
   v
ADLS Gen2
   |
   v
Databricks + PySpark
   |
   v
Delta Lake
```

🎉 CONGRATULATIONS! 🎉

[<< Day 28](../Day_28_API/28_API.md) | [Day 30 >>](../Day_30_Conclusions/30_Conclusions.md)
