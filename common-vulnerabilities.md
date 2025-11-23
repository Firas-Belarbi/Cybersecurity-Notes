# Common Web & Network Vulnerabilities

## 1. SQL Injection (SQLi)
Occurs when user input is inserted directly into an SQL query.
- Allows attackers to read databases
- Extract usernames/passwords
- Login as admin
- Read/write files on server

## 2. Cross-Site Scripting (XSS)
Malicious script injected into a website.
- Steals cookies
- Hijacks accounts
- Injects malware
- Redirects users

Types:
- Reflected XSS
- Stored XSS

## 3. Local File Inclusion (LFI)
Allows attacker to read files from the server.
- Read /etc/passwd (Linux users)
- Access configuration files
- Sometimes leads to remote code execution

## 4. Remote File Inclusion (RFI)
Allows attacker to load a file from remote server.
- Leads to complete compromise

## 5. Command Injection
Attacker injects OS commands.
- Execute arbitrary commands on the server
- Gain shell access

## 6. Directory Traversal
Example: `../../../etc/passwd`
- Read sensitive files
- Bypass restrictions

## 7. Weak Authentication
- Default passwords
- Weak hashing (MD5)
- No MFA
- Poor session management

## 8. Insecure HTTP (No HTTPS)
- MITM attacks possible
- Credentials exposed
- Traffic easily sniffed

## 9. Misconfigured Servers
- Open ports
- Outdated software
- Debug mode enabled
- Sensitive files exposed

## 10. ARP Poisoning / MITM
- Attacker positions himself between devices
- Sniffs traffic
- Intercepts credentials and cookies
- Modifies pages in real time
