# 📚 Python Built-in Library: `datetime`

The `datetime` module helps you work with **dates, times, timestamps, and time differences**. It is widely used in automation, logging, scheduling, APIs, and real-world applications.

> **Note:** `datetime` is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import datetime
```

Or

```python
from datetime import datetime
```

---

# 1️⃣ `datetime.now()`

Returns the current local date and time.

```python
from datetime import datetime

print(datetime.now())
```

### Output

```
2026-07-04 10:45:21.564327
```

---

# 2️⃣ `date.today()`

Returns today's date.

```python
from datetime import date

print(date.today())
```

### Output

```
2026-07-04
```

---

# 3️⃣ Create a Specific Date

```python
from datetime import date

birthday = date(2003, 5, 12)

print(birthday)
```

### Output

```
2003-05-12
```

---

# 4️⃣ Create a Specific Date & Time

```python
from datetime import datetime

meeting = datetime(2026, 7, 5, 14, 30, 0)

print(meeting)
```

### Output

```
2026-07-05 14:30:00
```

---

# 5️⃣ Access Individual Components

```python
from datetime import datetime

now = datetime.now()

print(now.year)
print(now.month)
print(now.day)
print(now.hour)
print(now.minute)
print(now.second)
```

### Output

```
2026
7
4
10
45
21
```

---

# 6️⃣ Format Date & Time (`strftime()`)

```python
from datetime import datetime

now = datetime.now()

print(now.strftime("%d/%m/%Y"))
print(now.strftime("%I:%M %p"))
print(now.strftime("%A"))
```

### Output

```
04/07/2026
10:45 AM
Saturday
```

---

# 7️⃣ Convert String to Date (`strptime()`)

```python
from datetime import datetime

date = datetime.strptime("04-07-2026", "%d-%m-%Y")

print(date)
```

### Output

```
2026-07-04 00:00:00
```

---

# 8️⃣ Add Days (`timedelta`)

```python
from datetime import datetime, timedelta

today = datetime.now()

future = today + timedelta(days=10)

print(future)
```

---

# 9️⃣ Subtract Dates

```python
from datetime import date

d1 = date(2026,7,4)
d2 = date(2026,6,20)

print(d1 - d2)
```

### Output

```
14 days, 0:00:00
```

---

# 🔟 Current UTC Time

```python
from datetime import datetime

print(datetime.utcnow())
```

---

# 📊 Common Format Codes

| Code | Meaning |
|------|---------|
| `%d` | Day |
| `%m` | Month |
| `%Y` | Year |
| `%H` | Hour (24h) |
| `%I` | Hour (12h) |
| `%M` | Minute |
| `%S` | Second |
| `%A` | Weekday |
| `%B` | Month Name |
| `%p` | AM / PM |

---

# 💡 Common Uses

- 📅 Scheduling
- 📝 Logging
- 🤖 Automation
- 🌐 APIs
- 📊 Data Analysis

---

## 🚀 Quick Example

```python
from datetime import datetime

print(datetime.now().strftime("%d %B %Y"))
```

### Output

```
04 July 2026
```

---

## ✅ Key Takeaways

- `datetime.now()` → Current date & time
- `date.today()` → Today's date
- `strftime()` → Format dates
- `strptime()` → Parse dates
- `timedelta()` → Add/Subtract time
- Access `.year`, `.month`, `.day`, etc.

⭐ `datetime` is one of Python's most frequently used modules in real-world applications.
