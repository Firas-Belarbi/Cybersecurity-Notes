
# Cybersecurity-Notes-Metasploit.md
# (Technical notes focusing on Metasploit tool usage, commands, and explanations)

# Metasploit Framework: Technical Notes and Commands

**Author:** Firas Belarbi  
**Source:** TryHackMe Metasploit room  
**Date:** (Add date)

---

## Overview

Metasploit Framework is an open-source penetration testing platform used to develop and execute exploit code against remote targets. It has two main editions:

- **Metasploit Pro:** A commercial GUI-based version with advanced features.  
- **Metasploit Framework:** Open-source CLI-based version commonly used by security professionals.

This note covers essential commands, module types, payloads, and practical usage learned from TryHackMe exercises.

---

## Core Components

- **msfconsole:** Main interface for using Metasploit modules interactively.  
- **Modules:** Exploit, Auxiliary, Post-exploitation, Payloads, Encoders, NOPs, and Evasion modules.  
- **msfvenom:** Standalone tool for creating payloads.

---

## Common Commands and Usage

| Command                | Description                                                                                  |
|------------------------|----------------------------------------------------------------------------------------------|
| `msfconsole`           | Starts the Metasploit Framework console.                                                    |
| `search <keyword>`     | Searches for modules matching the keyword.                                                  |
| `use <module_path>`    | Selects a module for use (e.g., exploit/windows/smb/ms17_010_eternalblue).                   |
| `show options`         | Displays configurable options for the selected module.                                      |
| `set <option> <value>` | Sets a variable for the current module context (e.g., `set RHOSTS 10.10.165.39`).          |
| `setg <option> <value>`| Sets a global variable affecting all modules (e.g., `setg RHOSTS 10.10.165.39`).            |
| `unset <option>`       | Clears a set option.                                                                         |
| `info`                 | Displays detailed information about the selected module.                                    |
| `exploit` or `run`     | Launches the selected exploit or auxiliary module.                                          |
| `sessions`             | Lists active sessions.                                                                       |
| `sessions -i <id>`     | Interacts with a specific active session.                                                   |
| `background`           | Sends the current session to the background.                                                |
| `exit`                 | Exits msfconsole.                                                                            |

---

## Module Types

- **Exploit:** Code that takes advantage of vulnerabilities to gain access.  
- **Auxiliary:** Tools such as scanners or fuzzers that do not create sessions.  
- **Post:** Modules that run after a session is established for further interaction.  
- **Payloads:** Code executed on the target after exploitation (e.g., Meterpreter shell).

---

## Practical Examples

- **Setting target IP globally:**  
setg RHOSTS 10.10.19.23

markdown
Copier le code
This sets the remote host IP globally, so all modules use it unless overridden.

- **Clearing the payload option:**  
unset PAYLOAD

css
Copier le code
Removes the payload setting, allowing you to set a different one.

- **Starting an exploit:**  
exploit

yaml
Copier le code
Initiates the attack based on configured options.

---

## Additional Notes

- The `msfconsole` prompt changes to reflect the current module context, helping keep track of the active module.  
- Global variables (setg) persist across module changes, useful for consistent target settings.  
- Running Linux commands within msfconsole is possible with `exec <command>`, which helps in quick reconnaissance.  
- The AttackBox environment on TryHackMe provides a sandbox to safely practice these commands and workflows.

---
