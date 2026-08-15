<div align="center">
  <h1>Python In 30 Days: Day 28 - API</h1>

<sub>Author:
<a href="https://github.com/camit001" target="_blank">Amit Kumar</a><br>

</sub>

</div>

[<< Day 27](../Day_27_Python_with_mongodb/27_Python_with_mongodb.md) | [Day 29 >>](../Day_29_Building_API/29_Building_API.md)

**[Python In 30 Days]**

- [📘 Day 28](#-day-28)
- [Application Programming Interface (API)](#application-programming-interface-api)
  - [API](#api)
  - [Building API](#building-api)
  - [HTTP (Hypertext Transfer Protocol)](#http-hypertext-transfer-protocol)
  - [Structure of HTTP](#structure-of-http)
  - [Initial Request Line](#initial-request-line)
    - [Initial Response Line (Status Line)](#initial-response-line-status-line)
    - [Header Fields](#header-fields)
    - [The Message Body](#the-message-body)
    - [Request Methods](#request-methods)
    - [Common HTTP Status Codes](#common-http-status-codes)
    - [REST API Concepts](#rest-api-concepts)
    - [JSON in APIs](#json-in-apis)
    - [Calling an API with Python](#calling-an-api-with-python)
  - [💻 Exercises: Day 28](#-exercises-day-28)

# 📘 Day 28

## Application Programming Interface (API)

### API

API stands for **Application Programming Interface**. In this section, we focus on **Web APIs**, which allow different applications and services to communicate with each other.

A Web API defines how a client can request data or perform an operation on a server. APIs commonly use **HTTP** for communication and **JSON** for exchanging structured data.

For example, a Python application can request customer data from a server, while another application can send new data to that same server through an API.

Modern Web APIs commonly follow REST-style principles. A REST API uses resources, URLs, HTTP methods, and HTTP status codes to communicate between clients and servers.

> **Note:** API design is broader than REST. REST is one common architectural style for Web APIs.

### Building API

A RESTful API commonly exposes **CRUD** operations:

| Operation | HTTP Method | Typical Purpose |
|---|---|---|
| Create | `POST` | Create a new resource |
| Read | `GET` | Retrieve resources |
| Update | `PUT` / `PATCH` | Update a resource |
| Delete | `DELETE` | Delete a resource |

In the previous sections, we learned Python, Flask, and MongoDB. These technologies can be combined to build a REST API that reads and modifies data stored in MongoDB.

For example:

```text
GET    /students
GET    /students/101
POST   /students
PUT    /students/101
DELETE /students/101
```

Each endpoint represents a resource or an operation on a resource.

## HTTP (Hypertext Transfer Protocol)

HTTP is an application-layer communication protocol used between clients and servers.

A client, such as a browser, mobile application, or Python program, sends an HTTP request to a server. The server processes the request and sends an HTTP response.

The basic communication flow is:

```text
Client
   |
   | HTTP Request
   v
Server
   |
   | HTTP Response
   v
Client
```

An HTTP request can contain:

- HTTP method
- URL/path
- headers
- query parameters
- optional request body

An HTTP response can contain:

- status code
- headers
- optional response body

## Structure of HTTP

HTTP messages generally contain:

1. A start line
2. Zero or more headers
3. A blank line
4. An optional message body

Example request:

```http
GET /students HTTP/1.1
Host: example.com
Accept: application/json
```

Example response:

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "name": "Amit Kumar",
    "city": "Mumbai"
}
```

### Initial Request Line

The initial request line contains:

- HTTP method
- requested path
- HTTP version

Example:

```http
GET /students HTTP/1.1
```

Here:

- `GET` is the HTTP method.
- `/students` is the requested resource.
- `HTTP/1.1` is the HTTP version.

### Initial Response Line (Status Line)

The response status line contains:

- HTTP version
- status code
- reason phrase

Example:

```http
HTTP/1.1 200 OK
```

The status code tells the client what happened with the request.

### Common HTTP Status Codes

| Status Code | Meaning | Typical Use |
|---|---|---|
| `200 OK` | Request succeeded | Successful GET/update response |
| `201 Created` | Resource created | Successful POST |
| `204 No Content` | Success with no response body | Successful DELETE |
| `400 Bad Request` | Invalid request | Missing/invalid input |
| `401 Unauthorized` | Authentication required/failed | Invalid credentials/token |
| `403 Forbidden` | Access denied | User lacks permission |
| `404 Not Found` | Resource not found | Invalid endpoint or ID |
| `405 Method Not Allowed` | Method not supported | Wrong HTTP method |
| `500 Internal Server Error` | Server-side failure | Unexpected application error |

A useful rule for beginners is:

```text
2xx = success
4xx = client/request problem
5xx = server problem
```

## Header Fields

Headers provide additional information about an HTTP request or response.

Example:

```http
GET /students HTTP/1.1
Host: example.com
Accept: application/json
Authorization: Bearer <token>
```

Common headers include:

- `Content-Type`: describes the format of the message body.
- `Accept`: tells the server which response format the client prefers.
- `Authorization`: carries authentication information.
- `User-Agent`: identifies the client.
- `Cache-Control`: provides caching instructions.

For JSON APIs, you will commonly see:

```http
Content-Type: application/json
```

## The Message Body

An HTTP message can contain a body.

For a `POST` or `PUT` request, the body commonly contains the data being sent to the server.

Example:

```http
POST /students HTTP/1.1
Content-Type: application/json

{
    "name": "Amit Kumar",
    "country": "India",
    "city": "Mumbai",
    "age": 25
}
```

The `Content-Type` header tells the server how to interpret the body.

## Request Methods

The most common HTTP methods used when building REST APIs are:

### 1. GET

`GET` retrieves data.

```http
GET /students
```

A GET request should not be used to modify server-side data.

### 2. POST

`POST` creates a new resource or submits data for processing.

```http
POST /students
```

Example JSON body:

```json
{
    "name": "Amit Kumar",
    "city": "Mumbai"
}
```

### 3. PUT

`PUT` is commonly used to replace the representation of an existing resource.

```http
PUT /students/101
```

### 4. PATCH

`PATCH` is commonly used for a partial update.

```http
PATCH /students/101
```

For example, changing only the student's city without sending every field.

### 5. DELETE

`DELETE` removes a resource.

```http
DELETE /students/101
```

## REST API Concepts

A REST API usually organizes data around **resources**.

For example, if the resource is `students`:

```text
GET    /students       -> Get all students
GET    /students/101   -> Get student 101
POST   /students       -> Create a student
PUT    /students/101   -> Replace student 101
PATCH  /students/101   -> Partially update student 101
DELETE /students/101   -> Delete student 101
```

### Path Parameters

A path parameter identifies a specific resource.

```text
/students/101
```

Here `101` can represent a student ID.

### Query Parameters

Query parameters are useful for filtering, sorting, pagination, and searching.

```text
/students?city=Mumbai
/students?limit=10
/students?city=Mumbai&sort=name
```

### Request Body

The request body carries data sent to the server, especially with `POST`, `PUT`, and `PATCH`.

## JSON in APIs

JSON stands for **JavaScript Object Notation**. It is one of the most common formats used for API requests and responses.

Example:

```json
{
    "name": "Amit Kumar",
    "country": "India",
    "city": "Mumbai",
    "skills": ["Python", "SQL", "PySpark"]
}
```

The equivalent Python dictionary is:

```py
student = {
    "name": "Amit Kumar",
    "country": "India",
    "city": "Mumbai",
    "skills": ["Python", "SQL", "PySpark"]
}
```

When working with APIs, JSON data is commonly converted between Python objects and JSON using the `json` module.

```py
import json

student = {
    "name": "Amit Kumar",
    "city": "Mumbai"
}

json_data = json.dumps(student)
print(json_data)

python_data = json.loads(json_data)
print(python_data)
```

## Calling an API with Python

Python can consume APIs using libraries such as `requests`.

Install it with:

```sh
pip install requests
```

Example:

```py
import requests

url = "https://api.github.com"

response = requests.get(url)

print(response.status_code)
print(response.headers.get("Content-Type"))
print(response.json())
```

### Sending Query Parameters

Instead of manually building a URL, pass query parameters using `params`.

```py
import requests

url = "https://api.example.com/students"

params = {
    "city": "Mumbai",
    "limit": 10
}

response = requests.get(url, params=params)

print(response.url)
print(response.status_code)
```

### Sending JSON Data

```py
import requests

url = "https://api.example.com/students"

student = {
    "name": "Amit Kumar",
    "city": "Mumbai"
}

response = requests.post(url, json=student)

print(response.status_code)
print(response.json())
```

### Handling API Errors

Do not assume every request succeeds. Computers enjoy disappointing people at inconvenient moments.

```py
import requests

response = requests.get("https://api.example.com/students")

if response.ok:
    print(response.json())
else:
    print("Request failed:", response.status_code)
```

You can also use:

```py
response.raise_for_status()
```

This raises an exception when the response contains an HTTP error status.

## Simple Flask API Example

The following example shows the basic structure of a Flask API.

```py
from flask import Flask, jsonify

app = Flask(__name__)

students = [
    {
        "id": 1,
        "name": "Amit Kumar",
        "city": "Mumbai"
    },
    {
        "id": 2,
        "name": "Rahul Sharma",
        "city": "Pune"
    }
]

@app.get("/students")
def get_students():
    return jsonify(students)

@app.get("/students/<int:student_id>")
def get_student(student_id):
    for student in students:
        if student["id"] == student_id:
            return jsonify(student)

    return jsonify({"error": "Student not found"}), 404

if __name__ == "__main__":
    app.run(debug=True)
```

Run:

```sh
python app.py
```

Then request:

```text
http://127.0.0.1:5000/students
```

This example uses an in-memory Python list. In a real application, the data would normally come from a database such as MongoDB or PostgreSQL.

## API Best Practices

When designing an API:

1. Use meaningful resource names.
2. Use the appropriate HTTP method.
3. Return meaningful HTTP status codes.
4. Validate incoming data.
5. Keep secrets such as API keys and database passwords out of source code.
6. Return consistent JSON responses.
7. Add authentication and authorization when required.
8. Use pagination for large collections.
9. Log errors without exposing sensitive information.
10. Document your endpoints.

A simple response format can make an API easier to consume:

```json
{
    "success": true,
    "data": {
        "id": 101,
        "name": "Amit Kumar"
    },
    "message": "Student retrieved successfully"
}
```

## 💻 Exercises: Day 28

### Exercises: Level 1

1. Read about APIs and HTTP.
2. Explain the difference between a client and a server.
3. Explain the difference between `GET`, `POST`, `PUT`, `PATCH`, and `DELETE`.
4. Explain the difference between path parameters and query parameters.
5. Explain the meaning of HTTP status codes `200`, `201`, `400`, `401`, `403`, `404`, and `500`.

### Exercises: Level 2

1. Install the `requests` package.
2. Call a public API using `requests.get()`.
3. Print the status code.
4. Print the response headers.
5. Convert the response to JSON using `.json()`.
6. Pass query parameters using the `params` argument.
7. Handle unsuccessful requests using `raise_for_status()`.

### Exercises: Level 3

Build a Flask API for a `students` resource.

Implement:

```text
GET    /students
GET    /students/<id>
POST   /students
PUT    /students/<id>
PATCH  /students/<id>
DELETE /students/<id>
```

Return appropriate HTTP status codes and JSON responses.

### Exercises: Level 4 - Data Engineering Practice

Build a small **Employee Data API** using Flask.

Create endpoints to:

1. Get all employees.
2. Get an employee by ID.
3. Filter employees by city.
4. Filter employees by department.
5. Add a new employee.
6. Update an employee.
7. Delete an employee.
8. Add pagination using `limit` and `offset`.
9. Store the employee data in MongoDB.
10. Return consistent JSON responses.

Example:

```text
GET /employees?department=Data%20Engineering&limit=10&offset=0
```

🎉 CONGRATULATIONS! 🎉

[<< Day 27](../Day_27_Python_with_mongodb/27_Python_with_mongodb.md) | [Day 29 >>](../Day_29_Building_API/29_Building_API.md)
