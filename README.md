# Task Manager Authentication Authorization

A backend-only **Node.js + Express.js Task Manager API** project with CRUD operations, JWT-based authentication, role-based authorization, and bcrypt password hashing.

This project is designed for testing with **Postman**. No frontend/webpage is required.

---

## Project Features

- User signup
- User login
- JWT access token generation
- Password hashing using bcrypt
- Role-based authorization
- Admin can create, view, update, and delete tasks
- User can only view their own assigned tasks
- Admin can view which user has which task
- Data stored in JSON files

---

## Technologies Used

- Node.js
- Express.js
- JSON Web Token (JWT)
- bcryptjs
- Postman
- JSON file storage

---

## Project Structure

```txt
task-manager-authentication-authorization
│
├── server.js
├── users.json
├── tasks.json
├── package.json
├── package-lock.json
└── README.md
```

---

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/your-username/task-manager-authentication-authorization.git
```

### 2. Go to the project folder

```bash
cd task-manager-authentication-authorization
```

### 3. Install dependencies

```bash
npm install
```

### 4. Run the server

```bash
node server.js
```

Server will run on:

```txt
http://localhost:5000
```

---

## Required JSON Files

Create a `users.json` file:

```json
[]
```

Create a `tasks.json` file:

```json
[]
```

---

## API Endpoints

| Feature | Method | Endpoint | Access |
|---|---|---|---|
| Signup | POST | `/signup` | Public |
| Login | POST | `/login` | Public |
| Create Task | POST | `/tasks` | Admin only |
| View Tasks | GET | `/tasks` | Admin/User |
| View Task by ID | GET | `/tasks/:id` | Admin/Assigned User |
| Update Task | PUT | `/tasks/:id` | Admin only |
| Delete Task | DELETE | `/tasks/:id` | Admin only |
| View Users with Tasks | GET | `/admin/users-tasks` | Admin only |

---

## Authentication and Authorization Logic

### Authentication

Authentication means verifying who the user is.

In this project, authentication is handled by:

- Signup
- Login
- JWT token generation
- JWT token verification

When a user logs in successfully, a JWT access token is generated. This token is required to access protected routes.

### Authorization

Authorization means controlling what a user is allowed to do.

In this project:

- Admin can create, view, update, and delete tasks.
- Admin can view all users and their assigned tasks.
- User can only view their own assigned tasks.
- User cannot create, update, or delete tasks.

---

## Password Security

Passwords are not stored directly.

During signup, the password is hashed using `bcryptjs` before saving it in `users.json`.

Example:

```txt
Original password: 12345
Stored password: hashed password
```

This improves password security.

---

## Postman Testing Guide

### 1. Signup Admin

**Method:** POST

**URL:**

```txt
http://localhost:5000/signup
```

**Body → raw → JSON**

```json
{
  "name": "Admin",
  "email": "admin@gmail.com",
  "password": "12345",
  "role": "admin"
}
```

---

### 2. Signup User

**Method:** POST

**URL:**

```txt
http://localhost:5000/signup
```

**Body → raw → JSON**

```json
{
  "name": "User One",
  "email": "user1@gmail.com",
  "password": "user123",
  "role": "user"
}
```

---

### 3. Login Admin

**Method:** POST

**URL:**

```txt
http://localhost:5000/login
```

**Body → raw → JSON**

```json
{
  "email": "admin@gmail.com",
  "password": "12345"
}
```

After successful login, copy the JWT token from the response.

---

### 4. Create Task as Admin

**Method:** POST

**URL:**

```txt
http://localhost:5000/tasks
```

**Authorization:**

```txt
Type: Bearer Token
Token: Admin token
```

**Body → raw → JSON**

```json
{
  "title": "Design login page",
  "description": "Create login page UI design",
  "assignedTo": 2
}
```

---

### 5. Admin View All Tasks

**Method:** GET

**URL:**

```txt
http://localhost:5000/tasks
```

**Authorization:**

```txt
Type: Bearer Token
Token: Admin token
```

Admin can see all tasks.

---

### 6. User Login

**Method:** POST

**URL:**

```txt
http://localhost:5000/login
```

**Body → raw → JSON**

```json
{
  "email": "user1@gmail.com",
  "password": "user123"
}
```

After successful login, copy the user token.

---

### 7. User View Own Tasks

**Method:** GET

**URL:**

```txt
http://localhost:5000/tasks
```

**Authorization:**

```txt
Type: Bearer Token
Token: User token
```

User can see only their own assigned tasks.

---

### 8. Admin Update Task

**Method:** PUT

**URL:**

```txt
http://localhost:5000/tasks/1
```

**Authorization:**

```txt
Type: Bearer Token
Token: Admin token
```

**Body → raw → JSON**

```json
{
  "title": "Design login page",
  "description": "Create login page UI design",
  "assignedTo": 2,
  "status": "completed"
}
```

---

### 9. Admin Delete Task

**Method:** DELETE

**URL:**

```txt
http://localhost:5000/tasks/1
```

**Authorization:**

```txt
Type: Bearer Token
Token: Admin token
```

No body is required.

---

### 10. Admin View Users with Assigned Tasks

**Method:** GET

**URL:**

```txt
http://localhost:5000/admin/users-tasks
```

**Authorization:**

```txt
Type: Bearer Token
Token: Admin token
```

This route shows each user with their assigned tasks.

---

## Example Role Permission

| Action | Admin | User |
|---|---|---|
| Signup | Yes | Yes |
| Login | Yes | Yes |
| Create task | Yes | No |
| View all tasks | Yes | No |
| View own tasks | Yes | Yes |
| Update task | Yes | No |
| Delete task | Yes | No |
| View users with tasks | Yes | No |

---

## Short Project Summary

This project is a backend-only Task Manager API using Node.js and Express.js. It includes authentication using JWT, password security using bcrypt, and role-based authorization for admin and user roles. Admin can manage all tasks, while users can only view their own assigned tasks. The API is tested using Postman.

---

## Author

Created by: Mahjabin
