# 📚 Python Built-in Library: `decimal`

The `decimal` module provides **precise decimal floating-point arithmetic**, avoiding the rounding errors that can occur with Python's built-in `float` type. It is especially useful for financial calculations, accounting, and scientific computations where precision is important.

> **Note:** The `decimal` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import decimal
```

Or import specific classes:

```python
from decimal import Decimal
```

---

# 🔹 Why Use `decimal` Instead of `float`?

Using `float`:

```python
print(0.1 + 0.2)
```

### Output

```
0.30000000000000004
```

Using `Decimal`:

```python
from decimal import Decimal

print(Decimal("0.1") + Decimal("0.2"))
```

### Output

```
0.3
```

---

# 1️⃣ `Decimal()`

Creates a decimal number with high precision.

```python
from decimal import Decimal

price = Decimal("99.99")

print(price)
```

### Output

```
99.99
```

---

# 2️⃣ Basic Arithmetic

```python
from decimal import Decimal

a = Decimal("10.5")
b = Decimal("2.5")

print(a + b)
print(a - b)
print(a * b)
print(a / b)
```

### Output

```
13.0
8.0
26.25
4.2
```

---

# 3️⃣ Precision Comparison

```python
from decimal import Decimal

print(0.1 * 3)

print(Decimal("0.1") * 3)
```

### Output

```
0.30000000000000004
0.3
```

---

# 4️⃣ `getcontext().prec`

Set the precision for decimal calculations.

```python
from decimal import Decimal, getcontext

getcontext().prec = 5

result = Decimal("1") / Decimal("7")

print(result)
```

### Output

```
0.14286
```

---

# 5️⃣ Rounding Numbers

```python
from decimal import Decimal

number = Decimal("3.14159265")

print(number.quantize(Decimal("0.01")))
```

### Output

```
3.14
```

---

# 6️⃣ Change Rounding Mode

```python
from decimal import Decimal, ROUND_UP

number = Decimal("3.141")

result = number.quantize(Decimal("0.01"), rounding=ROUND_UP)

print(result)
```

### Output

```
3.15
```

---

# 7️⃣ Square Root

```python
from decimal import Decimal

number = Decimal("16")

print(number.sqrt())
```

### Output

```
4
```

---

# 8️⃣ Power

```python
from decimal import Decimal

number = Decimal("5")

print(number ** 3)
```

### Output

```
125
```

---

# 9️⃣ Compare Decimal Numbers

```python
from decimal import Decimal

a = Decimal("10.50")
b = Decimal("10.5")

print(a == b)
```

### Output

```
True
```

---

# 🔟 Convert from Integer

```python
from decimal import Decimal

num = Decimal(100)

print(num)
```

### Output

```
100
```

---

# 1️⃣1️⃣ Financial Calculation Example

```python
from decimal import Decimal

price = Decimal("199.99")
tax = Decimal("0.15")

total = price + (price * tax)

print(total)
```

### Output

```
229.9885
```

---

# 1️⃣2️⃣ Common Rounding Modes

| Constant | Description |
|----------|-------------|
| `ROUND_HALF_UP` | Round to nearest (common method) |
| `ROUND_UP` | Always round up |
| `ROUND_DOWN` | Always round down |
| `ROUND_CEILING` | Round toward positive infinity |
| `ROUND_FLOOR` | Round toward negative infinity |

---

# 📊 Summary

| Function / Class | Description |
|------------------|-------------|
| `Decimal()` | Create decimal numbers |
| `getcontext().prec` | Set calculation precision |
| `quantize()` | Round decimal values |
| `sqrt()` | Square root |
| `**` | Power operation |

---

# 💡 Common Uses

- 💰 Financial applications
- 🏦 Banking systems
- 📊 Accounting software
- 🧾 Tax calculations
- 📈 Scientific computing
- 🤖 Automation
- 📋 Invoice and billing systems

---

## 🚀 Quick Example

```python
from decimal import Decimal

price = Decimal("49.99")
quantity = Decimal("3")

total = price * quantity

print(total)
```

### Output

```
149.97
```

---

## ✅ Key Takeaways

- No installation required.
- `Decimal` provides accurate decimal arithmetic.
- Avoid creating decimals from floating-point numbers (e.g., `Decimal(0.1)`); prefer strings like `Decimal("0.1")` to preserve exact values.
- `quantize()` is used for precise rounding.
- `getcontext().prec` controls calculation precision.
- `decimal` is preferred over `float` for financial and accounting applications.

---

⭐ **The `decimal` module is an essential Python library for high-precision arithmetic. It is widely used in finance, banking, accounting, taxation, and scientific applications where accuracy is critical.**
