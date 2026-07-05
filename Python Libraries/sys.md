# 📚 Python Built-in Library: `sys`

The `sys` module provides access to **Python interpreter variables and functions**. It is commonly used for handling command-line arguments, exiting programs, checking the Python version, and interacting with the interpreter.

> **Note:** The `sys` module is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import sys
```

---

# 1️⃣ `sys.version`

Returns the Python version currently running.

```python
import sys

print(sys.version)
```

### Output

```
3.13.0 (main, ...)
```

---

# 2️⃣ `sys.version_info`

Returns version information as a tuple-like object.

```python
import sys

print(sys.version_info)
```

### Output

```
sys.version_info(major=3, minor=13, micro=0, releaselevel='final', serial=0)
```

---

# 3️⃣ `sys.platform`

Returns the operating system platform.

```python
import sys

print(sys.platform)
```

### Output (Windows)

```
win32
```

### Output (Linux)

```
linux
```

---

# 4️⃣ `sys.executable`

Returns the path of the Python interpreter.

```python
import sys

print(sys.executable)
```

### Output

```
C:\Python313\python.exe
```

---

# 5️⃣ `sys.argv`

Returns the command-line arguments passed to a Python script.

```python
import sys

print(sys.argv)
```

Suppose you run:

```bash
python app.py hello 123
```

### Output

```
['app.py', 'hello', '123']
```

---

# 6️⃣ Access Individual Arguments

```python
import sys

print("Script Name:", sys.argv[0])

print("First Argument:", sys.argv[1])
```

Run:

```bash
python app.py Python
```

### Output

```
Script Name: app.py
First Argument: Python
```

---

# 7️⃣ `sys.exit()`

Terminates the program immediately.

```python
import sys

print("Program Started")

sys.exit()

print("This line will never execute.")
```

### Output

```
Program Started
```

---

# 8️⃣ `sys.path`

Displays the list of directories where Python searches for modules.

```python
import sys

print(sys.path)
```

### Example Output

```
[
 'C:\\Projects',
 'C:\\Python313\\Lib',
 ...
]
```

---

# 9️⃣ Add a New Module Search Path

```python
import sys

sys.path.append("C:\\MyModules")

print(sys.path)
```

---

# 🔟 `sys.maxsize`

Returns the largest integer a Python list or container can typically use as an index on the current platform.

```python
import sys

print(sys.maxsize)
```

### Output (64-bit)

```
9223372036854775807
```

---

# 1️⃣1️⃣ `sys.getsizeof()`

Returns the memory size of an object in bytes.

```python
import sys

x = [1, 2, 3, 4, 5]

print(sys.getsizeof(x))
```

### Output

```
104
```

*(Output may vary depending on the Python version and platform.)*

---

# 1️⃣2️⃣ `sys.stdin`

Reads user input from the keyboard.

```python
import sys

name = sys.stdin.readline()

print("Hello,", name)
```

---

# 1️⃣3️⃣ `sys.stdout`

Writes output directly to the console.

```python
import sys

sys.stdout.write("Hello World!\n")
```

### Output

```
Hello World!
```

---

# 1️⃣4️⃣ `sys.stderr`

Writes error messages to the standard error stream.

```python
import sys

sys.stderr.write("Error: Something went wrong!\n")
```

---

# 1️⃣5️⃣ `sys.modules`

Returns a dictionary of all imported modules.

```python
import sys

print("math" in sys.modules)
```

### Output

```
False
```

If you import the module first:

```python
import math
import sys

print("math" in sys.modules)
```

### Output

```
True
```

---

# 📊 Summary

| Function / Attribute | Description |
|----------------------|-------------|
| `version` | Python version |
| `version_info` | Detailed version information |
| `platform` | Operating system |
| `executable` | Python interpreter path |
| `argv` | Command-line arguments |
| `exit()` | Exit the program |
| `path` | Module search paths |
| `maxsize` | Maximum platform integer size |
| `getsizeof()` | Memory usage of an object |
| `stdin` | Standard input |
| `stdout` | Standard output |
| `stderr` | Standard error |
| `modules` | Imported modules |

---

# 💡 Common Uses

- 💻 Command-line applications
- 📦 Module management
- 🛑 Exiting programs
- 📊 Memory inspection
- 🔍 Debugging
- 🤖 Automation scripts
- 🖥️ System information

---

## 🚀 Quick Example

```python
import sys

if len(sys.argv) > 1:
    print("Hello,", sys.argv[1])
else:
    print("No name provided.")
```

Run:

```bash
python app.py Ashraful
```

### Output

```
Hello, Ashraful
```

---

## ✅ Key Takeaways

- No installation required.
- `sys.argv` is used to read command-line arguments.
- `sys.exit()` stops program execution.
- `sys.path` shows where Python looks for modules.
- `sys.version` and `sys.platform` provide interpreter and system information.
- `sys.getsizeof()` helps inspect memory usage.

---

⭐ **The `sys` module is essential for understanding how Python interacts with the operating system and the Python interpreter. It is widely used in scripting, automation, command-line tools, and debugging.**
