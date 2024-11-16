# Library API Documentation

The Library API enables users to view books and authors, while providing library administrators with the tools to manage them. The API includes endpoints for user registration, authentication, and book management.

## Endpoints Overview

### 1. Register a New User
- **Method:** `POST`
- **Endpoint:** `/user/register`
- **Description:** Registers a new user and adds them to the database if the username is available.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `username` (string): Desired username.
  - `password` (string): Account password.
- **Responses:**
  - **200 OK:** `{ "status": "success", "data": null }`
  - **200 OK (Username Taken):** `{ "status": "fail", "data": { "title": "Username already taken" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 2. Authenticate User
- **Method:** `POST`
- **Endpoint:** `/user/auth`
- **Description:** Verifies user credentials and returns an access token on success.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `username` (string): User's username.
  - `password` (string): User's password.
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<token>", "data": null }`
  - **200 OK (Authentication Failed):** `{ "status": "fail", "data": { "title": "Authentication Failed" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 3. Show Users
- **Method:** `GET`
- **Endpoint:** `/user/show`
- **Description:** Lists all registered users. Authorization token required.
- **Request Headers:**
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": [ { "user_id": "<user_id>", "username": "<username>" }, ... ] }`
  - **401 Unauthorized (Missing Authorization):** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 4. Update User
- **Method:** `PUT`
- **Endpoint:** `/user/update`
- **Description:** Updates a user's information. Authorization token required.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token.
  - `user_id` (integer): ID of the user.
  - `username` (string): New username.
  - `password` (string): New password.
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **401 Unauthorized (Missing Token):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Missing User ID):** `{ "status": "fail", "data": { "title": "User ID missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 5. Delete User
- **Method:** `DELETE`
- **Endpoint:** `/user/delete`
- **Description:** Deletes a user account. Authorization token required.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token.
  - `user_id` (integer): ID of the user.
- **Responses:**
  - **200 OK:** `{ "status": "success", "data": null }`
  - **400 Bad Request (Invalid JSON Payload):** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
  - **401 Unauthorized (Missing Token):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Missing User ID):** `{ "status": "fail", "data": { "title": "User ID missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **403 Forbidden:** `{ "status": "fail", "data": { "title": "Unauthorized action" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 6. Register a New Author
- **Method:** `POST`
- **Endpoint:** `/author/register`
- **Description:** Adds a new author to the database if the name is unique. Authorization token required.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token.
  - `name` (string): Author's name.
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **401 Unauthorized (Missing Token):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Missing Author Name):** `{ "status": "fail", "data": { "title": "Name missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **200 OK (Author Name Taken):** `{ "status": "fail", "data": { "title": "Author name already taken" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 7. Show All Authors
- **Method:** `GET`
- **Endpoint:** `/author/show`
- **Description:** Retrieves a list of all authors. Authorization token required.
- **Request Headers:**
  - `Authorization: Bearer <token>`
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": [ { "author_id": "<id>", "name": "<name>" }, ... ] }`
  - **401 Unauthorized (Missing Authorization):** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **200 OK (No Authors Found):** `{ "status": "fail", "message": "No authors found" }`
  - **500 Internal Server Error:** `{ "status": "fail", "message": "<error message>" }`

### 8. Update Author
- **Method:** `PUT`
- **Endpoint:** `/author/update`
- **Description:** Updates an author's information. Authorization token required.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token.
  - `author_id` (integer): ID of the author.
  - `name` (string): New name of the author.
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **401 Unauthorized (Missing Token):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Missing Author ID):** `{ "status": "fail", "data": { "title": "Author ID missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 9. Delete Author
- **Method:** `DELETE`
- **Endpoint:** `/author/delete`
- **Description:** Deletes an author by ID. Authorization token required.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token.

### 10. Register Book
- **Method:** `POST`
- **Endpoint:** `/book/register`
- **Description:** Allows users to register a new book in the database by providing a title and linking it to an existing author. A valid authorization token is required for this action.
- **Request Headers:**
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `token` (string): Authorization token for the user.
  - `title` (string): Title of the book.
  - `author_id` (integer): ID of the author to whom the book is linked.
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **401 Unauthorized (Token Missing):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Title or Author ID Missing):** `{ "status": "fail", "data": { "title": "Title or Author ID missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **400 Bad Request (Book Already Exists):** `{ "status": "fail", "data": { "title": "Book already exists" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 11. Show Books
- **Method:** `GET`
- **Endpoint:** `/book/show`
- **Description:** Fetches and returns a list of all books in the database. A valid authorization token is required to access the list.
- **Request Headers:**
  - `Authorization: Bearer <token>`
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": [{ "book_id": 1, "title": "Book Title", "author_id": 2 }, ...] }`
  - **401 Unauthorized (Authorization Header Missing):** `{ "status": "fail", "data": { "title": "Authorization header missing" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **404 Not Found (No Books Found):** `{ "status": "fail", "message": "No books found" }`
  - **500 Internal Server Error:** `{ "status": "fail", "message": "<error message>" }`

### 12. Update Book
- **Method:** `PUT`
- **Endpoint:** `/book/update`
- **Description:** Updates the details of an existing book, including its title and associated author. A valid authorization token is required along with the book ID in the request body.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `book_id`: The ID of the book to update (required)
    - `title`: The new title for the book (required)
    - `author_id`: The new author ID for the book (required)
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **401 Unauthorized (Token Missing):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Book ID Missing):** `{ "status": "fail", "data": { "title": "Book ID missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

### 13. Delete Book
- **Method:** `DELETE`
- **Endpoint:** `/book/delete`
- **Description:** Deletes a specific book by its ID. This operation requires a valid authorization token and the book's ID to be provided in the payload.
- **Request Payload:**
  - JSON body containing:
    - `token`: The authorization token (required)
    - `book_id`: The ID of the book to delete (required)
- **Responses:**
  - **200 OK:** `{ "status": "success", "token": "<new_token>", "data": null }`
  - **400 Bad Request (Invalid JSON Payload):** `{ "status": "fail", "data": { "title": "Invalid JSON payload" } }`
  - **401 Unauthorized (Token Missing):** `{ "status": "fail", "data": { "title": "Token missing in payload" } }`
  - **400 Bad Request (Book ID Missing):** `{ "status": "fail", "data": { "title": "Book ID missing in payload" } }`
  - **401 Unauthorized (Invalid/Expired Token):** `{ "status": "fail", "data": { "title": "Invalid or expired token" } }`
  - **500 Internal Server Error:** `{ "status": "fail", "data": { "title": "<error message>" } }`

**Developed by:**
  
**JOWILL DAVE B. ESTACIO -4B**
