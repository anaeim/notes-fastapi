# FastAPI — Path Parameters

## What Are Path Parameters?

Path parameters are values embedded directly in the URL used to identify a specific resource — similar to navigating a file system by path.

```
/users/documents/fastapi/section1   →   "section1" is the path parameter
```

---

## Static vs Dynamic Paths

| Type    | Example URL              | FastAPI Route              | Description                          |
|---------|--------------------------|----------------------------|--------------------------------------|
| Static  | `/books`                 | `@app.get("/books")`       | Fixed path, always returns all books |
| Dynamic | `/books/Title One`       | `@app.get("/books/{book_title}")` | Variable segment captured at runtime: variable that you can pass to the function |

---

## Defining a Path Parameter

The placeholder in the route `{param_name}` **must match** the function parameter name exactly.

```python
@app.get("/books/{book_title}")
async def read_book(book_title: str):
    for book in BOOKS:
        if book.get('title').casefold() == book_title.casefold():
            return book
```

- `casefold()` is a stronger version of `lower()` — ensures case-insensitive matching.
- URLs cannot contain spaces — encode them as `%20`.

```
GET /books/Title%20One   →   returns the book with title "Title One"
```

---

## Order Matters — How FastAPI Matches Incoming Requests

When a request arrives, FastAPI scans all registered routes (pathes) **from top to bottom** in the order they are defined in your file. It stops at the **first route whose pattern matches** the incoming URL and calls that function — it never checks the rest.

This means a dynamic route like `{book_title}` will match **any** string in that position, including values you intended for a specific static route defined below it.

**Wrong order — static route never reached:**
```python
@app.get("/books/{book_title}")   # matches /books/mybook → static route below is unreachable
async def read_book(book_title: str): ...

@app.get("/books/mybook")         # never called — already consumed above
async def read_my_book(): ...
```

**Correct order — static route first:**
```python
@app.get("/books/mybook")         # checked first; matches only the exact string "mybook"
async def read_my_book(): ...

@app.get("/books/{book_title}")   # fallback — matches anything that didn't match above
async def read_book(book_title: str): ...
```

**How the matching works step by step:**

| Incoming URL      | Checked first         | Match? | Result                          |
|-------------------|-----------------------|--------|---------------------------------|
| `/books/mybook`   | `/books/mybook`       | Yes    | `read_my_book()` is called      |
| `/books/Title One`| `/books/mybook`       | No     | moves to next route             |
|                   | `/books/{book_title}` | Yes    | `read_book("Title One")` called |

> **Rule:** Always place specific/static routes **above** dynamic ones.
