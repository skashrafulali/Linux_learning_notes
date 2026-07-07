# 📚 Python Built-in Library: `hashlib`

The `hashlib` module provides functions for generating **cryptographic hash values**. Hashing converts data into a fixed-length string, making it useful for password storage, file integrity checks, digital signatures, and cybersecurity.

> **Note:** The `hashlib` module is part of Python's Standard Library, so **no installation is required.**

---

# 📦 Import

```python
import hashlib
```

---

# 🔐 What is a Hash?

A **hash** is a fixed-size string generated from input data. The same input always produces the same hash, but even a tiny change in the input produces a completely different hash.

Example:

```
Hello
↓
8b1a9953c4611296a827abf8c47804d7
```

---

# 1️⃣ `hashlib.md5()`

Generates an MD5 hash.

```python
import hashlib

text = "Hello World"

hash_value = hashlib.md5(text.encode())

print(hash_value.hexdigest())
```

### Output

```
b10a8db164e0754105b7a99be72e3fe5
```

> **Warning:** MD5 is considered insecure for password storage and cryptographic purposes.

---

# 2️⃣ `hashlib.sha1()`

Generates a SHA-1 hash.

```python
import hashlib

text = "Hello World"

print(hashlib.sha1(text.encode()).hexdigest())
```

### Output

```
0a4d55a8d778e5022fab701977c5d840bbc486d0
```

> **Warning:** SHA-1 is also considered cryptographically broken for security-sensitive applications.

---

# 3️⃣ `hashlib.sha224()`

Generates a SHA-224 hash.

```python
import hashlib

print(hashlib.sha224(b"Python").hexdigest())
```

---

# 4️⃣ `hashlib.sha256()`

Generates a SHA-256 hash.

```python
import hashlib

text = "Hello World"

print(hashlib.sha256(text.encode()).hexdigest())
```

### Output

```
a591a6d40bf420404a011733cfb7b190...
```

---

# 5️⃣ `hashlib.sha384()`

Generates a SHA-384 hash.

```python
import hashlib

print(hashlib.sha384(b"Python").hexdigest())
```

---

# 6️⃣ `hashlib.sha512()`

Generates a SHA-512 hash.

```python
import hashlib

print(hashlib.sha512(b"Python").hexdigest())
```

---

# 7️⃣ Hash a File

Calculate the SHA-256 hash of a file.

```python
import hashlib

with open("example.txt", "rb") as file:
    data = file.read()

hash_value = hashlib.sha256(data).hexdigest()

print(hash_value)
```

---

# 8️⃣ Compare File Integrity

```python
import hashlib

original = hashlib.sha256(b"Python").hexdigest()
downloaded = hashlib.sha256(b"Python").hexdigest()

print(original == downloaded)
```

### Output

```
True
```

---

# 9️⃣ `digest()` vs `hexdigest()`

```python
import hashlib

text = hashlib.sha256(b"Hello")

print(text.digest())
print(text.hexdigest())
```

### Output

```
b'\x18_...'
185f8db32271fe25...
```

| Method | Output |
|---------|--------|
| `digest()` | Raw bytes |
| `hexdigest()` | Readable hexadecimal string |

---

# 🔟 Supported Algorithms

View all available hashing algorithms.

```python
import hashlib

print(hashlib.algorithms_available)
```

### Example Output

```
{'md5', 'sha1', 'sha224', 'sha256', 'sha384', 'sha512'}
```

---

# 1️⃣1️⃣ Create a Hash Object

```python
import hashlib

hash_obj = hashlib.new("sha256")

hash_obj.update(b"Hello")

print(hash_obj.hexdigest())
```

---

# 1️⃣2️⃣ Hash Multiple Values

```python
import hashlib

hash_obj = hashlib.sha256()

hash_obj.update(b"Hello ")
hash_obj.update(b"World")

print(hash_obj.hexdigest())
```

### Output

```
a591a6d40bf420404a011733cfb7b190...
```

---

# 📊 Common Hash Algorithms

| Algorithm | Digest Size | Recommended |
|-----------|------------:|-------------|
| MD5 | 128-bit | ❌ No |
| SHA-1 | 160-bit | ❌ No |
| SHA-224 | 224-bit | ✅ Yes |
| SHA-256 | 256-bit | ✅ Recommended |
| SHA-384 | 384-bit | ✅ Recommended |
| SHA-512 | 512-bit | ✅ Recommended |

---

# 💡 Common Uses

- 🔐 Password verification (with proper password hashing algorithms like `bcrypt` or `Argon2`, not raw SHA-256)
- 📁 File integrity verification
- 🌐 Digital signatures
- 🛡️ Cybersecurity
- ☁️ Blockchain
- 📦 Software download verification
- 🔍 Digital forensics

---

## 🚀 Quick Example

```python
import hashlib

password = "my_secure_password"

hash_value = hashlib.sha256(password.encode()).hexdigest()

print(hash_value)
```

### Output

```
f784b8d3d...
```

---

## ✅ Key Takeaways

- No installation required.
- Always encode strings before hashing (`.encode()`).
- Use `hexdigest()` for a readable hexadecimal hash.
- SHA-256 is a strong general-purpose hashing algorithm.
- Avoid using MD5 or SHA-1 for new security-sensitive applications.
- Hashing is **one-way**—you cannot recover the original input from its hash.

---

⭐ **The `hashlib` module is one of the most important libraries in cybersecurity. It is widely used for verifying file integrity, generating digital fingerprints, and supporting secure authentication systems.**
