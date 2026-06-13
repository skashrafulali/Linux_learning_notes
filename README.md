Linux Learning Notes

Introduction

This repository contains my Linux learning notes as I begin my cybersecurity journey.

Lets get started.

# 1. pwd (Print Working Directory)

Shows your current location in the filesystem.

```bash
pwd
```

Example Output:

```bash
/home/ashraful
```

---

2. ls (List Files and Directories)

Lists files and folders in the current directory.

```bash
ls
```

Example Output:

```bash
Documents Downloads Pictures
```

Useful Variants:

```bash
ls -l
```

Long listing format.

```bash
ls -a
```

Shows hidden files.

```bash
ls -la
```

Shows hidden files with detailed information.

---

3. cd (Change Directory)

Move between directories.

```bash
cd Documents
```

Moves into Documents folder.

Example:

```bash
/home/user
```

↓

```bash
cd Documents
```

↓

```bash
/home/user/Documents
```

Useful Variants:

```bash
cd ..
```

Go one folder back.

```bash
cd ~
```

Go to home directory.

```bash
cd /
```

Go to root directory.

```bash
cd
```

Also returns to home directory.

---

4. mkdir (Make Directory)

Create a new folder.

```bash
mkdir test
```

Creates:

```bash
test/
```

---

5. rmdir

Remove an empty directory.

```bash
rmdir test
```

---

6. touch

Create an empty file.

```bash
touch notes.txt
```

Creates:

```bash
notes.txt
```

---

7. cat

Display file contents.

```bash
cat notes.txt
```

Output:

```bash
Linux is awesome.
```

---

8. echo

Print text to terminal.

```bash
echo Hello Linux
```

Output:

```bash
Hello Linux
```

Write text into a file:

```bash
echo "Hello Linux" > notes.txt
```

---

9. clear

Clears the terminal screen.

```bash
clear
```

Shortcut:

```bash
Ctrl + L
```

---

10. whoami

Shows the current logged-in user.

```bash
whoami
```

Output:

```bash
ashraful
```

---

11. hostname

Displays system hostname.

```bash
hostname
```

Example:

```bash
kali
```

---

12. date

Shows current date and time.

```bash
date
```

Example Output:

```bash
Sat Jun 13 20:45:00 BST 2026
```

---

13. cal

Displays a calendar.

```bash
cal
```

Example:

```bash
June 2026
```

---

14. cp (Copy)

Copy files.

```bash
cp file.txt backup.txt
```

Creates:

```bash
backup.txt
```

---

15. mv (Move / Rename)

Rename file:

```bash
mv old.txt new.txt
```

Move file:

```bash
mv file.txt Documents/
```

---

16. rm (Remove)

Delete files.

```bash
rm file.txt
```

Delete directory and contents:

```bash
rm -r folder
```

⚠️ Be careful. Deleted files usually cannot be recovered.

---

17. find

Search for files.

```bash
find . -name notes.txt
```

Output:

```bash
./notes.txt
```

---

18. grep

Search text inside files.

```bash
grep Linux notes.txt
```

Output:

```bash
Linux is awesome
```

---

19. man (Manual)

Shows command documentation.

```bash
man ls
```

Exit manual:

```bash
q
```

---

20. history

Shows previously executed commands.

```bash
history
```

Example:

```bash
1 pwd
2 ls
3 cd Documents
4 mkdir test
```

---

