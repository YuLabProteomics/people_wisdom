## Basic PowerShell Command Line Cheat Sheet

### Navigation

```powershell
pwd                   # Show current directory
cd <path>             # Change directory
ls                    # List files (alias for Get-ChildItem)
```

---

### File & Folder Operations

```powershell
mkdir <folder>        # Create a new folder
New-Item <file>       # Create a new file
rm <item>             # Delete a file or folder
cp <source> <dest>    # Copy file or folder
mv <source> <dest>    # Move or rename file or folder
```

---

### Viewing Content

```powershell
Get-Content <file>    # Display content of a file
```

---

### Process Management

```powershell
Get-Process                   # List running processes
Stop-Process -Name <name>     # Stop a process by name
```

---

### System Info & Help

```powershell
Get-Date               # Show current date and time
Get-Command            # List all available commands
Get-Help <command>     # Show help info for a command
```

---

### Variables and Output

```powershell
$name = "Zixuan"       # Create a variable
Write-Output $name     # Print the variable
```

---

### Filtering with Pipelines

```powershell
# Show only running services
Get-Service | Where-Object { $_.Status -eq "Running" }
```

---

### Running Scripts

```powershell
.\script.ps1           # Run a PowerShell script

# If blocked, allow script execution
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

---

### Method: Open PowerShell Quickly with Shortcuts

| Action                                             | Shortcut                                 |
|----------------------------------------------------|------------------------------------------|
| Open PowerShell (Standard Privileges)              | `Win + R` → type `powershell` → `Enter`  |
| Open PowerShell (Administrator Privileges)         | `Win + X` → then press `A`               |
| Quickly Open Terminal Menu (Includes PowerShell)   | `Win + X` → use arrow keys to select `Windows PowerShell` |

---
