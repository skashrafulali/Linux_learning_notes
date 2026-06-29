# 🔍 Linux File Finding Commands

Finding files efficiently is one of the most important Linux skills, especially for system administrators, developers, and cybersecurity professionals. Linux provides several powerful commands to search for files, directories, and even specific content inside files.

---

# 📌 1. `find` – Search Files and Directories

The `find` command searches the filesystem in real time. It is one of the most powerful file-searching tools available.

## Basic Syntax

```bash
find [starting_directory] [options] [search_expression]
```

Example:

```bash
find . -name "notes.txt"
```

Searches for `notes.txt` in the current directory and all subdirectories.

---

# 📂 Find by File Name

### Exact Name

```bash
find . -name "report.pdf"
```

### Case-Insensitive Search

```bash
find . -iname "report.pdf"
```

Matches:

```
report.pdf
REPORT.PDF
Report.pdf
```

---

# 📁 Find Directories

Search only for directories.

```bash
find /home -type d -name "Documents"
```

Output Example:

```
/home/ashraful/Documents
```

---

# 📄 Find Regular Files

Search only for files.

```bash
find /home -type f -name "*.txt"
```

Finds all `.txt` files.

---

# 🔎 Find by Extension

### All PDF Files

```bash
find . -type f -name "*.pdf"
```

### All Images

```bash
find . -type f \( -name "*.jpg" -o -name "*.png" \)
```

---

# 📏 Find by File Size

### Larger Than 100 MB

```bash
find / -size +100M
```

### Smaller Than 5 MB

```bash
find / -size -5M
```

### Exactly 50 KB

```bash
find / -size 50k
```

Size Units

| Unit | Meaning |
|------|---------|
| c | Bytes |
| k | Kilobytes |
| M | Megabytes |
| G | Gigabytes |

---

# ⏰ Find by Modification Time

### Modified Within the Last 7 Days

```bash
find . -mtime -7
```

### Modified More Than 30 Days Ago

```bash
find . -mtime +30
```

---

# 👤 Find by Owner

Find all files owned by a specific user.

```bash
find /home -user ashraful
```

---

# 🔐 Find by Permissions

Find files with permission `777`.

```bash
find / -perm 777
```

Find files with permission `644`.

```bash
find . -perm 644
```

---

# ⚙️ Find Executable Files

```bash
find /usr/bin -type f -executable
```

Useful for locating executable programs.

---

# 📭 Find Empty Files

```bash
find . -empty
```

Finds:

- Empty files
- Empty directories

---

# 🗑️ Delete Files Found by `find`

Delete all `.tmp` files.

```bash
find . -name "*.tmp" -delete
```

⚠️ Be careful! Files deleted this way cannot be recovered easily.

---

# 🚀 Execute Commands on Search Results

Change permissions for every shell script.

```bash
find . -name "*.sh" -exec chmod +x {} \;
```

Delete all log files.

```bash
find . -name "*.log" -exec rm {} \;
```

---

# 📋 Find and List Detailed Information

```bash
find . -name "*.txt" -ls
```

Displays file permissions, owner, size, and modification time.

---

# ⚡ `locate` – Fast File Search

Unlike `find`, the `locate` command searches a pre-built database, making it much faster.

Example:

```bash
locate report.pdf
```

Output:

```
/home/ashraful/Documents/report.pdf
```

---

# 🔄 Update the Locate Database

If new files don't appear in search results, update the database.

```bash
sudo updatedb
```

---

# 📝 `which` – Find an Executable in PATH

Locate where a command is installed.

```bash
which python
```

Example Output:

```
/usr/bin/python
```

---

# 📝 `whereis` – Locate Binary, Source, and Manual

```bash
whereis python
```

Example Output:

```
python:
/usr/bin/python
/usr/lib/python3
/usr/share/man/man1/python.1.gz
```

---

# 📝 `type` – Identify Command Type

```bash
type ls
```

Example Output:

```
ls is aliased to 'ls --color=auto'
```

or

```
ls is /usr/bin/ls
```

---

# 🔍 Search Inside Files Using `grep`

Search for a word inside a file.

```bash
grep "password" notes.txt
```

Search recursively.

```bash
grep -r "admin" .
```

Ignore case.

```bash
grep -ri "linux" .
```

Show line numbers.

```bash
grep -rn "error" .
```

---

# 📚 Common Search Examples

Find every PDF

```bash
find . -name "*.pdf"
```

Find all hidden files

```bash
find . -name ".*"
```

Find all shell scripts

```bash
find . -name "*.sh"
```

Find files larger than 1 GB

```bash
find / -size +1G
```

Find files modified today

```bash
find . -mtime -1
```

Find every executable

```bash
find / -type f -executable
```

Find empty directories

```bash
find . -type d -empty
```

---

# ⚖️ `find` vs `locate`

| Feature | `find` | `locate` |
|---------|--------|----------|
| Searches Live Filesystem | ✅ | ❌ |
| Very Fast | ❌ | ✅ |
| Uses Database | ❌ | ✅ |
| Search by Size | ✅ | ❌ |
| Search by Permission | ✅ | ❌ |
| Search by Date | ✅ | ❌ |
| Execute Actions | ✅ | ❌ |

---

# 💡 Pro Tips

- Use `find` when you need accurate, real-time results.
- Use `locate` for quick filename searches.
- Combine `find` with `grep` to locate files containing specific text.
- Always double-check before using `-delete` or `-exec rm`.

---

# 📖 Summary

Linux offers several tools for finding files and directories:

- `find` → Powerful real-time filesystem search
- `locate` → Fast database-based search
- `which` → Locate executables in your `PATH`
- `whereis` → Find binaries, source files, and manuals
- `type` → Identify how a command is interpreted
- `grep` → Search for text inside files

Mastering these commands will make navigating and managing Linux systems much more efficient.

---

⭐ *Thanks for reading! If you found this helpful, consider giving the repository a star or following my Linux learning journey.*
