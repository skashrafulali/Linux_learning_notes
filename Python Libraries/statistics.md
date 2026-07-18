# 📚 Python Built-in Library: `statistics`

The `statistics` module provides functions for calculating **mathematical statistics** of numeric data. It is useful for finding averages, medians, modes, standard deviations, variances, and more.

> **Note:** The `statistics` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import statistics
```

Or import specific functions:

```python
from statistics import mean, median, mode
```

---

# 1️⃣ `mean()`

Returns the arithmetic mean (average).

```python
import statistics

numbers = [10, 20, 30, 40, 50]

print(statistics.mean(numbers))
```

### Output

```
30
```

---

# 2️⃣ `median()`

Returns the middle value of the data.

```python
import statistics

numbers = [5, 1, 8, 2, 7]

print(statistics.median(numbers))
```

### Output

```
5
```

---

# 3️⃣ `mode()`

Returns the most frequently occurring value.

```python
import statistics

numbers = [1, 2, 2, 3, 3, 3, 4]

print(statistics.mode(numbers))
```

### Output

```
3
```

---

# 4️⃣ `multimode()`

Returns all values with the highest frequency.

```python
import statistics

numbers = [1, 2, 2, 3, 3]

print(statistics.multimode(numbers))
```

### Output

```
[2, 3]
```

---

# 5️⃣ `fmean()`

Returns the floating-point arithmetic mean.

```python
import statistics

numbers = [10, 20, 30]

print(statistics.fmean(numbers))
```

### Output

```
20.0
```

---

# 6️⃣ `geometric_mean()`

Returns the geometric mean.

```python
import statistics

numbers = [4, 16, 64]

print(statistics.geometric_mean(numbers))
```

### Output

```
16.0
```

---

# 7️⃣ `harmonic_mean()`

Returns the harmonic mean.

```python
import statistics

numbers = [2, 4, 8]

print(statistics.harmonic_mean(numbers))
```

### Output

```
3.43
```

---

# 8️⃣ `variance()`

Returns the sample variance.

```python
import statistics

numbers = [2, 4, 4, 4, 5, 5, 7, 9]

print(statistics.variance(numbers))
```

### Output

```
4.571428571428571
```

---

# 9️⃣ `stdev()`

Returns the sample standard deviation.

```python
import statistics

numbers = [2, 4, 4, 4, 5, 5, 7, 9]

print(statistics.stdev(numbers))
```

### Output

```
2.138089935
```

---

# 🔟 `pvariance()`

Returns the population variance.

```python
import statistics

numbers = [2, 4, 4, 4, 5, 5, 7, 9]

print(statistics.pvariance(numbers))
```

### Output

```
4
```

---

# 1️⃣1️⃣ `pstdev()`

Returns the population standard deviation.

```python
import statistics

numbers = [2, 4, 4, 4, 5, 5, 7, 9]

print(statistics.pstdev(numbers))
```

### Output

```
2.0
```

---

# 1️⃣2️⃣ `median_low()`

Returns the lower median.

```python
import statistics

numbers = [10, 20, 30, 40]

print(statistics.median_low(numbers))
```

### Output

```
20
```

---

# 1️⃣3️⃣ `median_high()`

Returns the higher median.

```python
import statistics

numbers = [10, 20, 30, 40]

print(statistics.median_high(numbers))
```

### Output

```
30
```

---

# 1️⃣4️⃣ `median_grouped()`

Estimates the median for grouped continuous data.

```python
import statistics

numbers = [52, 52, 53, 54]

print(statistics.median_grouped(numbers))
```

### Example Output

```
52.5
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `mean()` | Arithmetic mean |
| `fmean()` | Floating-point mean |
| `median()` | Middle value |
| `median_low()` | Lower median |
| `median_high()` | Higher median |
| `median_grouped()` | Median for grouped data |
| `mode()` | Most frequent value |
| `multimode()` | All most frequent values |
| `geometric_mean()` | Geometric mean |
| `harmonic_mean()` | Harmonic mean |
| `variance()` | Sample variance |
| `stdev()` | Sample standard deviation |
| `pvariance()` | Population variance |
| `pstdev()` | Population standard deviation |

---

# 💡 Common Uses

- 📊 Data analysis
- 📈 Machine learning
- 📉 Statistical calculations
- 🤖 Automation
- 🧮 Scientific computing
- 📚 Academic projects
- 📋 Reports and analytics

---

## 🚀 Quick Example

```python
import statistics

marks = [85, 90, 78, 92, 88]

print("Mean:", statistics.mean(marks))
print("Median:", statistics.median(marks))
print("Standard Deviation:", statistics.stdev(marks))
```

### Output

```
Mean: 86.6
Median: 88
Standard Deviation: 5.46
```

---

## ✅ Key Takeaways

- No installation required.
- `mean()` calculates the average.
- `median()` finds the middle value.
- `mode()` returns the most common value.
- `variance()` and `stdev()` measure data spread.
- `pvariance()` and `pstdev()` are used for population data.
- The `statistics` module is ideal for basic statistical analysis without needing external libraries like NumPy or Pandas.

---

⭐ **The `statistics` module is an excellent built-in tool for performing descriptive statistical analysis in Python. It's widely used in data science, machine learning, research, finance, and academic projects.**
