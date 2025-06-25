---

```markdown
# 📚 Book Management REST API (Go + Chi + Docker)

A fully working Book Management REST API written in **Go**, using the **Chi router**, with support for **JWT** and **Basic Authentication**, containerized using **Docker**.

---

## 🚀 Features

- RESTful API (CRUD for books)
- JWT authentication for protected routes
- Basic Auth for token retrieval and listing books
- Dockerized for easy deployment
- Lightweight and simple

---

## 📂 Directory Structure

```

project/
├── main.go
├── go.mod
├── go.sum
└── Dockerfile

````

---

## 🐳 Docker Workflow

### ✅ Step 1: Navigate to your project folder

```bash
cd ~/Desktop/Go/chi/project
````

---

### ✅ Step 2: Build your Docker image (image name must be lowercase)

```bash
docker build -t mychi .
```

---

### ✅ Step 3: Make sure port `8080` is free

Check what containers are using it:

```bash
docker container ls
```

Stop conflicting ones:

```bash
docker container stop <container-id>
```

---

### ✅ Step 4: Run the container locally

```bash
docker run -d -p 8080:8080 mychi
```

Now the server is running at: [http://localhost:8080](http://localhost:8080)

---

### ✅ Step 5: Tag and push the image to Docker Hub

Make sure you're logged in:

```bash
docker login
```

Then tag and push:

```bash
docker tag mychi urmibiswas/mychi:latest
docker push urmibiswas/mychi:latest
```

---

## 🌍 How to Pull and Run Anywhere

On any machine with Docker installed:

```bash
docker pull urmibiswas/mychi:latest
docker run -d -p 8080:8080 urmibiswas/mychi:latest
```

---

## 🔐 Authentication

| Endpoint               | Method | Auth Type  | Description         |
| ---------------------- | ------ | ---------- | ------------------- |
| `/api/v1/get-token`    | GET    | Basic Auth | Get a JWT token     |
| `/api/v1/books`        | GET    | Basic Auth | List all books      |
| `/api/v1/books`        | POST   | JWT        | Create a new book   |
| `/api/v1/books/{uuid}` | GET    | JWT        | Get book by UUID    |
| `/api/v1/books/{uuid}` | PUT    | JWT        | Update book by UUID |
| `/api/v1/books/{uuid}` | DELETE | JWT        | Delete book by UUID |

---

## 🧪 API Examples with `curl`

### 🔑 Get JWT Token

```bash
curl -u AdminUser:AdminPassword http://localhost:8080/api/v1/get-token
```

---

### 📚 List All Books

```bash
curl -u AdminUser:AdminPassword http://localhost:8080/api/v1/books
```

---

### ➕ Create a Book

```bash
curl -X POST http://localhost:8080/api/v1/books \
  -H "Authorization: Bearer <JWT_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Docker in Go",
    "authorList": ["Urmi"],
    "publishDate": "2025-06-18",
    "isbn": "123-4567890000"
  }'
```

---

### 🔍 Get Book by UUID

```bash
curl http://localhost:8080/api/v1/books/<uuid> \
  -H "Authorization: Bearer <JWT_TOKEN>"
```

---

### ♻️ Update Book

```bash
curl -X PUT http://localhost:8080/api/v1/books/<uuid> \
  -H "Authorization: Bearer <JWT_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Updated Book",
    "authorList": ["Urmi", "Someone Else"],
    "publishDate": "2025-06-19",
    "isbn": "999-9999999999"
  }'
```

---

### ❌ Delete Book

```bash
curl -X DELETE http://localhost:8080/api/v1/books/<uuid> \
  -H "Authorization: Bearer <JWT_TOKEN>"
```

---

## 📘 Book Object Schema

```json
{
  "uuid": "generated-uuid",
  "name": "string",
  "authorList": ["string"],
  "publishDate": "YYYY-MM-DD",
  "isbn": "string"
}
```






  git add README.md
  git commit -m "Add complete Docker + API usage guide"
  git push origin main
````
