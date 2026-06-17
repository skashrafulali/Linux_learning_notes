# HTTP Status Codes Cheat Sheet

HTTP status codes are responses sent by a web server to indicate the result of a client's request.

## Status Code Categories

| Range   | Category                | Description                                                               |
| ------- | ----------------------- | ------------------------------------------------------------------------- |
| 100-199 | Informational Responses | The request has been received and the client should continue the process. |
| 200-299 | Success                 | The request was successfully received, understood, and processed.         |
| 300-399 | Redirection             | Further action is required to complete the request.                       |
| 400-499 | Client Errors           | The request contains bad syntax or cannot be fulfilled.                   |
| 500-599 | Server Errors           | The server failed to fulfill a valid request.                             |

---

# Common HTTP Status Codes

## Success Responses

### 200 OK

The request was completed successfully.

**Example:**

```bash
GET /index.html
```

**Response:**

```http
HTTP/1.1 200 OK
```

---

### 201 Created

A new resource has been successfully created.

**Example:**

```bash
POST /users
```

**Response:**

```http
HTTP/1.1 201 Created
```

---

## Redirection Responses

### 301 Moved Permanently

The requested resource has been permanently moved to a new URL.

**Example:**

```http
HTTP/1.1 301 Moved Permanently
Location: https://newsite.com
```

---

### 302 Found

The resource has been temporarily moved.

**Example:**

```http
HTTP/1.1 302 Found
Location: https://temporary-page.com
```

---

## Client Error Responses

### 400 Bad Request

The server cannot process the request due to invalid syntax or missing parameters.

**Example:**

```http
HTTP/1.1 400 Bad Request
```

---

### 401 Unauthorized

Authentication is required to access the resource.

**Example:**

```http
HTTP/1.1 401 Unauthorized
```

---

### 403 Forbidden

You are authenticated (or not), but you do not have permission to access the resource.

**Example:**

```http
HTTP/1.1 403 Forbidden
```

---

### 404 Not Found

The requested resource does not exist on the server.

**Example:**

```http
HTTP/1.1 404 Not Found
```

---

### 405 Method Not Allowed

The HTTP method used is not supported for the requested resource.

**Example:**

```bash
GET /create-account
```

When the endpoint expects:

```bash
POST /create-account
```

**Response:**

```http
HTTP/1.1 405 Method Not Allowed
```

---

## Server Error Responses

### 500 Internal Server Error

The server encountered an unexpected condition and could not process the request.

**Example:**

```http
HTTP/1.1 500 Internal Server Error
```

---

### 503 Service Unavailable

The server is temporarily unavailable due to maintenance or high traffic.

**Example:**

```http
HTTP/1.1 503 Service Unavailable
```

---

# Quick Memorization Tips

✅ **200** → Everything is OK

✅ **201** → Something new was Created

✅ **301** → Permanent Redirect

✅ **302** → Temporary Redirect

✅ **400** → Bad Request from Client

✅ **401** → Login Required

✅ **403** → Access Forbidden

✅ **404** → Page Not Found

✅ **405** → Wrong HTTP Method

✅ **500** → Server Broke

✅ **503** → Server Busy / Under Maintenance

---

*Part of my Linux & Cybersecurity Learning Journey.*
