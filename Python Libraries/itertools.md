# 📚 Python Built-in Library: `itertools`

The `itertools` module provides a collection of **fast, memory-efficient iterator building tools**. It is commonly used for looping, generating combinations and permutations, filtering data, and solving algorithmic problems.

> **Note:** The `itertools` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import itertools
```

Or import specific functions:

```python
from itertools import count, cycle, repeat
```

---

# 1️⃣ `count()`

Creates an infinite sequence of numbers.

```python
from itertools import count

for num in count(1):
    print(num)

    if num == 5:
        break
```

### Output

```
1
2
3
4
5
```

---

# 2️⃣ `cycle()`

Repeats an iterable forever.

```python
from itertools import cycle

colors = cycle(["Red", "Green", "Blue"])

for i in range(6):
    print(next(colors))
```

### Output

```
Red
Green
Blue
Red
Green
Blue
```

---

# 3️⃣ `repeat()`

Repeats the same value multiple times.

```python
from itertools import repeat

for item in repeat("Python", 3):
    print(item)
```

### Output

```
Python
Python
Python
```

---

# 4️⃣ `chain()`

Combines multiple iterables into one.

```python
from itertools import chain

numbers = chain([1, 2], [3, 4], [5, 6])

print(list(numbers))
```

### Output

```
[1, 2, 3, 4, 5, 6]
```

---

# 5️⃣ `compress()`

Filters data using selectors.

```python
from itertools import compress

letters = ["A", "B", "C", "D"]

selectors = [1, 0, 1, 0]

print(list(compress(letters, selectors)))
```

### Output

```
['A', 'C']
```

---

# 6️⃣ `accumulate()`

Returns accumulated results.

```python
from itertools import accumulate

numbers = [1, 2, 3, 4]

print(list(accumulate(numbers)))
```

### Output

```
[1, 3, 6, 10]
```

---

# 7️⃣ `product()`

Returns the Cartesian product.

```python
from itertools import product

result = product([1, 2], ["A", "B"])

print(list(result))
```

### Output

```
[(1, 'A'), (1, 'B'), (2, 'A'), (2, 'B')]
```

---

# 8️⃣ `permutations()`

Returns all possible arrangements.

```python
from itertools import permutations

print(list(permutations([1, 2, 3])))
```

### Output

```
[
(1, 2, 3),
(1, 3, 2),
(2, 1, 3),
(2, 3, 1),
(3, 1, 2),
(3, 2, 1)
]
```

---

# 9️⃣ `combinations()`

Returns all unique combinations.

```python
from itertools import combinations

print(list(combinations([1, 2, 3], 2)))
```

### Output

```
[
(1, 2),
(1, 3),
(2, 3)
]
```

---

# 🔟 `combinations_with_replacement()`

Returns combinations where elements can repeat.

```python
from itertools import combinations_with_replacement

print(list(combinations_with_replacement([1, 2], 2)))
```

### Output

```
[
(1, 1),
(1, 2),
(2, 2)
]
```

---

# 1️⃣1️⃣ `groupby()`

Groups consecutive identical elements.

```python
from itertools import groupby

data = "AAABBBCCDAA"

for key, group in groupby(data):
    print(key, list(group))
```

### Output

```
A ['A', 'A', 'A']
B ['B', 'B', 'B']
C ['C', 'C']
D ['D']
A ['A', 'A']
```

> **Note:** `groupby()` groups consecutive items only. Sort your data first if needed.

---

# 1️⃣2️⃣ `islice()`

Slices an iterator.

```python
from itertools import islice

numbers = range(100)

print(list(islice(numbers, 5, 10)))
```

### Output

```
[5, 6, 7, 8, 9]
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `count()` | Infinite counting iterator |
| `cycle()` | Repeat iterable forever |
| `repeat()` | Repeat a value |
| `chain()` | Combine iterables |
| `compress()` | Filter using selectors |
| `accumulate()` | Running totals |
| `product()` | Cartesian product |
| `permutations()` | All arrangements |
| `combinations()` | Unique combinations |
| `combinations_with_replacement()` | Combinations allowing repeats |
| `groupby()` | Group consecutive items |
| `islice()` | Slice iterators |

---

# 💡 Common Uses

- 🧮 Combinatorics
- 📊 Data processing
- 🤖 Automation
- 🏆 Competitive programming
- 📈 Data analysis
- 🧩 Algorithm design
- 🔐 Password and keyspace generation (for educational purposes)

---

## 🚀 Quick Example

```python
from itertools import combinations

students = ["Alice", "Bob", "Charlie", "David"]

teams = combinations(students, 2)

for team in teams:
    print(team)
```

### Output

```
('Alice', 'Bob')
('Alice', 'Charlie')
('Alice', 'David')
('Bob', 'Charlie')
('Bob', 'David')
('Charlie', 'David')
```

---

## ✅ Key Takeaways

- No installation required.
- `count()`, `cycle()`, and `repeat()` create iterators.
- `chain()` combines multiple iterables.
- `product()`, `permutations()`, and `combinations()` are useful for combinatorial problems.
- `groupby()` groups consecutive values.
- `islice()` allows slicing iterators without converting them to lists.
- `itertools` is optimized for speed and memory efficiency.

---

⭐ **The `itertools` module is an essential tool for writing efficient Python code. It is widely used in data analysis, competitive programming, automation, algorithm development, and scientific computing.**
