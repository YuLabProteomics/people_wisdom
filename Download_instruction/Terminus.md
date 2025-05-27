# 🧙‍♂️ Terminus Guide: Overview, SSH Setup, and Comparison with MobaXterm

**Terminus** is a modern, cross-platform, open-source terminal emulator. It blends the power of traditional terminals with a sleek GUI, supporting **SSH, SFTP, tabs, splits, themes, and plugins** — like VS Code, but for terminals.

---

## 🚀 Key Features of Terminus

* 🖥️ **Tabbed and split panes** for multitasking
* 🔐 **Built-in SSH** client with private key authentication
* 📂 **Integrated SFTP** file manager with drag-and-drop support
* 🎨 **Customizable themes and fonts**, including ligature fonts like `Fira Code`
* 🔌 **Plugin system** with extensible functionality (e.g., command search, terminal snippets)
* 🌈 **Cross-platform**: Works on Windows, macOS, and Linux

---

## 🔗 How to Set Up an SSH Connection in Terminus

All you need are the following details:

| Field             | Example                   | Description                               |
| ----------------- | ------------------------- | ----------------------------------------- |
| **Hostname (IP)** | `146.189.164.183`         | IP address or domain of the remote server |
| **Username**      | `zixuan_ye`               | Your login username on the remote machine |
| **Private Key**   | `~/.ssh/id_ed25519_yulab` | Path to your SSH private key              |
| **Label**         | `Wanglab Server`          | A nickname to identify the connection     |

### ✅ Steps:

1. Open Terminus → Click `Hosts` on the sidebar
2. Click `+ NEW HOST`
3. Fill in the four fields above
4. Click **Save**
5. Click the new host entry to SSH in with one click!

---

## 🔁 Terminus vs MobaXterm – Side-by-Side Comparison

| Feature                  | **Terminus**                   | **MobaXterm**                                   |
| ------------------------ | ------------------------------ | ----------------------------------------------- |
| 🖥️ Interface aesthetics | 🎨 Modern, themeable           | 🧱 Functional, dated UI                         |
| 🔐 SSH support           | ✅ Strong (keys, agent, SFTP)   | ✅ Strong (auto SFTP popup)                      |
| 📂 SFTP file transfer    | ✅ Supported, clean UI          | ✅ Highly visual, user-friendly                  |
| 🧩 Plugin ecosystem      | ✅ VS Code-like plugins         | ❌ No plugin support                             |
| 🖼️ Customizability      | ✅ High (UI + config JSON)      | ⚠️ Limited customization                        |
| 🌍 Cross-platform        | ✅ Yes (Win/macOS/Linux)        | ❌ Windows only                                  |
| 🚀 Startup speed         | ✅ Fast and lightweight         | ⚠️ Slightly heavier load                        |
| 💰 Pricing               | 🆓 Free and open source        | 🆓 Free version has limits; Pro version is paid |
| 👥 Best for              | Devs, power users, researchers | Beginners, GUI-focused users                    |

---

## 🧠 Who Should Use Terminus?

* Researchers, developers, and engineers managing **multiple remote servers**
* Anyone who enjoys **customizable, modern terminal environments**
* Users looking for a **cleaner, faster alternative** to MobaXterm or PuTTY

---

## 🔚 Summary

> **Terminus = Beautiful UI + Efficient Workflow + Power Features.**
> It’s more lightweight and customizable than MobaXterm, and perfect for users who want a modern terminal with built-in SSH, SFTP, and plugin support.

Once configured, you can connect to remote servers with a single click and manage files visually, all in one terminal window.

