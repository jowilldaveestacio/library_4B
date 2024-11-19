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

### **6️⃣ Add a New Book**
- **Method:** `POST`
- **Endpoint:** `/books/add`
- **Description:** Add a new book to the library. Requires admin authorization.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `title` *(string)*: Title of the book.
  - `author_id` *(integer)*: ID of the author.
  - `isbn` *(string)*: ISBN number of the book.
  - `published_date` *(string, YYYY-MM-DD)*: Published date of the book.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": null }`
  - 🚫 **400 Bad Request (Invalid Data):** `{ "status": "fail", "data": { "title": "Invalid data" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - 🚫 **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **7️⃣ Get All Books**
- **Method:** `GET`
- **Endpoint:** `/books`
- **Description:** Retrieve a list of all books in the library.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Responses:**
  - ✅ **200 OK:** 
    ```json
    { 
      "status": "success", 
      "data": [
        { "book_id": "<book_id>", "title": "<title>", "author": "<author>", "isbn": "<isbn>", "published_date": "<published_date>" }, 
        ... 
      ] 
    }
    ```
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **8️⃣ Get Book by ID**
- **Method:** `GET`
- **Endpoint:** `/books/<book_id>`
- **Description:** Retrieve a book by its unique ID.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Responses:**
  - ✅ **200 OK:** 
    ```json
    { 
      "status": "success", 
      "data": { 
        "book_id": "<book_id>", 
        "title": "<title>", 
        "author": "<author>", 
        "isbn": "<isbn>", 
        "published_date": "<published_date>" 
      }
    }
    ```
  - 🚫 **404 Not Found (Book Not Found):** `{ "status": "fail", "data": { "title": "Book not found" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **9️⃣ Update a Book**
- **Method:** `PUT`
- **Endpoint:** `/books/update/<book_id>`
- **Description:** Update details of an existing book. Requires admin authorization.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `title` *(string)*: New title of the book.
  - `author_id` *(integer)*: New author ID.
  - `isbn` *(string)*: New ISBN number.
  - `published_date` *(string, YYYY-MM-DD)*: New published date.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": null }`
  - 🚫 **400 Bad Request (Invalid Data):** `{ "status": "fail", "data": { "title": "Invalid data" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - 🚫 **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **🔟 Delete a Book**
- **Method:** `DELETE`
- **Endpoint:** `/books/delete/<book_id>`
- **Description:** Delete a book from the library collection. Requires admin authorization.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": null }`
  - 🚫 **400 Bad Request (Invalid JSON Payload):** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - 🚫 **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **1️⃣1️⃣ Add an Author**
- **Method:** `POST`
- **Endpoint:** `/authors/add`
- **Description:** Add a new author to the library system. Requires admin authorization.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Request Body Parameters:**
  - `name` *(string)*: Name of the author.
  - `biography` *(string)*: Short biography of the author.
  - `birthdate` *(string, YYYY-MM-DD)*: Birthdate of the author.
- **Responses:**
  - ✅ **200 OK:** `{ "status": "success", "data": null }`
  - 🚫 **400 Bad Request (Invalid Data):** `{ "status": "fail", "data": { "title": "Invalid data" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - 🚫 **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **1️⃣2️⃣ Get All Authors**
- **Method:** `GET`
- **Endpoint:** `/authors`
- **Description:** Retrieve a list of all authors in the library.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Responses:**
  - ✅ **200 OK:** 
    ```json
    { 
      "status": "success", 
      "data": [
        { "author_id": "<author_id>", "name": "<name>", "biography": "<biography>", "birthdate": "<birthdate>" }, 
        ... 
      ] 
    }
    ```
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

---

### **1️⃣3️⃣ Get Author by ID**
- **Method:** `GET`
- **Endpoint:** `/authors/<author_id>`
- **Description:** Retrieve details of a specific author by their unique ID.
- **Request Headers:**
  - `Authorization`: `Bearer <token>`
  - `Content-Type`: `application/json`
- **Responses:**
  - ✅ **200 OK:** 
    ```json
    { 
      "status": "success", 
      "data": { 
        "author_id": "<author_id>", 
        "name": "<name>", 
        "biography": "<biography>", 
        "birthdate": "<birthdate>" 
      }
    }
    ```
  - 🚫 **404 Not Found (Author Not Found):** `{ "status": "fail", "data": { "title": "Author not found" } }`
  - 🚫 **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - ⚠️ **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`
 
  ---
  ### **Developed by:**

**JOWILL DAVE B. ESTACIO - 4B**



