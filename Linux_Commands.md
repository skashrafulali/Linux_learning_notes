Linux Learning Notes

Here you can cover basic Linux commands.Some of them may work in you windows pc but these are mainly focused to run on linux terminal.
Get ready with your Linux pc.
And confused the brain with texts.

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
Linux Learning Notes - Day 2 

---

21. nano

Simple terminal text editor.

Open a file:

```bash
nano notes.txt
```

Save:

```bash
Ctrl + O
```

Exit:

```bash
Ctrl + X
```

---

22. less

View large files page by page.

```bash
less notes.txt
```

Navigation:

```bash
Space  -> Next page
b      -> Previous page
q      -> Quit
```

---

23. head

Show first 10 lines of a file.

```bash
head notes.txt
```

Show first 5 lines:

```bash
head -5 notes.txt
```
---

24. tail

Show last 10 lines.

```bash
tail notes.txt
```

Show last 20 lines:

```bash
tail -20 notes.txt
```

Monitor logs in real time:

```bash
tail -f logfile.log
```

---

25. wc (Word Count)

Count lines, words, and characters.

```bash
wc notes.txt
```

Example Output:

```bash
10 50 300 notes.txt
```

Meaning:

```text
10 lines
50 words
300 characters
```

---

26. sort

Sort lines alphabetically.

```bash
sort names.txt
```

Example:

Before:

```text
John
Alice
Bob
```

After:

```text
Alice
Bob
John
```

---

27. uniq

Remove duplicate lines.

```bash
uniq names.txt
```

Usually combined with sort:

```bash
sort names.txt | uniq
```

---

28. chmod

Change file permissions.

Current permissions:

```bash
ls -l
```

Example:

```text
-rw-r--r--
```

Make file executable:

```bash
chmod +x script.sh
```

Give everyone full permission:

```bash
chmod 777 file.txt
```

⚠️ Avoid 777 unless necessary.

---

29. chown

Change file owner.

```bash
sudo chown user file.txt
```

Example:

```bash
sudo chown ashraful notes.txt
```

---

30. sudo

Run commands as administrator.

```bash
sudo apt update
```

You may be asked for your password.

---

31. apt update

Update package lists.

```bash
sudo apt update
```

Does NOT install updates.

It only refreshes available package information.

---

32. apt upgrade

Install available updates.

```bash
sudo apt upgrade
```

Update everything automatically:

```bash
sudo apt upgrade -y
```

---

33. apt install

Install software.

Example:

```bash
sudo apt install nmap
```

Install multiple packages:

```bash
sudo apt install nmap net-tools
```

---

34. apt remove

Remove software.

```bash
sudo apt remove nmap
```

Remove configuration files too:

```bash
sudo apt purge nmap
```

---

35. which

Find where a command is located.

```bash
which python3
```

Example Output:

```bash
/usr/bin/python3
```

---

36. locate

Find files quickly.

```bash
locate notes.txt
```

May require database update first:

```bash
sudo updatedb
```

---

37. id

Show user information.

```bash
id
```

Example Output:

```bash
uid=1000(ashraful)
gid=1000(ashraful)
groups=1000(ashraful)
```

---

38. passwd

Change your password.

```bash
passwd
```

Change another user's password:

```bash
sudo passwd username
```

---

39. uname

Display system information.

```bash
uname
```

Detailed information:

```bash
uname -a
```

Example Output:

```text
Linux kali 6.12.0 x86_64 GNU/Linux
```

---

40. df

Show disk usage.

```bash
df
```

Human-readable format:

```bash
df -h
```

Example Output:

```text
Filesystem Size Used Avail Use%
100G       50G   50G  50%
```

---
