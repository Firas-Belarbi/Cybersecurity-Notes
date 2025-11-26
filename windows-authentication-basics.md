# Windows Authentication Basics

This document provides a technical overview of how authentication works in Windows environments, including both standalone machines and domain-joined systems.

---

## 1. Local Authentication
When logging into a standalone Windows machine:
- Credentials are validated against the local Security Account Manager (SAM)
- Password hashes are stored locally
- No domain controller is involved

Common characteristics:
- Only local accounts can authenticate
- Limited scalability
- Used for single-machine setups

---

## 2. Domain Authentication
When a machine is joined to a Windows domain:
- Authentication is handled by a Domain Controller (DC)
- The DC validates credentials stored within Active Directory
- User accounts become global across multiple machines

Benefits:
- Centralized identity management
- Group Policy support
- Delegated permissions
- Single Sign-On (SSO)

---

## 3. NTLM Authentication
NTLM is an older authentication protocol still supported for compatibility.

Key points:
- Challenge-response mechanism
- Does not require a timestamp
- Susceptible to replay attacks
- Used when:
  - Kerberos is not available
  - Machine is offline
  - Connecting to older systems

---

## 4. Kerberos Authentication
Kerberos is the default and preferred authentication protocol in modern AD environments.

Flow:
1. User requests a Ticket Granting Ticket (TGT)
2. DC issues the TGT
3. User requests a Service Ticket (TGS)
4. DC issues the TGS
5. User presents the TGS to access a service

Advantages:
- Mutual authentication
- Strong encryption
- Reduced authentication traffic

---

## 5. Credential Caching and Local Logon
When a domain user logs in:
- Windows caches hashed credentials locally
- Allows offline logon when the DC is unreachable

Important points:
- Cached logons do not validate with the DC
- Only a limited number of cached entries are stored

---

## 6. Session Isolation
Windows creates isolated interactive logon sessions.

Examples:
- Browser-based VM sessions in cloud labs
- RDP sessions (Remote Desktop)
- Local interactive sessions

Problems may occur when:
- Attempting multiple logins on the same host
- Conflicting credential cache
- Incorrectly merged interactive sessions

This was directly relevant to the AD troubleshooting case where the browser-based VM’s session prevented proper login as a different domain user.

---

## 7. Administrative Relevance
Understanding Windows authentication is critical for:

- Troubleshooting failed logons  
- Investigating domain access issues  
- Detecting credential misuse  
- Responding to authentication-related incidents  
- Diagnosing delegation or permission failures  

---

## 8. Summary
Windows authentication involves multiple layers:
- Local authentication (SAM)
- Domain-based authentication (Kerberos or NTLM)
- Session isolation
- Cached credentials

A solid understanding of these components is essential for SOC analysts, system administrators, and penetration testers.
