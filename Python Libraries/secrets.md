# 📚 Python Built-in Library: `secrets`

The `secrets` module is used to generate **cryptographically secure random numbers, tokens, and passwords**. Unlike the `random` module, `secrets` is designed specifically for **security-sensitive applications** such as authentication, password generation, and API keys.

> **Note:** The `secrets` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import secrets
```

---

# 🔹 Why Use `secrets` Instead of `random`?

The `random` module is suitable for simulations and games, but **it is not cryptographically secure**.

```python
import random

print(random.randint(1, 100))
```

For secure applications, use:

```python
import secrets

print(secrets.randbelow(100))
```

---

# 1️⃣ `randbelow()`

Generates a secure random integer below a given value.

```python
import secrets

number = secrets.randbelow(100)

print(number)
```

### Example Output

```
57
```

---

# 2️⃣ `choice()`

Securely selects a random element from a sequence.

```python
import secrets

colors = ["Red", "Green", "Blue", "Yellow"]

print(secrets.choice(colors))
```

### Example Output

```
Blue
```

---

# 3️⃣ `token_bytes()`

Generates a secure random byte string.

```python
import secrets

token = secrets.token_bytes(16)

print(token)
```

### Example Output

```
b'\x9d\xf2\xa1...'
```

---

# 4️⃣ `token_hex()`

Generates a secure hexadecimal token.

```python
import secrets

token = secrets.token_hex(16)

print(token)
```

### Example Output

```
d4f3a8c9b8d7e1f6c5a4b3d2e1f0a9b8
```

---

# 5️⃣ `token_urlsafe()`

Generates a URL-safe secure token.

```python
import secrets

token = secrets.token_urlsafe(16)

print(token)
```

### Example Output

```
tq9x1X9V2cA2QjQ8w0f6xQ
```

---

# 6️⃣ Generate a Secure Password

```python
import secrets
import string

characters = string.ascii_letters + string.digits + string.punctuation

password = "".join(secrets.choice(characters) for _ in range(12))

print(password)
```

### Example Output

```
G#8aP!2zL@9m
```

---

# 7️⃣ Generate a Numeric OTP

```python
import secrets
import string

otp = "".join(secrets.choice(string.digits) for _ in range(6))

print(otp)
```

### Example Output

```
483921
```

---

# 8️⃣ Generate a Random API Key

```python
import secrets

api_key = secrets.token_hex(32)

print(api_key)
```

### Example Output

```
4e1c6e0b7a9b...
```

---

# 9️⃣ `compare_digest()`

Securely compares two strings to help prevent timing attacks.

```python
import secrets

password1 = "Python123"
password2 = "Python123"

print(secrets.compare_digest(password1, password2))
```

### Output

```
True
```

---

# 🔟 Generate a Session Token

```python
import secrets

session_id = secrets.token_urlsafe(32)

print(session_id)
```

### Example Output

```
2vU5D9nMzG8kE2wQ1cY5VQbKx7eLhA9PzR
```

---

# 1️⃣1️⃣ Generate a Random Boolean

```python
import secrets

result = secrets.choice([True, False])

print(result)
```

### Example Output

```
True
```

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `randbelow()` | Secure random integer |
| `choice()` | Secure random selection |
| `token_bytes()` | Secure random bytes |
| `token_hex()` | Secure hexadecimal token |
| `token_urlsafe()` | URL-safe secure token |
| `compare_digest()` | Secure string comparison |

---

# 💡 Common Uses

- 🔐 Password generation
- 🔑 API keys
- 🔒 Authentication tokens
- 📱 OTP generation
- 🌐 Session IDs
- 🛡️ Cybersecurity applications
- ☁️ Web development

---

## 🚀 Quick Example

```python
import secrets
import string

alphabet = string.ascii_letters + string.digits

password = "".join(secrets.choice(alphabet) for _ in range(16))

print(password)
```

### Example Output

```
A7xK9mQ2Lp8ZrT5N
```

---

## ✅ Key Takeaways

- No installation required.
- `secrets` is designed for **cryptographically secure** random values.
- Use `randbelow()` instead of `random.randint()` for security-sensitive applications.
- `token_hex()` and `token_urlsafe()` are ideal for generating API keys and session tokens.
- `compare_digest()` securely compares sensitive values.
- Prefer `secrets` over `random` whenever security matters.

---

⭐ **The `secrets` module is an essential library for cybersecurity, authentication systems, password generation, session management, and secure web applications. It should always be used instead of `random` for security-related tasks.**
