# 📚 Python Built-in Library: `pathlib`

The `pathlib` module provides an **object-oriented way** to work with file system paths. It is easier to read, safer, and more modern than using `os.path`.

> **Note:** The `pathlib` module is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
from pathlib import Path
```

---

# 1️⃣ Create a Path Object

Create a path without checking if it exists.

```python
from pathlib import Path

path = Path("Documents")

print(path)
```

### Output

```
Documents
```

---

# 2️⃣ Current Working Directory

Get the current working directory.

```python
from pathlib import Path

print(Path.cwd())
```

### Output

```
C:\Users\Ashraful\Projects
```

---

# 3️⃣ Home Directory

Returns the current user's home directory.

```python
from pathlib import Path

print(Path.home())
```

### Output

```
C:\Users\Ashraful
```

---

# 4️⃣ Check if a File or Folder Exists

```python
from pathlib import Path

file = Path("notes.txt")

print(file.exists())
```

### Output

```
True
```

---

# 5️⃣ Check if it's a File

```python
from pathlib import Path

file = Path("main.py")

print(file.is_file())
```

### Output

```
True
```

---

# 6️⃣ Check if it's a Directory

```python
from pathlib import Path

folder = Path("Projects")

print(folder.is_dir())
```

### Output

```
True
```

---

# 7️⃣ Create a Directory

```python
from pathlib import Path

Path("Python_Project").mkdir()
```

---

# 8️⃣ Create Nested Directories

```python
from pathlib import Path

Path("Projects/Python/Day1").mkdir(parents=True)
```

---

# 9️⃣ Delete a File

```python
from pathlib import Path

Path("notes.txt").unlink()
```

---

# 🔟 Remove an Empty Directory

```python
from pathlib import Path

Path("Python_Project").rmdir()
```

---

# 1️⃣1️⃣ Rename a File

```python
from pathlib import Path

Path("old.txt").rename("new.txt")
```

---

# 1️⃣2️⃣ Get File Name

```python
from pathlib import Path

file = Path("Documents/report.pdf")

print(file.name)
```

### Output

```
report.pdf
```

---

# 1️⃣3️⃣ Get File Extension

```python
from pathlib import Path

file = Path("photo.png")

print(file.suffix)
```

### Output

```
.png
```

---

# 1️⃣4️⃣ Get File Name Without Extension

```python
from pathlib import Path

file = Path("photo.png")

print(file.stem)
```

### Output

```
photo
```

---

# 1️⃣5️⃣ Get Parent Directory

```python
from pathlib import Path

file = Path("Documents/report.pdf")

print(file.parent)
```

### Output

```
Documents
```

---

# 1️⃣6️⃣ Join Paths

Use the `/` operator to join paths.

```python
from pathlib import Path

path = Path("Projects") / "Python" / "main.py"

print(path)
```

### Output

```
Projects/Python/main.py
```

---

# 1️⃣7️⃣ Read a Text File

```python
from pathlib import Path

file = Path("notes.txt")

print(file.read_text())
```

---

# 1️⃣8️⃣ Write to a Text File

```python
from pathlib import Path

file = Path("notes.txt")

file.write_text("Hello, World!")
```

---

# 1️⃣9️⃣ List Files in a Directory

```python
from pathlib import Path

for item in Path(".").iterdir():
    print(item)
```

### Example Output

```
main.py
notes.txt
images
```

---

# 2️⃣0️⃣ Find Files Using `glob()`

Find all Python files.

```python
from pathlib import Path

for file in Path(".").glob("*.py"):
    print(file)
```

### Example Output

```
main.py
calculator.py
test.py
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `Path()` | Create a path object |
| `cwd()` | Current working directory |
| `home()` | Home directory |
| `exists()` | Check if path exists |
| `is_file()` | Check if path is a file |
| `is_dir()` | Check if path is a directory |
| `mkdir()` | Create a directory |
| `unlink()` | Delete a file |
| `rmdir()` | Remove an empty directory |
| `rename()` | Rename a file/folder |
| `name` | File name |
| `suffix` | File extension |
| `stem` | File name without extension |
| `parent` | Parent directory |
| `iterdir()` | List directory contents |
| `glob()` | Find matching files |
| `read_text()` | Read a text file |
| `write_text()` | Write to a text file |

---

# 💡 Why Use `pathlib` Instead of `os.path`?

| `os.path` | `pathlib` |
|-----------|-----------|
| String-based | Object-oriented |
| Longer syntax | Cleaner syntax |
| `os.path.join()` | `/` operator |
| Older approach | Modern Python approach |
| More verbose | Easier to read |

---

## 🚀 Quick Example

```python
from pathlib import Path

project = Path("Projects") / "Python"

project.mkdir(exist_ok=True)

file = project / "hello.txt"

file.write_text("Welcome to pathlib!")

print(file.read_text())
```

### Output

```
Welcome to pathlib!
```

---

## ✅ Key Takeaways

- No installation required.
- `Path()` creates path objects.
- Use `/` instead of `os.path.join()`.
- Easily create, rename, delete, and search for files.
- Read and write files with built-in methods.
- `pathlib` is the **recommended way** to work with files and directories in modern Python.

---

⭐ **The `pathlib` module is the modern replacement for many `os.path` operations. Its clean, readable syntax makes file and directory management easier for beginners and professionals alike.**
