# 📚 Python Built-in Library: `re`

The `re` module provides support for **Regular Expressions (Regex)**, which are powerful patterns used to search, match, replace, and validate text. It is widely used for text processing, data validation, web scraping, and cybersecurity.

> **Note:** The `re` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import re
```

---

# 1️⃣ `re.search()`

Searches for the **first occurrence** of a pattern in a string.

```python
import re

text = "Python is awesome"

result = re.search("awesome", text)

print(result)
```

### Output

```
<re.Match object; span=(10, 17), match='awesome'>
```

---

# 2️⃣ Check if a Pattern Exists

```python
import re

text = "Python is awesome"

if re.search("Python", text):
    print("Found!")
```

### Output

```
Found!
```

---

# 3️⃣ `re.match()`

Checks if the pattern matches **only at the beginning** of the string.

```python
import re

text = "Python Programming"

print(re.match("Python", text))
```

### Output

```
<re.Match object>
```

Example:

```python
print(re.match("Programming", text))
```

### Output

```
None
```

---

# 4️⃣ `re.findall()`

Returns all matches as a list.

```python
import re

text = "apple banana apple mango apple"

print(re.findall("apple", text))
```

### Output

```
['apple', 'apple', 'apple']
```

---

# 5️⃣ `re.finditer()`

Returns an iterator containing all matches.

```python
import re

text = "cat bat rat"

for match in re.finditer(r"\w+at", text):
    print(match.group())
```

### Output

```
cat
bat
rat
```

---

# 6️⃣ `re.sub()`

Replaces matched text.

```python
import re

text = "I like Java"

new_text = re.sub("Java", "Python", text)

print(new_text)
```

### Output

```
I like Python
```

---

# 7️⃣ `re.split()`

Splits a string based on a pattern.

```python
import re

text = "Python,Java,C++,Go"

print(re.split(",", text))
```

### Output

```
['Python', 'Java', 'C++', 'Go']
```

---

# 8️⃣ `re.fullmatch()`

Checks if the **entire string** matches the pattern.

```python
import re

print(re.fullmatch(r"\d{4}", "2026"))
```

### Output

```
<re.Match object>
```

Example:

```python
print(re.fullmatch(r"\d{4}", "2026ABC"))
```

### Output

```
None
```

---

# 9️⃣ Validate an Email Address

```python
import re

email = "user@example.com"

pattern = r"^[\w.-]+@[\w.-]+\.\w+$"

if re.fullmatch(pattern, email):
    print("Valid Email")
else:
    print("Invalid Email")
```

### Output

```
Valid Email
```

---

# 🔟 Extract Numbers from Text

```python
import re

text = "Order 123 costs 450 dollars."

numbers = re.findall(r"\d+", text)

print(numbers)
```

### Output

```
['123', '450']
```

---

# 1️⃣1️⃣ Extract Words

```python
import re

text = "Python is fun."

words = re.findall(r"\w+", text)

print(words)
```

### Output

```
['Python', 'is', 'fun']
```

---

# 1️⃣2️⃣ Ignore Case

```python
import re

text = "Python python PYTHON"

print(re.findall("python", text, re.IGNORECASE))
```

### Output

```
['Python', 'python', 'PYTHON']
```

---

# 1️⃣3️⃣ Common Regex Patterns

| Pattern | Meaning |
|---------|---------|
| `.` | Any character except newline |
| `\d` | Digit (0–9) |
| `\D` | Non-digit |
| `\w` | Letter, digit, or underscore |
| `\W` | Non-word character |
| `\s` | Whitespace |
| `\S` | Non-whitespace |
| `^` | Start of string |
| `$` | End of string |
| `+` | One or more |
| `*` | Zero or more |
| `?` | Zero or one |
| `{n}` | Exactly n times |
| `{m,n}` | Between m and n times |

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `search()` | Find first match |
| `match()` | Match at the beginning |
| `fullmatch()` | Match entire string |
| `findall()` | Return all matches |
| `finditer()` | Iterate over matches |
| `sub()` | Replace text |
| `split()` | Split string using regex |

---

# 💡 Common Uses

- 📧 Email validation
- 🔐 Password validation
- 📱 Phone number validation
- 🌐 URL matching
- 📄 Log file analysis
- 🕷️ Web scraping
- 🛡️ Cybersecurity
- 📊 Data cleaning

---

## 🚀 Quick Example

```python
import re

text = "My phone number is 01712345678."

phone = re.search(r"01\d{9}", text)

if phone:
    print(phone.group())
```

### Output

```
01712345678
```

---

## ✅ Key Takeaways

- No installation required.
- `search()` finds the first occurrence of a pattern.
- `match()` checks only the beginning of a string.
- `fullmatch()` validates an entire string.
- `findall()` extracts all matching values.
- `sub()` replaces text using regex.
- Regular expressions are powerful tools for text processing and validation.

---

⭐ **The `re` module is one of the most valuable Python libraries for text processing, automation, web scraping, data validation, and cybersecurity. Learning Regex will greatly improve your programming skills.**
