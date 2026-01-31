# Building a REST API with Node.js and Express: Beginner Guide

This tutorial will walk you through creating a simple REST API using Node.js and Express. By the end, you will have a functioning API capable of handling basic CRUD operations for a task management system.



## Prerequisites
- Node.js installed (v16+ recommended)  
- Basic understanding of JavaScript  
- A code editor (e.g., VS Code)  
- Postman or similar API testing tool


## Step 1: Initialize Project
1. Create a new folder:
```bash
mkdir task-api
cd task-api

	2.	Initialize Node.js:

npm init -y

	3.	Install dependencies:

npm install express body-parser




Step 2: Setup Express Server

Create server.js:

const express = require('express');
const bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.json());

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});

Tip: body-parser allows us to parse JSON requests.


Step 3: Define Routes

3.1 Create Tasks

let tasks = [];

app.post('/tasks', (req, res) => {
  const { title, description } = req.body;
  const task = { id: tasks.length + 1, title, description, status: 'pending' };
  tasks.push(task);
  res.status(201).json(task);
});

3.2 Get All Tasks

app.get('/tasks', (req, res) => {
  res.json(tasks);
});

3.3 Update Task Status

app.put('/tasks/:id', (req, res) => {
  const task = tasks.find(t => t.id == req.params.id);
  if (!task) return res.status(404).json({ error: 'Task not found' });
  task.status = req.body.status;
  res.json(task);
});

3.4 Delete Task

app.delete('/tasks/:id', (req, res) => {
  tasks = tasks.filter(t => t.id != req.params.id);
  res.json({ message: 'Task deleted successfully' });
});




Step 4: Test with Postman
	1.	Open Postman → New request
	2.	Test endpoints:
	•	POST /tasks → Create a task
	•	GET /tasks → Retrieve tasks
	•	PUT /tasks/:id → Update task
	•	DELETE /tasks/:id → Delete task
	3.	Check responses for correctness


Notes
	•	This tutorial demonstrates basic REST API principles.
	•	In real applications, use a database (e.g., MongoDB) instead of in-memory storage.
	•	Add authentication and error handling for production-ready APIs.
	•	Properly format JSON responses and include status codes.



