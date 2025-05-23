
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

## Step-by-Step Guide: Creating a Separate Windows User for SSH

### 1. Open PowerShell as Administrator

- Press `Win`, type `PowerShell`
- Right-click the icon and choose "Run as administrator"

### 2. Create a new user (e.g., `cecilia`)

```powershell
net user cecilia Yezi2098! /add
````

Note: The password must meet Windows complexity requirements (mixed case, digits, and a symbol).

---

## Configure SSH Access for the New User

### 3. Create the `.ssh` folder and `authorized_keys` file

```powershell
New-Item -ItemType Directory -Path "C:\Users\cecilia\.ssh" -Force
notepad C:\Users\cecilia\.ssh\authorized_keys
```

Then paste your Mac public key into this file. You can obtain it on your Mac using:

```bash
cat ~/.ssh/id_ed25519.pub
```

Save and close the file.

---

### 4. Set Correct Permissions on the Key File

```powershell
icacls "C:\Users\cecilia\.ssh\authorized_keys" /inheritance:r
icacls "C:\Users\cecilia\.ssh\authorized_keys" /grant:r "desktop-<MACHINENAME>\cecilia:F"
```

Replace `<MACHINENAME>` with the actual result of `whoami`, before the backslash.

---

### 5. Restart the SSH Service

```powershell
Restart-Service sshd
```

---

## Connecting from Mac

On your Mac, connect using:

```bash
ssh cecilia@<windows-ip>
```

Or define a shortcut in your `~/.ssh/config`:

```bash
Host winpc
    HostName <windows-ip>
    User cecilia
    IdentityFile ~/.ssh/id_ed25519
    IdentitiesOnly yes
```

Then connect using:

```bash
ssh winpc
```

---

## Final Notes

This approach ensures a cleaner, safer, and more maintainable SSH setup, particularly useful when sharing access, auditing activity, or running isolated workflows.

