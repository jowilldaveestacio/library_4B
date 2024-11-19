# 📚 Library API Documentation

The **Library API** provides a powerful interface for managing users, books, and authors in a library system. It supports operations for user authentication, book and author management, and administrative controls.

---

## 🚀 Features
- User registration and authentication.
- Management of books and authors.
- Secure endpoints with token-based authentication.

---

## 🛠️ Endpoints Overview

### **1. User Management**
#### Register a New User
- **Method:** `POST`
- **Endpoint:** `/user/register`
- **Description:** Register a new user if the username is available.
- **Request:**
  ```json
  {
    "username": "your_username",
    "password": "your_password"
  }
