
# Setting Up a Dedicated Windows User for SSH Access from Mac

## Why You Should Not Use Your Default Account (e.g., `pc`)

Using your main Windows account for SSH login is discouraged for several reasons:

| Reason              | Explanation |
|---------------------|-------------|
| Security            | Default accounts often have administrative privileges. If compromised via SSH, your entire system is exposed. |
| Clean Configuration | A dedicated user keeps `.ssh` files, permissions, and environment isolated from your main workflow. |
| Access Control      | It's easier to apply folder or privilege restrictions to a separate user. |
| Auditability        | Actions performed via SSH are clearly associated with the SSH user, not your personal account. |
| Industry Practice   | Following the principle of least privilege is standard in systems administration and DevOps. |

---

# Full Guide: Creating a Dedicated Windows User for SSH Login (Public Key Authentication from Mac)

This guide walks you through creating a new local Windows user and configuring SSH key-based login using PowerShell and macOS Terminal.

---

## Step 1: Open PowerShell as Administrator

- Press `Win`, search for "PowerShell"
- Right-click → "Run as administrator"

---

## Step 2: Create a New Local User

```powershell
net user cecilia Yezi2333! /add
````

* Replace `cecilia` with your desired username.
* Replace `Yezi2098!` with a strong password (must contain uppercase, lowercase, digit, and symbol).
* This creates a local standard user (non-admin).

To verify:

```powershell
net user
```

---

## Step 3: Create `.ssh` Folder and `authorized_keys` File

```powershell
New-Item -ItemType Directory -Path "C:\Users\cecilia\.ssh" -Force
notepad C:\Users\cecilia\.ssh\authorized_keys
```

Paste your Mac public key (output of `cat ~/.ssh/id_ed25519.pub`) into the file, save and close.

---

## Step 4: Set Correct File Permissions

```powershell
icacls "C:\Users\cecilia\.ssh\authorized_keys" /inheritance:r
icacls "C:\Users\cecilia\.ssh\authorized_keys" /grant:r "desktop-<MACHINE_NAME>\cecilia:F"
```

Replace `desktop-<MACHINE_NAME>` with the output of `whoami`, up to the backslash.

Example:

If `whoami` outputs:

```
desktop-8jq74oi\pc
```

Then use:

```powershell
icacls "C:\Users\cecilia\.ssh\authorized_keys" /grant:r "desktop-8jq74oi\cecilia:F"
```

---

## Step 5: Restart SSH Server

```powershell
Restart-Service sshd
```

If you haven't installed OpenSSH Server yet, run this first:

```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

---

## Step 6: SSH from Mac

From macOS terminal:

```bash
ssh cecilia@<windows-ip>
```

You can also add a shortcut in `~/.ssh/config`:

```bash
Host winbox
    HostName 192.168.1.123
    User cecilia
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

Then just use:

```bash
ssh winbox
```

---

## Final Notes

* You now have a dedicated user account for SSH access.
* You can safely restrict this user’s permissions further (e.g. limited folders).
* Avoid exposing your main Windows user (like `pc`) to SSH.

