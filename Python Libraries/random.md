# 📚 Python Built-in Library: `random`

The `random` module is used to generate random numbers, make random selections, and shuffle data. It is commonly used in games, simulations, password generators, and testing.

```python
import random
```

---

# 🎲 `random.randint(a, b)`

Returns a random integer between `a` and `b` (inclusive).

```python
import random

num = random.randint(1, 10)
print(num)
```

Possible Output:

```
7
```

---

# 🎯 `random.randrange(start, stop, step)`

Returns a random number from a specified range.

```python
import random

print(random.randrange(0, 20, 2))
```

Possible Output:

```
14
```

---

# 🎲 `random.random()`

Returns a random float between **0.0** and **1.0**.

```python
import random

print(random.random())
```

Possible Output:

```
0.6732415
```

---

# 📋 `random.choice()`

Returns a random element from a sequence.

```python
import random

fruits = ["Apple", "Banana", "Mango", "Orange"]

print(random.choice(fruits))
```

Possible Output:

```
Mango
```

---

# 🎁 `random.choices()`

Returns multiple random elements (duplicates allowed).

```python
import random

colors = ["Red", "Blue", "Green"]

print(random.choices(colors, k=5))
```

Possible Output:

```
['Blue', 'Green', 'Blue', 'Red', 'Blue']
```

---

# 🎲 `random.sample()`

Returns unique random elements (no duplicates).

```python
import random

numbers = [1,2,3,4,5,6,7,8,9]

print(random.sample(numbers, 4))
```

Possible Output:

```
[8, 2, 6, 4]
```

---

# 🔀 `random.shuffle()`

Shuffles a list in place.

```python
import random

cards = [1,2,3,4,5]

random.shuffle(cards)

print(cards)
```

Possible Output:

```
[4, 1, 5, 2, 3]
```

---

# 🎯 `random.uniform(a, b)`

Returns a random floating-point number between `a` and `b`.

```python
import random

print(random.uniform(10, 20))
```

Possible Output:

```
15.4837
```

---

# 🌱 `random.seed()`

Produces the same random results every time.

```python
import random

random.seed(42)

print(random.randint(1,100))
```

Output (always):

```
82
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `randint(a,b)` | Random integer (inclusive) |
| `randrange()` | Random number from a range |
| `random()` | Random float (0–1) |
| `choice()` | Random item from a sequence |
| `choices()` | Multiple random items (duplicates allowed) |
| `sample()` | Multiple unique random items |
| `shuffle()` | Shuffle a list |
| `uniform()` | Random float in a range |
| `seed()` | Generate repeatable random values |

---

# 💡 Common Uses

- 🎮 Games
- 🔑 Password generators
- 🎲 Dice simulators
- 🧪 Testing
- 📊 Simulations
- 🤖 Randomized algorithms

---

⭐ The `random` module is part of Python's Standard Library, so **no installation is required**.
