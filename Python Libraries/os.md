# 📚 Python Built-in Library: `os`

The `os` module provides a way to interact with the operating system. It allows you to work with files, directories, environment variables, and execute system-level operations.

> **Note:** The `os` module is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import os
```

---

# 1️⃣ `os.getcwd()`

Returns the current working directory.

```python
import os

print(os.getcwd())
```

### Output

```
C:\Users\Ashraful\Documents
```

---

# 2️⃣ `os.chdir(path)`

Changes the current working directory.

```python
import os

os.chdir("C:\\Users\\Ashraful\\Desktop")

print(os.getcwd())
```

---

# 3️⃣ `os.listdir()`

Returns a list of files and folders inside a directory.

```python
import os

print(os.listdir())
```

### Output

```
['main.py', 'notes.txt', 'images']
```

---

# 4️⃣ `os.mkdir()`

Creates a new directory.

```python
import os

os.mkdir("Python_Project")
```

---

# 5️⃣ `os.makedirs()`

Creates nested directories.

```python
import os

os.makedirs("Projects/Python/Day1")
```

---

# 6️⃣ `os.rmdir()`

Removes an empty directory.

```python
import os

os.rmdir("Python_Project")
```

---

# 7️⃣ `os.remove()`

Deletes a file.

```python
import os

os.remove("notes.txt")
```

---

# 8️⃣ `os.rename()`

Renames a file or folder.

```python
import os

os.rename("old.txt", "new.txt")
```

---

# 9️⃣ `os.path.exists()`

Checks whether a file or directory exists.

```python
import os

print(os.path.exists("main.py"))
```

### Output

```
True
```

---

# 🔟 `os.path.isfile()`

Checks if the given path is a file.

```python
import os

print(os.path.isfile("main.py"))
```

### Output

```
True
```

---

# 1️⃣1️⃣ `os.path.isdir()`

Checks if the given path is a directory.

```python
import os

print(os.path.isdir("Projects"))
```

### Output

```
True
```

---

# 1️⃣2️⃣ `os.path.join()`

Creates file paths safely across different operating systems.

```python
import os

path = os.path.join("Projects", "Python", "main.py")

print(path)
```

### Output (Windows)

```
Projects\Python\main.py
```

### Output (Linux/macOS)

```
Projects/Python/main.py
```

---

# 1️⃣3️⃣ `os.path.basename()`

Returns the filename from a path.

```python
import os

path = "C:/Users/Ashraful/Documents/report.pdf"

print(os.path.basename(path))
```

### Output

```
report.pdf
```

---

# 1️⃣4️⃣ `os.path.dirname()`

Returns the directory portion of a path.

```python
import os

path = "C:/Users/Ashraful/Documents/report.pdf"

print(os.path.dirname(path))
```

### Output

```
C:/Users/Ashraful/Documents
```

---

# 1️⃣5️⃣ `os.path.abspath()`

Returns the absolute path.

```python
import os

print(os.path.abspath("main.py"))
```

### Output

```
C:\Users\Ashraful\Documents\main.py
```

---

# 1️⃣6️⃣ `os.environ`

Accesses environment variables.

```python
import os

print(os.environ.get("USERNAME"))
```

### Output

```
Ashraful
```

---

# 1️⃣7️⃣ `os.system()`

Executes a system command.

```python
import os

os.system("echo Hello World")
```

### Output

```
Hello World
```

> **Note:** Avoid using `os.system()` for user-supplied input. Prefer the `subprocess` module for new projects.

---

# 1️⃣8️⃣ `os.name`

Returns the operating system name.

```python
import os

print(os.name)
```

### Output (Windows)

```
nt
```

### Output (Linux/macOS)

```
posix
```

---

# 1️⃣9️⃣ Walking Through Directories (`os.walk()`)

Traverses all files and folders recursively.

```python
import os

for folder, subfolders, files in os.walk("Projects"):
    print("Folder:", folder)
    print("Files:", files)
```

---

# 2️⃣0️⃣ Delete an Empty Directory Tree

```python
import os

os.removedirs("Projects/Python/Day1")
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `getcwd()` | Get current directory |
| `chdir()` | Change directory |
| `listdir()` | List files/folders |
| `mkdir()` | Create directory |
| `makedirs()` | Create nested directories |
| `rmdir()` | Remove empty directory |
| `removedirs()` | Remove nested empty directories |
| `remove()` | Delete file |
| `rename()` | Rename file/folder |
| `system()` | Execute system command |
| `walk()` | Traverse directories |
| `name` | Operating system name |

### `os.path` Functions

| Function | Description |
|----------|-------------|
| `exists()` | Check if path exists |
| `isfile()` | Check if path is a file |
| `isdir()` | Check if path is a directory |
| `join()` | Join file paths safely |
| `basename()` | Get filename |
| `dirname()` | Get directory name |
| `abspath()` | Get absolute path |

---

# 💡 Common Uses

- 📁 File management
- 📂 Directory operations
- 🤖 Automation scripts
- 🖥️ System administration
- 🐧 Linux scripting
- 🔐 Cybersecurity tools
- 📊 Log management

---

## 🚀 Quick Example

```python
import os

for file in os.listdir():
    if file.endswith(".py"):
        print(file)
```

### Output

```
main.py
calculator.py
test.py
```

---

## ✅ Key Takeaways

- No installation required.
- Use `os` to interact with the operating system.
- `os.path` makes working with file paths easy.
- `os.walk()` is useful for searching directories recursively.
- Prefer `os.path.join()` instead of manually writing file paths.
- For executing external commands, prefer `subprocess` over `os.system()` in modern Python code.

---

⭐ **The `os` module is one of the most important Python libraries for automation, file management, scripting, DevOps, and cybersecurity. Mastering it will make working with the operating system much easier.**
