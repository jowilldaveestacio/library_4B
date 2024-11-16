## API Documentation 

#### The Library API is designed for users to view and library administrators to manage books and authors. It provides endpoints for registering and authenticating users, as well as viewing, adding and modifying book information.

## ENDPOINTS
### 1. Register a New User
- **Method:** `POST`
- **Endpoint:** `/user/register`
- **Description:** Registers a new user by checking if the username is available and, if so, adds the user to the database.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:**
  - `username` (string): Desired username for the new account.
  - `password` (string): Password for the new account.
- **Responses:**
  - **Success:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "success", "data": null }`
  - **Failure: Username Taken:** 
    - **Status:** `200 OK`
    - **Body:** `{ "status": "fail", "data": { "title": "Username already taken" } }`
  - **Failure: Database Error:** 
    - **Status:** `500 Internal Server Error`
    - **Body:** `{ "status": "fail", "data": { "title": "<error message>" } }`
