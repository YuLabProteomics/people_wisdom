# Git + SSH Quick Reference Guide (macOS)

## 1. Generate an SSH key (without overwriting existing keys)

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/id_ed25519_custom
```

Follow the prompts and press enter, or set a passphrase if desired. This will create:

- Private key: `~/.ssh/id_ed25519_custom`
- Public key: `~/.ssh/id_ed25519_custom.pub`

### What is ed25519?

`ed25519` is a modern, secure, and fast elliptic curve algorithm. Compared to the older `rsa`, it offers:
- Smaller key size
- Higher security
- Faster signing

It is the recommended algorithm by GitHub.

## 2. Add your SSH key to GitHub

```bash
pbcopy < ~/.ssh/id_ed25519_custom.pub
```

Then go to:

https://github.com/settings/keys

- Click "New SSH key"
- Give it a title
- Paste your copied public key
- Click Save

## 3. Configure `~/.ssh/config` (recommended for managing multiple keys/accounts)

```bash
nano ~/.ssh/config
```

Add the following block:

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_custom
  IdentitiesOnly yes
```

Save and exit: `Ctrl + X`, then `Y`, then `Enter`

## 4. Test your connection to GitHub

```bash
ssh -T git@github.com
```

Expected output:

```
Hi your_username! You've successfully authenticated, but GitHub does not provide shell access.
```

## 5. Change your GitHub repository remote URL to use SSH

```bash
git remote set-url origin git@github.com:your_username/your_repo.git
```

Or if you used a custom remote name (e.g., `wisdom`):

```bash
git remote set-url wisdom git@github.com:YuLabProteomics/people_wisdom.git
```

Check current remote:

```bash
git remote -v
```

## 6. Full Git push workflow

```bash
git add .
git commit -m "your commit message"
git push -u origin main  # replace with your branch if different
```

You will not be prompted for username or password—SSH will handle authentication.

## 7. Recommended `.gitignore` file

Example contents for a clean repository:

```
__pycache__/
.ipynb_checkpoints/
*.pyc
.env
*.log
```

## Additional useful commands

| Task | Command |
|------|---------|
| View current remotes | `git remote -v` |
| List loaded SSH keys | `ssh-add -l` |
| List all keys in `.ssh` | `ls ~/.ssh` |
| View recent Git commits | `git log --oneline` |

This reference helps streamline your Git workflow using SSH: secure, efficient, and password-free.
