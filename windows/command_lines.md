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

### Finding the IP Address of Windows: Using Command Prompt (Recommended)

1. Press `Win + R` to open the **Run** dialog.

2. Type `cmd` and press **Enter** to open the **Command Prompt**.

3. In the Command Prompt window, type the following command and press **Enter**:

   ```bash
   ipconfig
   ```

4. Look for the following section (your network might be named differently):

   ```
   Wireless LAN adapter Wi-Fi:

      IPv4 Address. . . . . . . . . . . : 192.168.1.101
   ```

   The line labeled **"IPv4 Address"** shows your local IP address.

---

