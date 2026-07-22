# 📚 Python Built-in Library: `bisect`

The `bisect` module provides functions for **maintaining a sorted list** without having to sort it after every insertion. It uses the **binary search algorithm**, making searches and insertions much faster than a linear search.

> **Note:** The `bisect` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import bisect
```

---

# 🔹 What is Binary Search?

Binary search repeatedly divides a **sorted list** in half to find the correct position of an element.

Example:

```
Sorted List:
[10, 20, 30, 40, 50]

Search for 30
        ↓
Found at index 2
```

Binary search has a time complexity of **O(log n)** for searching.

---

# 1️⃣ `bisect()`

Returns the insertion index while keeping the list sorted.

```python
import bisect

numbers = [10, 20, 30, 40, 50]

index = bisect.bisect(numbers, 35)

print(index)
```

### Output

```
3
```

---

# 2️⃣ `bisect_left()`

Returns the leftmost insertion position.

```python
import bisect

numbers = [10, 20, 20, 20, 30]

print(bisect.bisect_left(numbers, 20))
```

### Output

```
1
```

---

# 3️⃣ `bisect_right()`

Returns the rightmost insertion position.

```python
import bisect

numbers = [10, 20, 20, 20, 30]

print(bisect.bisect_right(numbers, 20))
```

### Output

```
4
```

---

# 4️⃣ `insort()`

Inserts an element while maintaining sorted order.

```python
import bisect

numbers = [10, 20, 30, 40]

bisect.insort(numbers, 25)

print(numbers)
```

### Output

```
[10, 20, 25, 30, 40]
```

---

# 5️⃣ `insort_left()`

Inserts an element at the leftmost valid position.

```python
import bisect

numbers = [10, 20, 20, 30]

bisect.insort_left(numbers, 20)

print(numbers)
```

### Output

```
[10, 20, 20, 20, 30]
```

---

# 6️⃣ `insort_right()`

Inserts an element at the rightmost valid position.

```python
import bisect

numbers = [10, 20, 20, 30]

bisect.insort_right(numbers, 20)

print(numbers)
```

### Output

```
[10, 20, 20, 20, 30]
```

---

# 7️⃣ Check if an Element Exists

```python
import bisect

numbers = [10, 20, 30, 40, 50]

index = bisect.bisect_left(numbers, 30)

if index < len(numbers) and numbers[index] == 30:
    print("Found")
else:
    print("Not Found")
```

### Output

```
Found
```

---

# 8️⃣ Find the Correct Position

```python
import bisect

scores = [60, 70, 80, 90]

new_score = 85

position = bisect.bisect(scores, new_score)

print(position)
```

### Output

```
3
```

---

# 9️⃣ Insert Multiple Values

```python
import bisect

numbers = [10, 30, 50]

for num in [20, 40, 60]:
    bisect.insort(numbers, num)

print(numbers)
```

### Output

```
[10, 20, 30, 40, 50, 60]
```

---

# 🔟 Find the Nearest Greater Value

```python
import bisect

numbers = [10, 20, 30, 40, 50]

index = bisect.bisect_right(numbers, 35)

print(numbers[index])
```

### Output

```
40
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `bisect()` | Find insertion position (right) |
| `bisect_left()` | Leftmost insertion position |
| `bisect_right()` | Rightmost insertion position |
| `insort()` | Insert while keeping sorted |
| `insort_left()` | Insert on the left |
| `insort_right()` | Insert on the right |

---

# 💡 Common Uses

- 🔍 Binary search
- 📊 Maintaining sorted lists
- 🤖 Automation
- 📈 Ranking systems
- 🎮 Leaderboards
- 🏆 Competitive programming
- 🗂️ Data processing

---

## 🚀 Quick Example

```python
import bisect

leaderboard = [1200, 1500, 1800, 2100]

new_score = 1700

bisect.insort(leaderboard, new_score)

print(leaderboard)
```

### Output

```
[1200, 1500, 1700, 1800, 2100]
```

---

## ✅ Key Takeaways

- No installation required.
- `bisect` works **only with sorted lists**.
- `bisect_left()` inserts before duplicate values.
- `bisect_right()` inserts after duplicate values.
- `insort()` inserts while maintaining sorted order.
- Binary search operations run in **O(log n)** for searching, though insertion into a Python list is **O(n)** because elements may need to be shifted.
- `bisect` is excellent for maintaining ordered data efficiently.

---

⭐ **The `bisect` module is a lightweight yet powerful tool for binary search and sorted list management. It is widely used in competitive programming, ranking systems, scheduling, search algorithms, and data processing.**
