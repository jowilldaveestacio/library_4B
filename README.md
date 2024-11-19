# 📚 Library API Documentation

Welcome to the **Library API** documentation. This API enables users to view books and authors while empowering library administrators with tools to manage them. Features include user registration, authentication, and robust book and author management capabilities.

---

## 🗂️ Endpoints Overview

### **1️⃣ Register a New User**
- **Method:** `POST`
- **Endpoint:** `/user/register`
- **Description:** Register a new user and save them to the database if the username is available.
- **Request Headers:**
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `username` *(string)*: Desired username.
  - `password` *(string)*: Account password.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": null }`
  - 🚫 **200 OK (Username Taken):** `{ "status": "fail", "data": { "title": "Username already taken" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **2️⃣ Authenticate User**
- **Method:** `POST`
- **Endpoint:** `/user/auth`
- **Description:** Authenticate user credentials and receive an access token upon success.
- **Request Headers:**
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `username` *(string)*: Username of the user.
  - `password` *(string)*: Password of the user.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "token": "<token>", "data": null }`
  - 🚫 **200 OK (Authentication Failed):** `{ "status": "fail", "data": { "title": "Authentication Failed" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **3️⃣ Show Users**
- **Method:** `GET`
- **Endpoint:** `/user/show`
- **Description:** Retrieve a list of all registered users. Requires authorization.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": [{ "user_id": "<user_id>", "username": "<username>" }, ... ] }`
  - 🚫 **401 Unauthorized (Missing Authorization):** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **4️⃣ Update User**
- **Method:** `PUT`
- **Endpoint:** `/user/update`
- **Description:** Update user information. Requires authorization.
- **Request Headers:**
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `token` *(string)*: Authorization token.
  - `user_id` *(integer)*: ID of the user.
  - `username` *(string)*: New username.
  - `password` *(string)*: New password.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - 🚫 **401 Unauthorized (Missing Token):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - 🚫 **400 Bad Request (Missing User ID):** `{ "status": "fail", "data": { "title": "User ID missing in payload" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - 🚫 **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **5️⃣ Delete User**
- **Method:** `DELETE`
- **Endpoint:** `/user/delete`
- **Description:** Delete a user account. Requires authorization.
- **Request Headers:**
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `token` *(string)*: Authorization token.
  - `user_id` *(integer)*: ID of the user.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": null }`
  - 🚫 **400 Bad Request (Invalid JSON Payload):** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
  - 🚫 **401 Unauthorized (Missing Token):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - 🚫 **400 Bad Request (Missing User ID):** `{ "status": "fail", "data": { "title": "User ID missing in payload" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - 🚫 **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---


