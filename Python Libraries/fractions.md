# 📚 Python Built-in Library: `fractions`

The `fractions` module provides support for **rational number arithmetic**. It represents numbers as **fractions (numerator/denominator)** instead of floating-point values, ensuring exact calculations without rounding errors.

> **Note:** The `fractions` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import fractions
```

Or import the `Fraction` class:

```python
from fractions import Fraction
```

---

# 🔹 Why Use `fractions`?

Using `float`:

```python
print(0.1 + 0.2)
```

### Output

```
0.30000000000000004
```

Using `Fraction`:

```python
from fractions import Fraction

print(Fraction(1, 10) + Fraction(2, 10))
```

### Output

```
3/10
```

---

# 1️⃣ `Fraction()`

Creates a fraction from a numerator and denominator.

```python
from fractions import Fraction

f = Fraction(3, 4)

print(f)
```

### Output

```
3/4
```

---

# 2️⃣ Automatic Simplification

Fractions are automatically reduced to their simplest form.

```python
from fractions import Fraction

print(Fraction(10, 20))
```

### Output

```
1/2
```

---

# 3️⃣ Basic Arithmetic

```python
from fractions import Fraction

a = Fraction(1, 2)
b = Fraction(1, 3)

print(a + b)
print(a - b)
print(a * b)
print(a / b)
```

### Output

```
5/6
1/6
1/6
3/2
```

---

# 4️⃣ Create from a Float

```python
from fractions import Fraction

f = Fraction(0.5)

print(f)
```

### Output

```
1/2
```

> **Note:** Floats may already contain small rounding errors. When possible, create fractions from strings for exact values.

---

# 5️⃣ Create from a String

```python
from fractions import Fraction

print(Fraction("3/8"))
```

### Output

```
3/8
```

---

# 6️⃣ `limit_denominator()`

Finds the closest fraction with a limited denominator.

```python
from fractions import Fraction

f = Fraction(3.14159)

print(f.limit_denominator(100))
```

### Output

```
311/99
```

---

# 7️⃣ Access Numerator and Denominator

```python
from fractions import Fraction

f = Fraction(7, 5)

print(f.numerator)
print(f.denominator)
```

### Output

```
7
5
```

---

# 8️⃣ Convert to Float

```python
from fractions import Fraction

f = Fraction(3, 4)

print(float(f))
```

### Output

```
0.75
```

---

# 9️⃣ Convert to Integer

```python
from fractions import Fraction

f = Fraction(8, 2)

print(int(f))
```

### Output

```
4
```

---

# 🔟 Compare Fractions

```python
from fractions import Fraction

a = Fraction(1, 2)
b = Fraction(2, 4)

print(a == b)
print(a > Fraction(1, 3))
```

### Output

```
True
True
```

---

# 1️⃣1️⃣ Power Operation

```python
from fractions import Fraction

f = Fraction(2, 3)

print(f ** 2)
```

### Output

```
4/9
```

---

# 1️⃣2️⃣ Mixed Arithmetic

```python
from fractions import Fraction

result = Fraction(3, 4) + 2

print(result)
```

### Output

```
11/4
```

---

# 📊 Summary

| Function / Class | Description |
|------------------|-------------|
| `Fraction()` | Create a fraction |
| `limit_denominator()` | Find the closest simple fraction |
| `numerator` | Return numerator |
| `denominator` | Return denominator |
| `float()` | Convert to float |
| `int()` | Convert to integer |

---

# 💡 Common Uses

- ➗ Exact fraction calculations
- 📐 Mathematics
- 📊 Scientific computing
- 📚 Educational software
- 🤖 Automation
- 🧮 Symbolic calculations
- 📈 Financial calculations requiring exact ratios

---

## 🚀 Quick Example

```python
from fractions import Fraction

recipe = Fraction(3, 4)
double_recipe = recipe * 2

print(double_recipe)
```

### Output

```
3/2
```

---

## ✅ Key Takeaways

- No installation required.
- `Fraction()` creates exact rational numbers.
- Fractions are automatically simplified.
- Supports all arithmetic operations.
- `limit_denominator()` approximates decimal values as simple fractions.
- `fractions` avoids floating-point precision errors.
- Ideal for mathematics, scientific computing, and exact ratio calculations.

---

⭐ **The `fractions` module is a powerful built-in library for exact arithmetic with rational numbers. It is widely used in mathematics, education, engineering, and applications where precision matters more than floating-point speed.**
