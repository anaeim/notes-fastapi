# FastAPI — GET Request Method

## Running the Server

```bash
uvicorn books:app --reload
```

**Uvicorn** is an ASGI web server that serves the FastAPI application. FastAPI itself is just a framework — it needs a server like Uvicorn to handle incoming HTTP connections and pass them to your app.

| Part       | Meaning                                      |
|------------|----------------------------------------------|
| `uvicorn`  | The web server that runs the FastAPI app     |
| `books`    | The Python file (`books.py`): python file that has fastapi instance                 |
| `app`      | The `FastAPI()` instance inside that file: name of fastapi instance inside books.py    |
| `--reload` | Auto-restart the server on every code change |

Server runs at: `http://127.0.0.1:8000`

URL to run read_all_books function: `http://127.0.0.1:8000/books`

NOTE: to run fastapi app, in addition to `uvicorn books:app --reload`, you can also use `fastapi run books.py` for prod env and `fastapi dev books.py` for dev env.

### Shutting Down

Press `Ctrl + C` in the terminal where the server is running.

---

## Project Setup

**File:** `books.py`

```python
from fastapi import FastAPI

app = FastAPI()

BOOKS = [
    {'title': 'Title One',   'author': 'Author One',   'category': 'science'},
    {'title': 'Title Two',   'author': 'Author Two',   'category': 'science'},
    {'title': 'Title Three', 'author': 'Author Three', 'category': 'history'},
    {'title': 'Title Four',  'author': 'Author Four',  'category': 'math'},
    {'title': 'Title Five',  'author': 'Author Five',  'category': 'math'},
    {'title': 'Title Six',   'author': 'Author Two',   'category': 'math'},
]

@app.get("/books")
async def read_all_books():
    return BOOKS
```

---



## Swagger UI (`/docs`)

FastAPI automatically generates interactive API documentation — no extra setup needed.

| URL | Purpose |
|-----|---------|
| `http://127.0.0.1:8000/docs` | Swagger UI — interactive docs |
| `http://127.0.0.1:8000/redoc` | ReDoc — alternative read-only docs |

**Swagger UI** lets you:
- See all available endpoints and their HTTP methods
- Expand each endpoint to view expected inputs and outputs
- Execute requests directly from the browser and inspect live responses

It is powered by the **OpenAPI** standard — FastAPI builds the spec automatically from your route decorators and type hints.

> Useful for testing endpoints during development without needing tools like Postman or curl.

---

## Key Concepts

| Concept         | Detail                                                                 |
|-----------------|------------------------------------------------------------------------|
| `@app.get(<path>)` | Decorator that registers a function as a GET endpoint                  |
| Path / Route    | GET endpoint (path) that we're adding: path or URL to call this Python function. (e.g. `/books`)          |
| `async def`     | Optional but explicit — FastAPI handles async internally if omitted    |
| Swagger UI      | Auto-generated docs available at `http://127.0.0.1:8000/docs`         |

---

## Endpoint

| Method | Path     | Function          | Returns        |
|--------|----------|-------------------|----------------|
| GET    | `/books` | `read_all_books`  | All books list |
