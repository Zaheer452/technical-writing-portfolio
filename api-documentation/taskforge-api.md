# TaskForge API Documentation

**Version:** 1.0  
**Base URL:** `https://api.taskforge.com/v1`  

---

## Overview
TaskForge API allows developers to manage tasks, projects, and user authentication programmatically. This documentation covers authentication, task management endpoints, and common error handling.

---

## Authentication

**Method:** JWT (JSON Web Token)  

**Endpoint:** `/auth/login`  
**Method:** POST  

**Request Example:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123"
}

Response Example:

{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "expires_in": 3600
}

Notes:
	•	Include the token in the Authorization header as Bearer <token> for all protected endpoints.
	•	Tokens expire in 1 hour. Refresh tokens can be requested via /auth/refresh.

⸻

Endpoints

1️⃣ Create Task

Endpoint: /tasks
Method: POST

Request Example:

{
  "title": "Finish quarterly report",
  "description": "Compile and submit the Q1 report",
  "due_date": "2026-02-28T23:59:59Z",
  "assigned_to": "user_id_123"
}

Response Example:

{
  "id": "task_456",
  "title": "Finish quarterly report",
  "status": "pending",
  "created_at": "2026-01-31T10:00:00Z"
}

Error Codes:
	•	400: Bad Request (missing fields)
	•	401: Unauthorized (invalid token)
	•	404: User not found

⸻

2️⃣ Get Tasks

Endpoint: /tasks
Method: GET

Query Parameters (optional):
	•	status – Filter by task status (pending, completed)
	•	assigned_to – Filter by user ID

Response Example:

[
  {
    "id": "task_456",
    "title": "Finish quarterly report",
    "status": "pending",
    "due_date": "2026-02-28T23:59:59Z"
  },
  {
    "id": "task_789",
    "title": "Update client presentation",
    "status": "completed",
    "due_date": "2026-01-25T12:00:00Z"
  }
]


⸻

3️⃣ Update Task

Endpoint: /tasks/{id}
Method: PUT

Request Example:

{
  "status": "completed"
}

Response Example:

{
  "id": "task_456",
  "title": "Finish quarterly report",
  "status": "completed"
}


⸻

4️⃣ Delete Task

Endpoint: /tasks/{id}
Method: DELETE

Response Example:

{
  "message": "Task deleted successfully."
}


⸻

Error Handling

Code	Message	Description
400	Bad Request	Invalid input or missing fields
401	Unauthorized	Missing or invalid token
403	Forbidden	Access denied
404	Not Found	Resource does not exist
500	Internal Server Error	Unexpected server error


⸻

Notes
	•	All timestamps are in ISO 8601 UTC format.
	•	Use Content-Type: application/json in headers for all requests.
	•	Rate limit: 100 requests per minute per API key.


