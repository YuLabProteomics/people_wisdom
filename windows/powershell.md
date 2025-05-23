## What is PowerShell?

PowerShell is a tool you use in a **command-line window** to control your computer with text commands. It's made by Microsoft and is mainly used to **automate tasks**, especially on Windows.

Unlike the old Command Prompt, PowerShell is smarter — it doesn’t just read text; it works with **real data objects**, which makes it more powerful and easier to work with complex stuff.

---

## Why Use PowerShell?

* You can **automate boring tasks** (like renaming lots of files).
* You can **control your system** (start/stop programs, manage files, check settings).
* You can **write scripts** to do the same thing over and over without repeating yourself.

---

## What Makes It Different from Linux Terminal?

| PowerShell                | Linux Terminal (bash)                     |
| ------------------------- | ----------------------------------------- |
| Uses data objects         | Uses plain text                           |
| Works great on Windows    | Works great on Linux                      |
| Uses `Verb-Noun` commands | Uses short commands like `ls`, `cd`, `rm` |
| Script file: `.ps1`       | Script file: `.sh`                        |

---

## Example

```powershell
# Show all programs that are running
Get-Process

# Find files larger than 10MB
Get-ChildItem -Recurse | Where-Object { $_.Length -gt 10MB }
```

---

## In One Sentence

PowerShell is like the **super version of Command Prompt** — it helps you tell your computer what to do, quickly and automatically.

---

# PowerShell vs Windows Terminal — What's the Difference?

## TL;DR

| Feature                         | PowerShell                                           | Windows Terminal                                 |
|---------------------------------|------------------------------------------------------|--------------------------------------------------|
| What is it?                    | A command-line shell and scripting language          | A terminal emulator for command-line tools       |
| What does it do?               | Runs commands like `Get-Process`, scripts (.ps1)     | Hosts PowerShell, CMD, WSL, Git Bash, etc.       |
| Is it standalone?              | Yes                                                 | No (used to run other shells)                    |
| Use case                       | Scripting, system administration, automation         | Managing multiple command-line environments       |

---

## Key Concept

PowerShell is the tool.  
Windows Terminal is the container that can host many tools.

Windows Terminal can run PowerShell, CMD, WSL, and more — each in its own tab.

---

## Example

```powershell
Get-Process
---

