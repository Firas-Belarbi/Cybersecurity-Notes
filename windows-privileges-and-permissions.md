# Windows Privileges and Permissions Overview

## 1. Local Accounts vs Domain Accounts
- **Local Account**: Exists only on one machine.
- **Domain Account**: Managed centrally by Active Directory.
- Authentication is controlled by the Domain Controller.

---

## 2. Privilege Levels
### Standard User
- Limited control over system-wide settings.
- Can run applications.
- Cannot modify system files.

### Local Administrator
- Full control over the local machine.
- Can install software.
- Manage local users and services.

### Domain Administrator
- Highest level of privilege in a Windows domain.
- Can control any workstation, server, or user object.
- Full access to Group Policies, OUs, and domain configuration.

---

## 3. Active Directory Permission Delegation
Delegation allows granting limited administrative rights without giving full domain admin access.

Example:
Delegate Control → Reset user passwords

yaml
Copier le code
Used to allow non-admin users (e.g., Phillip) to:
- Reset passwords for specific OUs
- Manage users inside a defined scope

---

## 4. Common Permission Types
- **Reset Password**
- **Read / Write user attributes**
- **Create and delete child objects**
- **Full Control**

Delegation should always follow the principle of **Least Privilege**.

---

## 5. Remote Access Methods
### RDP (mstsc)
- Standard method to connect to Windows machines.
- Creates a new, isolated session.
- Useful when the main session is occupied (e.g., admin logged in).

### SSH
- Used mainly for Linux and some Windows configurations.

---

## 6. Session Isolation Issue (Relevant to AD Case Study)
Windows does not reliably allow two different interactive sessions on the *same* browser-based VM.

A separate host (e.g., physical machine through RDP) avoids:
- Session overlap
- Credential conflicts
- Cached authentication issues

---

## 7. Relevance to SOC / IT Roles
Understanding permissions is mandatory for:
- Account troubleshooting  
- Access issues  
- Password resets  
- Privilege escalation detection  
- Incident response where credentials are involved
