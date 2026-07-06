# 📚 Python Built-in Library: `json`

The `json` module allows you to **convert Python objects to JSON** and **JSON data back into Python objects**. It is commonly used when working with APIs, configuration files, and data storage.

> **Note:** The `json` module is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import json
```

---

# 1️⃣ `json.dumps()`

Converts a Python object into a JSON string.

```python
import json

student = {
    "name": "Alice",
    "age": 22,
    "department": "CSE"
}

json_data = json.dumps(student)

print(json_data)
```

### Output

```json
{"name": "Alice", "age": 22, "department": "CSE"}
```

---

# 2️⃣ `json.loads()`

Converts a JSON string into a Python object.

```python
import json

data = '{"name":"Alice","age":22}'

student = json.loads(data)

print(student)
print(type(student))
```

### Output

```
{'name': 'Alice', 'age': 22}
<class 'dict'>
```

---

# 3️⃣ `json.dump()`

Writes a Python object to a JSON file.

```python
import json

student = {
    "name": "Alice",
    "age": 22,
    "department": "CSE"
}

with open("student.json", "w") as file:
    json.dump(student, file)
```

---

# 4️⃣ `json.load()`

Reads JSON data from a file.

```python
import json

with open("student.json", "r") as file:
    data = json.load(file)

print(data)
```

### Output

```
{'name': 'Alice', 'age': 22, 'department': 'CSE'}
```

---

# 5️⃣ Pretty Print JSON (`indent`)

Makes JSON more readable.

```python
import json

student = {
    "name": "Alice",
    "age": 22,
    "department": "CSE"
}

print(json.dumps(student, indent=4))
```

### Output

```json
{
    "name": "Alice",
    "age": 22,
    "department": "CSE"
}
```

---

# 6️⃣ Sort JSON Keys

Sorts keys alphabetically.

```python
import json

student = {
    "department": "CSE",
    "age": 22,
    "name": "Alice"
}

print(json.dumps(student, indent=4, sort_keys=True))
```

### Output

```json
{
    "age": 22,
    "department": "CSE",
    "name": "Alice"
}
```

---

# 7️⃣ Convert a List to JSON

```python
import json

languages = ["Python", "Java", "C++"]

print(json.dumps(languages))
```

### Output

```json
["Python", "Java", "C++"]
```

---

# 8️⃣ Convert JSON Array to Python List

```python
import json

data = '["Python", "Java", "C++"]'

languages = json.loads(data)

print(languages)
print(type(languages))
```

### Output

```
['Python', 'Java', 'C++']
<class 'list'>
```

---

# 9️⃣ Access JSON Data

```python
import json

data = '{"name":"Alice","age":22}'

student = json.loads(data)

print(student["name"])
```

### Output

```
Alice
```

---

# 🔟 Write JSON with Indentation

```python
import json

student = {
    "name": "Alice",
    "age": 22
}

with open("student.json", "w") as file:
    json.dump(student, file, indent=4)
```

Generated `student.json`

```json
{
    "name": "Alice",
    "age": 22
}
```

---

# 1️⃣1️⃣ Convert Python Types to JSON

```python
import json

data = {
    "name": "Alice",
    "age": 22,
    "active": True,
    "skills": ["Python", "SQL"],
    "cgpa": 3.85
}

print(json.dumps(data, indent=4))
```

---

# 1️⃣2️⃣ Python ↔ JSON Data Types

| Python | JSON |
|---------|------|
| `dict` | Object |
| `list` | Array |
| `tuple` | Array |
| `str` | String |
| `int` | Number |
| `float` | Number |
| `True` | `true` |
| `False` | `false` |
| `None` | `null` |

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `dumps()` | Python object → JSON string |
| `loads()` | JSON string → Python object |
| `dump()` | Python object → JSON file |
| `load()` | JSON file → Python object |

---

# 💡 Common Uses

- 🌐 REST APIs
- 🤖 Automation
- ⚙️ Configuration files
- 💾 Data storage
- 📊 Data exchange
- 🔐 Cybersecurity tools
- ☁️ Web development

---

## 🚀 Quick Example

```python
import json

user = {
    "username": "admin",
    "role": "administrator",
    "active": True
}

json_data = json.dumps(user, indent=4)

print(json_data)
```

### Output

```json
{
    "username": "admin",
    "role": "administrator",
    "active": true
}
```

---

## ✅ Key Takeaways

- No installation required.
- `dumps()` converts a Python object into a JSON string.
- `loads()` converts a JSON string into a Python object.
- `dump()` writes JSON to a file.
- `load()` reads JSON from a file.
- Use `indent=4` to create readable JSON.
- JSON is the most common data format used in APIs and modern web applications.

---

⭐ **The `json` module is one of Python's most important libraries for web development, automation, data exchange, and cybersecurity. Nearly every REST API uses JSON for sending and receiving data.**
