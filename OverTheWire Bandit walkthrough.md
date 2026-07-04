# OverTheWire Bandit Walkthrough (Level 0 → 12)

## 🎯 Goal

I'm currently learning Linux, command-line navigation, and basic cybersecurity concepts through the OverTheWire Bandit wargame.

These are my personal notes and solutions for Bandit Levels 0–12, including what I learned and why the commands worked.


# Dont try to follow the passwords I have given.OverTheWire may change the passwords whenever they like.
# Do follow the instruction to retrieve the passwords.


---

# Bandit 0

### Password

```
bandit0
```

### Objective

Connect to the Bandit server.

### Command Used

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### What I Learned

* `ssh` allows secure remote login.
* `-p` specifies a custom port number.
* The first level teaches basic SSH access.

### Password Found

```text
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

Using:

```bash
cat readme
```

---

# Bandit 1

### Challenge

The password was stored in a file named:

```text
-
```

### Problem

Linux interprets `-` as an option rather than a filename.

### Command Used

```bash
cat ./-
```

### What I Learned

* `./` tells Linux to use the file in the current directory.
* This prevents `cat` from treating `-` as a command option.

### Password Found

```text
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

---

# Bandit 2

### Challenge

The password was stored in a file with spaces in its name.

### Command Used

```bash
cat ./--spaces\ in\ this\ filename--
```

or

```bash
cat "./--spaces in this filename--"
```

### What I Learned

* Spaces break command arguments.
* Quotes or backslashes help Linux read the filename correctly.
* `./` prevents confusion with filenames starting with `--`.

### Password Found

```text
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

---

# Bandit 3

### Challenge

The password was hidden inside a hidden file.

### Commands Used

```bash
ls -a
cat .hidden
```

### What I Learned

* Hidden files begin with a dot (`.`).
* `ls -a` shows all files, including hidden ones.

### Password Found

```text
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

---

# Bandit 4

### Challenge

One file among many contained human-readable text.

### Command Used

```bash
file ./*
```

### What I Learned

* `file` identifies file types.
* ASCII files are human-readable.
* Much faster than opening files one by one.

### Password Found

```text
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

---

# Bandit 5

### Hint

The file was:

* Human-readable
* 1033 bytes
* Not executable

### Command Used

```bash
find . -type f -size 1033c ! -executable
```

### What I Learned

* `find` searches recursively.
* `-type f` searches for files.
* `-size 1033c` means exactly 1033 bytes.
* `! -executable` excludes executable files.

### Password Found

```text
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

---

# Bandit 6

### Hint

The file was:

* Owned by user `bandit7`
* Owned by group `bandit6`
* 33 bytes in size

### Command Used

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### What I Learned

* Searches the entire filesystem.
* `2>/dev/null` hides permission denied errors.

### Password Found

```text
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

---

# Bandit 7

### Hint

Password stored next to the word:

```text
millionth
```

### Command Used

```bash
grep "millionth" data.txt
```

### What I Learned

* `grep` searches text files for matching lines.
* Extremely useful for large datasets.

### Password Found

```text
dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

---

# Bandit 8

### Hint

Find the line that appears only once.

### Commands Used

```bash
sort data.txt | uniq -u
```

Useful alternative:

```bash
sort data.txt | uniq -c
```

### What I Learned

* `uniq` only works correctly on sorted data.
* `uniq -u` shows unique entries.
* `uniq -c` counts occurrences.

### Password Found

```text
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

---

# Bandit 9

### Hint

Password is one of the few human-readable strings and is preceded by several `=` signs.

### Command Used

```bash
strings data.txt | grep "==="
```

### What I Learned

* `strings` extracts readable text from binary files.
* `grep` helps locate specific patterns quickly.

### Password Found

```text
FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

---

# Bandit 10

### Hint

Password stored in Base64 encoded data.

### Command Used

```bash
base64 -d data.txt
```

### What I Learned

* Base64 is encoding, not encryption.
* `-d` decodes encoded content.

### Password Found

```text
dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

---

# Bandit 11

### Hint

Data was encoded using ROT13.

### Command Used

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### What I Learned

* `tr` translates characters.
* ROT13 shifts letters by 13 positions.

### Password Found

```text
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

---

# Bandit 12

### Hint

The file was a hexdump that had been compressed multiple times.

### Commands Used

Create workspace:

```bash
mktemp -d
cd /tmp/tempfolder
```

Copy file:

```bash
cp ~/data.txt .
```

Reverse hexdump:

```bash
xxd -r data.txt > data
```

Identify file type:

```bash
file data
```

Extract based on type:

```bash
gunzip file.gz
bunzip2 file.bz2
tar -xf file.tar
```

Repeat:

```bash
file filename
```

until a text file appears.

### What I Learned

* `xxd -r` reverses a hexdump.
* `file` identifies file types.
* `gunzip`, `bunzip2`, and `tar` extract archives.
* Real-world troubleshooting often requires repeatedly inspecting files.

### Password Found

```text
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

---

