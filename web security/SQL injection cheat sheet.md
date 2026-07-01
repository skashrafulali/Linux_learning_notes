# SQL Injection Cheat Sheet (Study Notes)

> Personal notes compiled while learning SQL Injection from labs and documentation.

---

# 📌 String Concatenation

Combine multiple strings into one.

| Database             | Syntax                |
| -------------------- | --------------------- |
| Oracle               | `'foo' \|\| 'bar'`    |
| Microsoft SQL Server | `'foo' + 'bar'`       |
| PostgreSQL           | `'foo' \|\| 'bar'`    |
| MySQL                | `CONCAT('foo','bar')` |

---

# 📌 Substring Functions

Extract part of a string.

| Database   | Example                   |
| ---------- | ------------------------- |
| Oracle     | `SUBSTR('foobar',4,2)`    |
| SQL Server | `SUBSTRING('foobar',4,2)` |
| PostgreSQL | `SUBSTRING('foobar',4,2)` |
| MySQL      | `SUBSTRING('foobar',4,2)` |

---

# 📌 SQL Comments

Useful for terminating the remainder of a query.

| Database   | Syntax                                     |
| ---------- | ------------------------------------------ |
| Oracle     | `-- comment`                               |
| SQL Server | `-- comment`, `/* comment */`              |
| PostgreSQL | `-- comment`, `/* comment */`              |
| MySQL      | `# comment`, `-- comment`, `/* comment */` |

---

# 📌 Database Version

Common commands used to identify the database version.

| Database   | Query                          |
| ---------- | ------------------------------ |
| Oracle     | `SELECT banner FROM v$version` |
| SQL Server | `SELECT @@version`             |
| PostgreSQL | `SELECT version()`             |
| MySQL      | `SELECT @@version`             |

---

# 📌 Database Enumeration

Useful metadata tables.

| Database | Tables                                                    |
| -------- | --------------------------------------------------------- |
| Oracle   | `all_tables`, `all_tab_columns`                           |
| Others   | `information_schema.tables`, `information_schema.columns` |

---

# 📌 Conditional Logic

Useful concepts:

* CASE expressions
* IF statements
* Boolean conditions
* Error-based conditions
* Time-based conditions

---

# 📌 Time Delay Functions

Common functions used during blind SQL Injection testing.

| Database   | Function                      |
| ---------- | ----------------------------- |
| Oracle     | `dbms_pipe.receive_message()` |
| SQL Server | `WAITFOR DELAY`               |
| PostgreSQL | `pg_sleep()`                  |
| MySQL      | `SLEEP()`                     |

---

# 📌 Useful Concepts Learned

* String concatenation
* String extraction
* SQL comments
* Database fingerprinting
* Metadata enumeration
* Error-based SQL Injection
* Blind SQL Injection
* Time-based SQL Injection
* Conditional queries

---

# 📝 Notes

* Different database engines use different SQL syntax.
* Fingerprinting the backend database is an important first step.
* `information_schema` is commonly used to enumerate database structure.
* Time delays can help identify blind SQL Injection vulnerabilities.
* Always practice only in legal environments such as PortSwigger Web Security Academy, TryHackMe, or Hack The Box.

---

# 📚 Resources

* PortSwigger Web Security Academy
* OWASP Web Security Testing Guide
* OWASP SQL Injection Prevention Cheat Sheet
