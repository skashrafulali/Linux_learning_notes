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

# 41. ps

View running processes.

```bash
ps
```

More useful:

```bash
ps aux
```

Example Output:

```text
USER      PID   %CPU   COMMAND
root      1     0.1    systemd
ashraful  2500  0.5    firefox
```

---

# 42. top

Real-time process monitor.

```bash
top
```

Useful for:

* CPU usage
* Memory usage
* Running processes

Exit:

```bash
q
```

---

# 43. htop

Better version of top.

Install:

```bash
sudo apt install htop
```

Run:

```bash
htop
```

Exit:

```bash
q
```

---

# 44. kill

Terminate a process.

Find PID:

```bash
ps aux
```

Kill process:

```bash
kill 1234
```

Example:

```bash
kill 2500
```

---

# 45. kill -9

Force kill.

```bash
kill -9 2500
```

Use only if normal kill fails.

---

## Network Commands

---

# 46. ping

Check network connectivity.

```bash
ping google.com
```

Send only 4 packets:

```bash
ping -c 4 google.com
```

---

# 47. ip a

Show network interfaces.

```bash
ip a
```

Useful to find:

* IP Address
* Interface Name
* Network Status

---

# 48. ip route

Show routing table.

```bash
ip route
```

Example:

```text
default via 192.168.0.1
```

This is usually your router.

---

# 49. ss

Show active connections.

```bash
ss -tuln
```

Meaning:

```text
t = TCP
u = UDP
l = Listening
n = Numeric
```

Very important for cybersecurity.

---

# 50. netstat

Older but still useful.

Install:

```bash
sudo apt install net-tools
```

Run:

```bash
netstat -tuln
```

---

## Downloading Files

---

# 51. wget

Download files.

```bash
wget https://example.com/file.zip
```

Save with custom name:

```bash
wget -O notes.zip https://example.com/file.zip
```

---

# 52. curl

Download or interact with websites/APIs.

View webpage source:

```bash
curl https://example.com
```

Download file:

```bash
curl -O https://example.com/file.zip
```

Cybersecurity professionals use curl constantly.

---

## Archives

---

# 53. tar

Create archive.

```bash
tar -cvf backup.tar folder/
```

Extract:

```bash
tar -xvf backup.tar
```

---

# 54. gzip

Compress file.

```bash
gzip notes.txt
```

Creates:

```text
notes.txt.gz
```

---

# 55. unzip

Extract zip files.

```bash
unzip file.zip
```

---

# 56. zip

Create zip archive.

```bash
zip files.zip file1.txt file2.txt
```

---

## System Services

---

# 57. systemctl

Manage services.

Check SSH:

```bash
systemctl status ssh
```

Start SSH:

```bash
sudo systemctl start ssh
```

Enable at boot:

```bash
sudo systemctl enable ssh
```

---

# 58. service

Older service manager.

```bash
service ssh status
```

Restart:

```bash
sudo service ssh restart
```

---

## Terminal Productivity

---

# 59. alias

Create shortcuts.

Example:

```bash
alias ll='ls -la'
```

Now:

```bash
ll
```

works like:

```bash
ls -la
```

---

# 60. history | grep

Search command history.

```bash
history | grep apt
```

Example Output:

```text
23 sudo apt update
24 sudo apt upgrade
```

Very useful when you forget previous commands.

---

# Practice Lab

Open Terminal and perform:

```bash
ip a

ping -c 4 google.com

ss -tuln

curl https://example.com

wget https://example.com

ps aux

top

history | grep sudo

alias ll='ls -la'

ll
```

---

# Cybersecurity Commands Learned

Process Monitoring:

* ps
* top
* htop
* kill

Networking:

* ping
* ip
* ss
* netstat

Downloads:

* curl
* wget

Archives:

* tar
* zip
* unzip
* gzip

Services:

* systemctl
* service

Productivity:

* alias
* history | grep


---
