# 📚 Python Built-in Library: `csv`

The `csv` module allows you to **read from and write to CSV (Comma-Separated Values) files**. CSV files are widely used for storing tabular data such as spreadsheets, databases, reports, and exported application data.

> **Note:** The `csv` module is part of Python's Standard Library, so **no installation is required.**

---

## 📦 Import

```python
import csv
```

---

# 1️⃣ `csv.reader()`

Reads data from a CSV file.

Suppose `students.csv` contains:

```csv
Name,Age,Department
Alice,22,CSE
Bob,21,EEE
Charlie,23,BBA
```

```python
import csv

with open("students.csv", "r") as file:
    reader = csv.reader(file)

    for row in reader:
        print(row)
```

### Output

```
['Name', 'Age', 'Department']
['Alice', '22', 'CSE']
['Bob', '21', 'EEE']
['Charlie', '23', 'BBA']
```

---

# 2️⃣ Skip the Header Row

```python
import csv

with open("students.csv", "r") as file:
    reader = csv.reader(file)

    next(reader)

    for row in reader:
        print(row)
```

### Output

```
['Alice', '22', 'CSE']
['Bob', '21', 'EEE']
['Charlie', '23', 'BBA']
```

---

# 3️⃣ `csv.writer()`

Writes data to a CSV file.

```python
import csv

with open("students.csv", "w", newline="") as file:
    writer = csv.writer(file)

    writer.writerow(["Name", "Age", "Department"])
    writer.writerow(["Alice", 22, "CSE"])
    writer.writerow(["Bob", 21, "EEE"])
```

Generated `students.csv`

```csv
Name,Age,Department
Alice,22,CSE
Bob,21,EEE
```

---

# 4️⃣ `writerows()`

Writes multiple rows at once.

```python
import csv

rows = [
    ["Alice", 22, "CSE"],
    ["Bob", 21, "EEE"],
    ["Charlie", 23, "BBA"]
]

with open("students.csv", "w", newline="") as file:
    writer = csv.writer(file)

    writer.writerow(["Name", "Age", "Department"])
    writer.writerows(rows)
```

---

# 5️⃣ `csv.DictReader()`

Reads a CSV file as dictionaries.

```python
import csv

with open("students.csv", "r") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row)
```

### Output

```
{'Name': 'Alice', 'Age': '22', 'Department': 'CSE'}
{'Name': 'Bob', 'Age': '21', 'Department': 'EEE'}
{'Name': 'Charlie', 'Age': '23', 'Department': 'BBA'}
```

---

# 6️⃣ Access Individual Columns

```python
import csv

with open("students.csv", "r") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["Name"], row["Department"])
```

### Output

```
Alice CSE
Bob EEE
Charlie BBA
```

---

# 7️⃣ `csv.DictWriter()`

Writes dictionaries to a CSV file.

```python
import csv

with open("students.csv", "w", newline="") as file:
    fieldnames = ["Name", "Age", "Department"]

    writer = csv.DictWriter(file, fieldnames=fieldnames)

    writer.writeheader()

    writer.writerow({
        "Name": "Alice",
        "Age": 22,
        "Department": "CSE"
    })

    writer.writerow({
        "Name": "Bob",
        "Age": 21,
        "Department": "EEE"
    })
```

---

# 8️⃣ Change the Delimiter

By default, CSV files use commas. You can use a different delimiter such as a semicolon.

```python
import csv

with open("students.csv", "w", newline="") as file:
    writer = csv.writer(file, delimiter=";")

    writer.writerow(["Name", "Age"])
    writer.writerow(["Alice", 22])
```

Generated file

```csv
Name;Age
Alice;22
```

---

# 9️⃣ Count Rows in a CSV File

```python
import csv

count = 0

with open("students.csv", "r") as file:
    reader = csv.reader(file)

    next(reader)

    for row in reader:
        count += 1

print(count)
```

### Output

```
3
```

---

# 🔟 Read a Specific Column

```python
import csv

with open("students.csv", "r") as file:
    reader = csv.DictReader(file)

    for row in reader:
        print(row["Age"])
```

### Output

```
22
21
23
```

---

# 1️⃣1️⃣ Append New Rows

```python
import csv

with open("students.csv", "a", newline="") as file:
    writer = csv.writer(file)

    writer.writerow(["David", 24, "BBA"])
```

The new row is added to the end of the file.

---

# 1️⃣2️⃣ CSV File Modes

| Mode | Description |
|------|-------------|
| `"r"` | Read |
| `"w"` | Write (overwrites existing data) |
| `"a"` | Append |
| `"r+"` | Read and write |

---

# 📊 Summary

| Function | Description |
|----------|-------------|
| `reader()` | Read CSV file |
| `writer()` | Write CSV file |
| `writerow()` | Write one row |
| `writerows()` | Write multiple rows |
| `DictReader()` | Read rows as dictionaries |
| `DictWriter()` | Write dictionaries |
| `writeheader()` | Write column headers |

---

# 💡 Common Uses

- 📊 Excel data processing
- 🗄️ Database exports
- 🤖 Automation scripts
- 📈 Data analysis
- 🌐 Data exchange
- 📋 Reports
- 🧪 Machine Learning datasets

---

## 🚀 Quick Example

```python
import csv

with open("employees.csv", "w", newline="") as file:
    writer = csv.writer(file)

    writer.writerow(["ID", "Name", "Salary"])
    writer.writerow([1, "Alice", 50000])
    writer.writerow([2, "Bob", 60000])

print("CSV file created successfully!")
```

### Output

```
CSV file created successfully!
```

Generated `employees.csv`

```csv
ID,Name,Salary
1,Alice,50000
2,Bob,60000
```

---

## ✅ Key Takeaways

- No installation required.
- `reader()` reads CSV files row by row.
- `writer()` creates and writes CSV files.
- `DictReader()` reads each row as a dictionary.
- `DictWriter()` writes dictionary data.
- Always use `newline=""` when writing CSV files to avoid blank lines.
- CSV files are widely used for spreadsheets, databases, and data exchange.

---

⭐ **The `csv` module is an essential Python library for handling spreadsheet data, reports, data analysis, automation, and machine learning datasets.**
