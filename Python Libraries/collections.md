# 📚 Python Built-in Library: `collections`

The `collections` module provides specialized container data types that extend Python's built-in data structures such as lists, tuples, and dictionaries. These containers make your code cleaner, faster, and more efficient.

> **Note:** The `collections` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import collections
```

Or import specific classes:

```python
from collections import Counter, defaultdict, deque, namedtuple
```

---

# 1️⃣ `Counter`

Counts the frequency of elements in an iterable.

```python
from collections import Counter

fruits = ["apple", "banana", "apple", "orange", "banana", "apple"]

count = Counter(fruits)

print(count)
```

### Output

```
Counter({'apple': 3, 'banana': 2, 'orange': 1})
```

---

# 2️⃣ Most Common Elements

```python
from collections import Counter

text = "mississippi"

count = Counter(text)

print(count.most_common(3))
```

### Output

```
[('i', 4), ('s', 4), ('p', 2)]
```

---

# 3️⃣ Count Words

```python
from collections import Counter

sentence = "python is fun python is easy"

words = sentence.split()

print(Counter(words))
```

### Output

```
Counter({'python': 2, 'is': 2, 'fun': 1, 'easy': 1})
```

---

# 4️⃣ `defaultdict`

Provides a default value for missing keys.

```python
from collections import defaultdict

students = defaultdict(int)

students["Alice"] += 1

print(students)
```

### Output

```
defaultdict(<class 'int'>, {'Alice': 1})
```

---

# 5️⃣ Group Data with `defaultdict`

```python
from collections import defaultdict

data = [
    ("CSE", "Alice"),
    ("EEE", "Bob"),
    ("CSE", "Charlie")
]

groups = defaultdict(list)

for dept, student in data:
    groups[dept].append(student)

print(groups)
```

### Output

```
defaultdict(<class 'list'>,
{'CSE': ['Alice', 'Charlie'],
 'EEE': ['Bob']})
```

---

# 6️⃣ `deque`

A double-ended queue that allows fast insertion and deletion from both ends.

```python
from collections import deque

queue = deque([1, 2, 3])

queue.append(4)

queue.appendleft(0)

print(queue)
```

### Output

```
deque([0, 1, 2, 3, 4])
```

---

# 7️⃣ Remove Elements from a `deque`

```python
from collections import deque

queue = deque([1, 2, 3, 4])

queue.pop()

queue.popleft()

print(queue)
```

### Output

```
deque([2, 3])
```

---

# 8️⃣ Rotate a `deque`

```python
from collections import deque

numbers = deque([1, 2, 3, 4, 5])

numbers.rotate(2)

print(numbers)
```

### Output

```
deque([4, 5, 1, 2, 3])
```

---

# 9️⃣ `namedtuple`

Creates lightweight objects with named fields.

```python
from collections import namedtuple

Student = namedtuple("Student", ["name", "age", "department"])

s = Student("Alice", 21, "CSE")

print(s.name)
print(s.age)
```

### Output

```
Alice
21
```

---

# 🔟 Convert a `namedtuple` to a Dictionary

```python
from collections import namedtuple

Student = namedtuple("Student", ["name", "cgpa"])

s = Student("Alice", 3.85)

print(s._asdict())
```

### Output

```
{'name': 'Alice', 'cgpa': 3.85}
```

---

# 1️⃣1️⃣ `OrderedDict`

Maintains insertion order (mainly useful for compatibility with older Python versions).

```python
from collections import OrderedDict

student = OrderedDict()

student["Name"] = "Alice"
student["Age"] = 21
student["Department"] = "CSE"

print(student)
```

### Output

```
OrderedDict([
('Name', 'Alice'),
('Age', 21),
('Department', 'CSE')
])
```

> **Note:** Since Python 3.7, the built-in `dict` also preserves insertion order, so `OrderedDict` is less commonly needed.

---

# 1️⃣2️⃣ `ChainMap`

Combines multiple dictionaries into one view.

```python
from collections import ChainMap

dict1 = {"name": "Alice"}

dict2 = {"age": 21}

combined = ChainMap(dict1, dict2)

print(combined["name"])
print(combined["age"])
```

### Output

```
Alice
21
```

---

# 📊 Summary

| Class | Description |
|--------|-------------|
| `Counter` | Count occurrences of elements |
| `defaultdict` | Dictionary with default values |
| `deque` | Double-ended queue |
| `namedtuple` | Tuple with named fields |
| `OrderedDict` | Dictionary preserving insertion order |
| `ChainMap` | Combine multiple dictionaries |

---

# 💡 Common Uses

- 📊 Frequency counting
- 📄 Text analysis
- 📋 Queue and stack implementation
- 🤖 Automation scripts
- 🗂️ Data grouping
- 🧮 Competitive programming
- 🔐 Cybersecurity log analysis

---

## 🚀 Quick Example

```python
from collections import Counter

logs = [
    "INFO",
    "ERROR",
    "INFO",
    "WARNING",
    "ERROR",
    "INFO"
]

count = Counter(logs)

print(count)
print(count.most_common(1))
```

### Output

```
Counter({
'INFO': 3,
'ERROR': 2,
'WARNING': 1
})

[('INFO', 3)]
```

---

## ✅ Key Takeaways

- No installation required.
- `Counter` counts elements efficiently.
- `defaultdict` avoids `KeyError` for missing keys.
- `deque` is faster than lists for queue operations.
- `namedtuple` provides readable, lightweight objects.
- `ChainMap` combines multiple dictionaries without copying data.
- `collections` offers optimized data structures for cleaner and faster code.

---

⭐ **The `collections` module is one of Python's most powerful Standard Library modules. It simplifies data handling, improves performance, and is widely used in automation, data analysis, competitive programming, and cybersecurity.**
