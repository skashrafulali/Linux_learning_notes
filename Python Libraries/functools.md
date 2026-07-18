# 📚 Python Built-in Library: `functools`

The `functools` module provides **higher-order functions** and utilities that work with other functions. It helps you write cleaner, reusable, and more efficient code through features like partial functions, caching, function reduction, and decorators.

> **Note:** The `functools` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import functools
```

Or import specific functions:

```python
from functools import reduce, partial, lru_cache
```

---

# 1️⃣ `reduce()`

Applies a function cumulatively to the items of an iterable.

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

result = reduce(lambda x, y: x + y, numbers)

print(result)
```

### Output

```
15
```

---

# 2️⃣ Multiply All Numbers

```python
from functools import reduce

numbers = [2, 3, 4]

result = reduce(lambda x, y: x * y, numbers)

print(result)
```

### Output

```
24
```

---

# 3️⃣ `partial()`

Creates a new function with some arguments already filled in.

```python
from functools import partial

def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)

print(square(5))
```

### Output

```
25
```

---

# 4️⃣ Another `partial()` Example

```python
from functools import partial

def greet(greeting, name):
    return f"{greeting}, {name}!"

hello = partial(greet, "Hello")

print(hello("Alice"))
```

### Output

```
Hello, Alice!
```

---

# 5️⃣ `lru_cache()`

Caches function results to improve performance.

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(10))
```

### Output

```
55
```

---

# 6️⃣ Cache Information

```python
from functools import lru_cache

@lru_cache(maxsize=5)
def square(n):
    return n * n

square(2)
square(2)
square(3)

print(square.cache_info())
```

### Example Output

```
CacheInfo(hits=1, misses=2, maxsize=5, currsize=2)
```

---

# 7️⃣ Clear the Cache

```python
from functools import lru_cache

@lru_cache
def cube(n):
    return n ** 3

cube(5)

cube.cache_clear()

print(cube.cache_info())
```

### Output

```
CacheInfo(hits=0, misses=0, maxsize=128, currsize=0)
```

---

# 8️⃣ `cmp_to_key()`

Converts an old-style comparison function into a key function for sorting.

```python
from functools import cmp_to_key

def compare(a, b):
    return len(a) - len(b)

words = ["banana", "kiwi", "apple", "fig"]

sorted_words = sorted(words, key=cmp_to_key(compare))

print(sorted_words)
```

### Output

```
['fig', 'kiwi', 'apple', 'banana']
```

---

# 9️⃣ `wraps()`

Preserves metadata when creating decorators.

```python
from functools import wraps

def decorator(func):

    @wraps(func)
    def wrapper():
        print("Before function")
        func()

    return wrapper

@decorator
def hello():
    """Say hello."""
    print("Hello!")

print(hello.__name__)
```

### Output

```
hello
```

---

# 🔟 Using `wraps()`

```python
from functools import wraps

def logger(func):

    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Function called")
        return func(*args, **kwargs)

    return wrapper

@logger
def add(a, b):
    return a + b

print(add(3, 5))
```

### Output

```
Function called
8
```

---

# 1️⃣1️⃣ `total_ordering`

Automatically fills in missing comparison methods.

```python
from functools import total_ordering

@total_ordering
class Student:

    def __init__(self, marks):
        self.marks = marks

    def __eq__(self, other):
        return self.marks == other.marks

    def __lt__(self, other):
        return self.marks < other.marks

a = Student(80)
b = Student(90)

print(a < b)
print(a >= b)
```

### Output

```
True
False
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `reduce()` | Reduce iterable to one value |
| `partial()` | Create partially applied functions |
| `lru_cache()` | Cache function results |
| `cmp_to_key()` | Convert comparison function to key |
| `wraps()` | Preserve function metadata in decorators |
| `total_ordering` | Generate comparison methods |

---

# 💡 Common Uses

- ⚡ Performance optimization
- 🤖 Automation
- 🧠 Memoization
- 📊 Data processing
- 🧩 Functional programming
- 🏆 Competitive programming
- 🖥️ Decorator development

---

## 🚀 Quick Example

```python
from functools import reduce

prices = [100, 250, 150, 300]

total = reduce(lambda x, y: x + y, prices)

print(total)
```

### Output

```
800
```

---

## ✅ Key Takeaways

- No installation required.
- `reduce()` combines values into a single result.
- `partial()` creates reusable functions with preset arguments.
- `lru_cache()` speeds up repeated function calls.
- `wraps()` is essential when writing decorators.
- `cmp_to_key()` helps customize sorting.
- `functools` makes code cleaner, faster, and more reusable.

---

⭐ **The `functools` module is an essential part of Python for functional programming, optimization, decorators, and writing efficient, maintainable code.**
