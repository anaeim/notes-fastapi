# FastAPI Basics — Books Project Overview

## What We're Building

A simple **Books API** that demonstrates CRUD operations using FastAPI. The dataset is a list of books, each with three fields:

| Field    | Example Values                        |
|----------|---------------------------------------|
| title    | Title 1, Title 2, ... Title 5         |
| author   | Author 1, Author 2, ... Author 5      |
| category | Science, History, Math                |

---

## CRUD Operations

| CRUD Operation | HTTP Method | Description                    |
|-----------|-------------|--------------------------------|
| Create    | `POST`      | Add a new book to the list     |
| Read      | `GET`       | Retrieve one or more books     |
| Update    | `PUT`       | Modify an existing book        |
| Delete    | `DELETE`    | Remove a book from the list    |

---

## Request / Response Flow

```
Web Page  →  HTTP Request  →  FastAPI Server
Web Page  ←  HTTP Response ←  FastAPI Server
```

- The client sends an HTTP request specifying **what it wants** (e.g. "give me books 2 and 4").
- FastAPI processes the request and returns the matching data.

---

## Swagger UI

FastAPI ships with **Swagger UI** built in — no extra setup needed.

- **URL:** `http://localhost:8000/docs`
- Lists all available endpoints and lets you test them interactively.

---

## Key Takeaway

The first endpoint we build is a `GET` request — the foundation for reading and returning data to the client.
