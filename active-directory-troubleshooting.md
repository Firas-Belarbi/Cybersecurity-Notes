# Active Directory Troubleshooting Case Study

This document describes a real troubleshooting scenario performed in a TryHackMe Active Directory lab.  
The objective was to apply theoretical knowledge from CompTIA A+ (Troubleshooting Theory) to a practical domain environment.

---

## 1. Task Overview

The original lab required completing the following steps:

1. Log in as the domain administrator.
2. Remove an outdated Organizational Unit (OU).
3. Rebuild the domain structure based on a provided organizational diagram.
4. Delegate permissions for user "Phillip" to reset passwords in the Sales OU (where "Sophie" is located).
5. Log in as Phillip.
6. Reset Sophie's password via remote access.
7. Log in as Sophie to verify the password change.

---

## 2. Active Directory Configuration

After logging in as the domain administrator:

- Opened **Active Directory Users and Computers (ADUC)**.
- Enabled **Advanced Features** to allow modification of protected OUs.
- Removed the deprecated OU.
- Created new OUs as specified in the organizational diagram.
- Assigned users to their respective departments.
- Delegated the **Reset Password** permission to Phillip for the Sales OU using:
Delegate Control → Reset user passwords and force password change at next logon

yaml
Copier le code

At this stage, the AD structure and permission delegation were completed successfully.

---

## 3. Problem: Unable to Log In as Phillip

When attempting to log in as Phillip using the browser-based virtual machine:

- The system repeatedly returned an "incorrect password" error.
- The password was verified to be correct.
- Multiple retries, VM restarts, and network adjustments did not resolve the issue.

This indicated that the problem was not credential-related.

---

## 4. Additional Attempts

### Attempt 1: Using Linux and OpenVPN
- Connected to TryHackMe via OpenVPN.
- Attempted accessing the AD host from a Linux browser session.
- Network performance was unstable; remote access did not load correctly.
- Using a secondary VPN layer did not improve connectivity.

This approach was not viable due to performance limitations.

---

## 5. Root Cause Analysis

After eliminating several possibilities, the likely cause became clear:

The login attempt was being made from the *same machine/session* already authenticated as the domain administrator.  
Active Directory does not reliably handle multiple simultaneous interactive logins with different users from the same host in this context.

Conclusion:  
A separate logical host was required to perform the login as Phillip.

---

## 6. Final Solution (Working Method)

The working solution was to use the physical Windows machine to connect via Remote Desktop.

Steps:

1. Kept the administrator session running in the TryHackMe browser VM.
2. On the local Windows host:
 - Opened Remote Desktop Connection using:
   ```
   Win + R → mstsc
   ```
 - Entered the target machine's IP address.
 - Logged in using Phillip’s credentials.
3. After successful login:
 - Accessed the remote machine.
 - Performed the required password reset for Sophie.
4. Logged out and then logged in as Sophie to verify the password reset.

This method worked because it created a separate, clean session independent from the administrator login.

---

## 7. Alignment with CompTIA A+ Troubleshooting Theory

This scenario applied all seven steps of the CompTIA troubleshooting model:

1. **Identify the problem**  
 Login failures despite correct credentials.
2. **Establish a theory of probable cause**  
 Session conflict rather than incorrect password.
3. **Test the theory**  
 Linux + VPN attempts, multiple environments.
4. **Establish a plan of action**  
 Use a separate Windows host for authentication.
5. **Implement the solution**  
 Remote Desktop via `mstsc`.
6. **Verify full system functionality**  
 Password reset + successful login as Sophie.
7. **Document findings**  
 This file serves as the complete documentation.

---

## 8. Summary

This case demonstrated:

- Active Directory OU configuration and delegation.
- Remote authentication troubleshooting.
- Logical isolation of sessions.
- Practical application of troubleshooting frameworks.
- Experience with RDP (`mstsc`), ADUC, and VPN-based lab environments.
