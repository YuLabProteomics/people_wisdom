# Git + SSH 快速操作（适用于 macOS）

---

## 1. 生成 SSH key（不要覆盖现有 key！）

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/id_ed25519_custom
```

按提示回车，或设置密码（passphrase），生成的 key 会是：

- 私钥：`~/.ssh/id_ed25519_custom`
- 公钥：`~/.ssh/id_ed25519_custom.pub`

### 什么是 ed25519？

`ed25519` 是一种现代、**更安全、更快**的椭圆曲线算法，比旧的 `rsa` 算法更推荐。它有：
- 更小的 key 文件
- 更高的安全性
- 更快的签名速度

GitHub 官方强烈建议使用 `ed25519`。

---

## 2. 添加 SSH key 到 GitHub

```bash
pbcopy < ~/.ssh/id_ed25519_custom.pub
```

然后打开：

👉 [https://github.com/settings/keys](https://github.com/settings/keys)

➜ 点击 **“New SSH key”**  
➜ Title 随便写，粘贴复制的内容 ➜ Save 🔐

---

## 3. 配置 `~/.ssh/config`（多 key 多账号神器）

```bash
nano ~/.ssh/config
```

加一段（如果没有就新建）：

```bash
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_yulab
  IdentitiesOnly yes
  AddKeysToAgent yes
  UseKeychain yes
```

然后运行一次：ssh-add --apple-use-keychain ~/.ssh/id_ed25519_yulab

保存退出：`Ctrl + X` ➜ `Y` ➜ `Enter`

---

## 4. 测试是否成功连接

```bash
ssh -T git@github.com
```

成功输出：

```bash
Hi your_username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## 5. 设置 GitHub 仓库 remote 为 SSH

```bash
git remote set-url origin git@github.com:your_username/your_repo.git
```

或者如果你用的是自定义 remote 名字（比如 `wisdom`）：

```bash
git remote set-url wisdom git@github.com:YuLabProteomics/people_wisdom.git
```

查看当前 remote：

```bash
git remote -v
```

---

## 6. 一次完整的 Git push 流程

```bash
git add .
git commit -m "your commit message"
git push -u origin main  # or whatever your branch is
```

无需输入用户名密码，全程 SSH 直连！

---

## 7. 建议添加 `.gitignore` 文件（例）

`.gitignore` 推荐内容：

```
__pycache__/
.ipynb_checkpoints/
*.pyc
.env
*.log
```

---

## Bonus：快捷命令备查

| 操作 | 命令 |
|------|------|
| 查看当前 remote 地址 | `git remote -v` |
| 查看当前 SSH key fingerprint | `ssh-add -l` |
| 列出所有 key | `ls ~/.ssh` |
| 查看最近 Git 提交 | `git log --oneline` |

---

