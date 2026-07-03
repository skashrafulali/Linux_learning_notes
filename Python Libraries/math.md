# 📚 Python Built-in Library: `math`

The `math` module provides mathematical functions for performing calculations such as square roots, logarithms, trigonometry, factorials, and more.

> **Note:** The `math` module is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import math
```

---

# 1️⃣ `math.sqrt(x)`

Returns the square root of a number.

```python
import math

print(math.sqrt(25))
print(math.sqrt(81))
```

### Output

```
5.0
9.0
```

---

# 2️⃣ `math.pow(x, y)`

Raises `x` to the power of `y`.

```python
import math

print(math.pow(2, 5))
print(math.pow(7, 2))
```

### Output

```
32.0
49.0
```

> **Tip:** The `**` operator is generally faster than `math.pow()`.

---

# 3️⃣ `math.factorial(x)`

Returns the factorial of a positive integer.

```python
import math

print(math.factorial(5))
print(math.factorial(7))
```

### Output

```
120
5040
```

---

# 4️⃣ `math.ceil(x)`

Rounds a number **up** to the nearest integer.

```python
import math

print(math.ceil(4.2))
print(math.ceil(7.9))
```

### Output

```
5
8
```

---

# 5️⃣ `math.floor(x)`

Rounds a number **down** to the nearest integer.

```python
import math

print(math.floor(4.8))
print(math.floor(7.9))
```

### Output

```
4
7
```

---

# 6️⃣ `math.gcd(a, b)`

Returns the Greatest Common Divisor (GCD).

```python
import math

print(math.gcd(24, 36))
print(math.gcd(18, 30))
```

### Output

```
12
6
```

---

# 7️⃣ `math.lcm(a, b)`

Returns the Least Common Multiple (LCM).

```python
import math

print(math.lcm(12, 18))
print(math.lcm(5, 7))
```

### Output

```
36
35
```

---

# 8️⃣ `math.fabs(x)`

Returns the absolute (positive) value as a float.

```python
import math

print(math.fabs(-15))
print(math.fabs(-3.7))
```

### Output

```
15.0
3.7
```

---

# 9️⃣ `math.pi`

Returns the value of π (Pi).

```python
import math

print(math.pi)
```

### Output

```
3.141592653589793
```

---

# 🔟 `math.e`

Returns Euler's number.

```python
import math

print(math.e)
```

### Output

```
2.718281828459045
```

---

# 1️⃣1️⃣ `math.sin(x)`

Returns the sine of an angle (in radians).

```python
import math

print(math.sin(math.pi / 2))
```

### Output

```
1.0
```

---

# 1️⃣2️⃣ `math.cos(x)`

Returns the cosine of an angle.

```python
import math

print(math.cos(0))
```

### Output

```
1.0
```

---

# 1️⃣3️⃣ `math.tan(x)`

Returns the tangent of an angle.

```python
import math

print(math.tan(math.pi / 4))
```

### Output

```
0.9999999999999999
```

> This value is approximately `1` due to floating-point precision.

---

# 1️⃣4️⃣ `math.radians(x)`

Converts degrees to radians.

```python
import math

print(math.radians(180))
```

### Output

```
3.141592653589793
```

---

# 1️⃣5️⃣ `math.degrees(x)`

Converts radians to degrees.

```python
import math

print(math.degrees(math.pi))
```

### Output

```
180.0
```

---

# 1️⃣6️⃣ `math.log(x)`

Returns the natural logarithm (base *e*).

```python
import math

print(math.log(10))
```

### Output

```
2.302585092994046
```

---

# 1️⃣7️⃣ `math.log10(x)`

Returns the base-10 logarithm.

```python
import math

print(math.log10(1000))
```

### Output

```
3.0
```

---

# 1️⃣8️⃣ `math.exp(x)`

Returns **eˣ**.

```python
import math

print(math.exp(2))
```

### Output

```
7.38905609893065
```

---

# 1️⃣9️⃣ `math.isqrt(x)`

Returns the integer square root.

```python
import math

print(math.isqrt(17))
print(math.isqrt(81))
```

### Output

```
4
9
```

---

# 2️⃣0️⃣ `math.dist(p, q)`

Calculates the Euclidean distance between two points.

```python
import math

point1 = (2, 3)
point2 = (5, 7)

print(math.dist(point1, point2))
```

### Output

```
5.0
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `sqrt(x)` | Square root |
| `pow(x, y)` | Power |
| `factorial(x)` | Factorial |
| `ceil(x)` | Round up |
| `floor(x)` | Round down |
| `gcd(a, b)` | Greatest Common Divisor |
| `lcm(a, b)` | Least Common Multiple |
| `fabs(x)` | Absolute value |
| `pi` | Value of π |
| `e` | Euler's number |
| `sin(x)` | Sine |
| `cos(x)` | Cosine |
| `tan(x)` | Tangent |
| `radians(x)` | Degrees → Radians |
| `degrees(x)` | Radians → Degrees |
| `log(x)` | Natural logarithm |
| `log10(x)` | Base-10 logarithm |
| `exp(x)` | eˣ |
| `isqrt(x)` | Integer square root |
| `dist(p, q)` | Distance between two points |

---

# 💡 Common Uses

- ➗ Scientific calculations
- 📐 Geometry
- 📈 Statistics
- 🤖 Machine Learning
- 🎮 Game development
- 📊 Data Analysis
- 🧮 Competitive Programming

---

## 🚀 Quick Example

```python
import math

radius = 7

area = math.pi * math.pow(radius, 2)

print(f"Area of Circle = {area:.2f}")
```

### Output

```
Area of Circle = 153.94
```

---

## ✅ Key Takeaways

- Import using `import math`
- No installation required
- Contains 60+ mathematical functions and constants
- Ideal for scientific, engineering, and programming calculations
- More reliable than implementing mathematical formulas manually

---

⭐ **The `math` module is one of the most essential Python Standard Library modules and is widely used in competitive programming, data science, AI, and software development.**
