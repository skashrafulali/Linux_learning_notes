# 📚 Python Built-in Library: `heapq`

The `heapq` module provides an implementation of the **heap queue algorithm**, also known as a **priority queue**. It allows you to efficiently retrieve the smallest (or largest) element and is widely used in algorithms, scheduling, simulations, and graph problems.

> **Note:** The `heapq` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import heapq
```

---

# 🔹 What is a Heap?

A **heap** is a special tree-based data structure where the **smallest element is always at the root** (Min Heap).

Example:

```
Heap:
      1
     / \
    3   5
   / \
  7   9
```

In Python, `heapq` implements a **Min Heap** by default.

---

# 1️⃣ `heapify()`

Converts a list into a heap.

```python
import heapq

numbers = [5, 3, 8, 1, 9]

heapq.heapify(numbers)

print(numbers)
```

### Example Output

```
[1, 3, 8, 5, 9]
```

> The internal order may differ, but the smallest element will always be at index `0`.

---

# 2️⃣ `heappush()`

Adds an element to the heap.

```python
import heapq

heap = [2, 4, 6]

heapq.heapify(heap)

heapq.heappush(heap, 1)

print(heap)
```

### Output

```
[1, 2, 6, 4]
```

---

# 3️⃣ `heappop()`

Removes and returns the smallest element.

```python
import heapq

heap = [5, 2, 8, 1]

heapq.heapify(heap)

print(heapq.heappop(heap))
print(heap)
```

### Output

```
1
[2, 5, 8]
```

---

# 4️⃣ `heappushpop()`

Pushes a new item and then pops the smallest item.

```python
import heapq

heap = [2, 4, 6]

heapq.heapify(heap)

result = heapq.heappushpop(heap, 3)

print(result)
print(heap)
```

### Output

```
2
[3, 4, 6]
```

---

# 5️⃣ `heapreplace()`

Removes the smallest element and inserts a new one.

```python
import heapq

heap = [1, 3, 5]

heapq.heapify(heap)

result = heapq.heapreplace(heap, 4)

print(result)
print(heap)
```

### Output

```
1
[3, 4, 5]
```

---

# 6️⃣ `nlargest()`

Returns the largest **n** elements.

```python
import heapq

numbers = [8, 2, 10, 5, 7]

print(heapq.nlargest(3, numbers))
```

### Output

```
[10, 8, 7]
```

---

# 7️⃣ `nsmallest()`

Returns the smallest **n** elements.

```python
import heapq

numbers = [8, 2, 10, 5, 7]

print(heapq.nsmallest(3, numbers))
```

### Output

```
[2, 5, 7]
```

---

# 8️⃣ Priority Queue

```python
import heapq

tasks = []

heapq.heappush(tasks, (2, "Study"))

heapq.heappush(tasks, (1, "Eat"))

heapq.heappush(tasks, (3, "Sleep"))

while tasks:
    print(heapq.heappop(tasks))
```

### Output

```
(1, 'Eat')
(2, 'Study')
(3, 'Sleep')
```

---

# 9️⃣ Merge Sorted Lists

```python
import heapq

list1 = [1, 4, 7]
list2 = [2, 5, 8]
list3 = [3, 6, 9]

result = heapq.merge(list1, list2, list3)

print(list(result))
```

### Output

```
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

# 🔟 Simulate a Max Heap

Since `heapq` only supports a min heap, use negative values.

```python
import heapq

numbers = [5, 1, 9, 3]

max_heap = [-n for n in numbers]

heapq.heapify(max_heap)

print(-heapq.heappop(max_heap))
```

### Output

```
9
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `heapify()` | Convert a list into a heap |
| `heappush()` | Add an element |
| `heappop()` | Remove the smallest element |
| `heappushpop()` | Push then pop |
| `heapreplace()` | Pop then push |
| `nlargest()` | Largest *n* elements |
| `nsmallest()` | Smallest *n* elements |
| `merge()` | Merge sorted iterables |

---

# 💡 Common Uses

- 📋 Priority queues
- 📈 Scheduling systems
- 🛣️ Dijkstra's shortest path algorithm
- 🌐 Network routing
- 🎮 Game AI
- 🤖 Task scheduling
- 🧮 Competitive programming

---

## 🚀 Quick Example

```python
import heapq

scores = [95, 80, 70, 100, 85]

top_three = heapq.nlargest(3, scores)

print(top_three)
```

### Output

```
[100, 95, 85]
```

---

## ✅ Key Takeaways

- No installation required.
- `heapq` implements a **Min Heap**.
- `heappush()` inserts an element efficiently.
- `heappop()` always removes the smallest element.
- `nlargest()` and `nsmallest()` quickly retrieve top values.
- Use negative numbers to simulate a Max Heap.
- `heapq` is much more efficient than sorting when you only need the smallest or largest few elements.

---

⭐ **The `heapq` module is a powerful tool for implementing priority queues and solving optimization problems. It is widely used in algorithms, competitive programming, scheduling systems, graph algorithms, and data processing.**
