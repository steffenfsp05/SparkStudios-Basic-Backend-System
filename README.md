# Simple Task API (Spring Boot & SQLite)

This is a basic backend API system that manages tasks (create, read, delete) built with Spring Boot, Spring Data JPA, and SQLite.

## Requirements
* Java Development Kit (JDK) 17 or higher
* Maven 3.6+

## Setup Instructions
1. Extract the `.zip` file into a directory of your choice.
2. Open a terminal and navigate to the project root directory.
3. The application will automatically create an SQLite database file named `tasks.db` in the root folder upon its first run.

## How to Run the Server
Run the application using the Maven wrapper included in the project:
```bash
# On Linux/macOS
./mvnw spring-boot:run

# On Windows
mvnw.cmd spring-boot:run
```

*The server will start on `http://localhost:8080`.*

---

## API Endpoint Documentation

> **Note:** The API exclusively accepts and returns data in the `application/json` format.

### 1. Retrieve All Tasks
Returns a list of all tasks stored in the database.

* **Method:** `GET`
* **Path:** `/tasks`

**Success Response (200 OK)**
```json
[
  {
    "id": 1,
    "title": "Finish Trial Task",
    "description": "Complete the Spring Boot backend and SQLite integration."
  }
]
```

---

### 2. Create a New Task
Adds a new task to the system.

* **Method:** `POST`
* **Path:** `/tasks`
* **Headers:** `Content-Type: application/json`

**Request Body**
```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, Eggs, Bread"
}
```

**Success Response (201 Created)**  
Returns the created task object including the newly generated `id`.

**Error Response (400 Bad Request)**  
Occurs if the `title` or `description` field is empty or missing.
```json
{
  "title": "XX is required"
}
```

---

### 3. Delete a Task
Removes a specific task by its unique identifier.

* **Method:** `DELETE`
* **Path:** `/tasks/{id}`
* **Parameter:** `id` (Long) - The ID of the task to delete.

**Success Response (200 OK)**
```json
{
  "message": "Task successfully deleted"
}
```

**Error Response (404 Not Found)**  
Occurs if no task exists with the provided ID.
```json
{
  "error": "Task not found"
}
```
