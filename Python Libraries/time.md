# 📚 Python Built-in Library: `time`

The `time` module provides functions for working with **timestamps, delays, execution time, and formatting time**.

> **Note:** `time` is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import time
```

---

# 1️⃣ `time.time()`

Returns the current Unix timestamp.

```python
import time

print(time.time())
```

### Output

```
1783158123.27491
```

---

# 2️⃣ `time.ctime()`

Converts a timestamp into a readable date.

```python
import time

print(time.ctime())
```

### Output

```
Sat Jul 4 10:48:12 2026
```

---

# 3️⃣ `time.sleep(seconds)`

Pauses the program.

```python
import time

print("Start")

time.sleep(3)

print("Finished")
```

### Output

```
Start
(wait 3 seconds)
Finished
```

---

# 4️⃣ `time.localtime()`

Returns the current local time as a structure.

```python
import time

t = time.localtime()

print(t)
```

### Output

```
time.struct_time(...)
```

---

# 5️⃣ Access Components

```python
import time

t = time.localtime()

print(t.tm_year)
print(t.tm_mon)
print(t.tm_mday)
print(t.tm_hour)
```

### Output

```
2026
7
4
10
```

---

# 6️⃣ `time.strftime()`

Formats the current time.

```python
import time

print(time.strftime("%d/%m/%Y"))
print(time.strftime("%H:%M:%S"))
```

### Output

```
04/07/2026
10:48:31
```

---

# 7️⃣ Measure Execution Time

```python
import time

start = time.time()

for i in range(1000000):
    pass

end = time.time()

print(end - start)
```

### Output

```
0.04
```

---

# 8️⃣ Convert Timestamp

```python
import time

timestamp = time.time()

print(time.ctime(timestamp))
```

---

# 📊 Common Format Codes

| Code | Meaning |
|------|---------|
| `%d` | Day |
| `%m` | Month |
| `%Y` | Year |
| `%H` | Hour |
| `%M` | Minute |
| `%S` | Second |
| `%A` | Weekday |
| `%B` | Month |

---

# 💡 Common Uses

- ⏱️ Measure program speed
- ⏳ Delays
- 🤖 Automation
- 📊 Benchmarking
- ⏰ Scheduling

---

## 🚀 Quick Example

```python
import time

for i in range(5):
    print(i)
    time.sleep(1)
```

### Output

```
0
1
2
3
4
```

*(Printed one number every second.)*

---

## ✅ Key Takeaways

- `time()` → Unix timestamp
- `ctime()` → Readable date
- `sleep()` → Pause execution
- `localtime()` → Local time structure
- `strftime()` → Format time
- Great for timing and automation scripts

⭐ The `time` module is ideal for delays, performance testing, and working with timestamps.
