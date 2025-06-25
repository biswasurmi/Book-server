# Book Management REST API (Go + Chi + JWT + Basic Auth)

A simple REST API for managing books with basic CRUD operations, written in Go using the Chi router.  
Supports Basic Authentication and JWT-based authorization. Data is stored in-memory (not persistent).

---

## Features

- Create, read, update, and delete books
- Basic authentication for token retrieval and listing
- JWT authentication for modifying books
- In-memory storage for simplicity

---

## Book Model

```json
{
  "uuid": "auto-generated string",
  "name": "string",
  "authorList": ["string"],
  "publishDate": "YYYY-MM-DD",
  "isbn": "string"
}
Getting Started
Prerequisites
Go 1.22 or higher

Git (optional, for cloning repo)

Run Server
bash
Copy
Edit
go run main.go
Command line flags:

-auth (default true): Enable or disable authentication

-port (default 8080): Specify port number

Example disabling auth:

bash
Copy
Edit
go run main.go -auth=false
API Endpoints
Method	Endpoint	Description	Auth Required
GET	/api/v1/get-token	Get JWT token (Basic Auth)	Basic Auth
GET	/api/v1/books	List all books	Basic Auth or JWT
POST	/api/v1/books	Create a new book	JWT
GET	/api/v1/books/{id}	Get book by UUID	JWT
PUT	/api/v1/books/{id}	Update book by UUID	JWT
DELETE	/api/v1/books/{id}	Delete book by UUID	JWT

Usage Examples
Get JWT Token (Basic Auth)
bash
Copy
Edit
curl -u AdminUser:AdminPassword http://localhost:8080/api/v1/get-token
Response:

json
Copy
Edit
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
List All Books (Basic Auth or JWT)
bash
Copy
Edit
curl -u AdminUser:AdminPassword http://localhost:8080/api/v1/books
or with JWT token:

bash
Copy
Edit
curl -H "Authorization: Bearer <TOKEN>" http://localhost:8080/api/v1/books
Create a Book (JWT Required)
bash
Copy
Edit
curl -X POST http://localhost:8080/api/v1/books \
  -H "Authorization: Bearer <TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Go Programming",
    "authorList": ["Alan A. A."],
    "publishDate": "2023-01-01",
    "isbn": "123-4567890123"
  }'
Response:

json
Copy
Edit
{
  "uuid": "generated-uuid",
  "name": "Go Programming",
  "authorList": ["Alan A. A."],
  "publishDate": "2023-01-01",
  "isbn": "123-4567890123"
}
Get Book by UUID (JWT Required)
bash
Copy
Edit
curl -H "Authorization: Bearer <TOKEN>" http://localhost:8080/api/v1/books/<uuid>
Update Book (JWT Required)
bash
Copy
Edit
curl -X PUT http://localhost:8080/api/v1/books/<uuid> \
  -H "Authorization: Bearer <TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Updated Book",
    "authorList": ["New Author"],
    "publishDate": "2025-06-01",
    "isbn": "999-9999999999"
  }'
Delete Book (JWT Required)
bash
Copy
Edit
curl -X DELETE http://localhost:8080/api/v1/books/<uuid> \
  -H "Authorization: Bearer <TOKEN>"
Notes
Data is stored in memory and will be lost on server restart.

JWT secret key is hardcoded for simplicity — consider environment variables for production.

The server logs all requests with Chi's logger middleware.
```