# Practical Guide for Hybrid Windows + Linux (WSL) Development

This guide outlines best practices for proteomics-related development, analysis, Jupyter notebook usage, and data management using a Linux terminal (via WSL) on a Windows machine. It’s ideal for common bioinformatics and computational workflows such as Jupyter + Python + Snakemake.

---

## Why Use WSL? What’s the Point?

WSL (Windows Subsystem for Linux) is an official Microsoft solution that lets you run a native Linux environment within Windows. Many proteomics tools are Windows-based, but when it comes to software development and data processing, Linux is hands-down the better choice. For our group, a hybrid Windows + Linux setup is the way to go.

### Why WSL is better than just using Windows:

| Advantage                                     | Explanation                                                                                               |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Better support for research tools**         | Many bioinformatics tools (e.g., Snakemake, ProteoWizard CLI, Pyteomics) are natively developed for Linux |
| **No need for dual boot or reboot**           | Run Linux tools directly inside Windows—no need to reboot or use a VM                                     |
| **More powerful CLI & flexible package mgmt** | Linux terminals beat Windows CMD/Powershell for scripting and dev work                                    |
| **Remote/server-friendly & consistent**       | Linux-style paths and commands match HPC/cluster setups—code is portable                                  |
| **High performance**                          | WSL2 uses a native Linux kernel via virtual disk—much faster than Docker or Git Bash                      |
| **Access Windows files from Linux**           | `/mnt/c/...` gives direct access to Windows files for easy data transfer                                  |

---

## 1. Setting Up Your Environment

### Use WSL + Ubuntu

* Recommended: latest version of WSL + Ubuntu
* WSL setup: [https://ubuntu.com/desktop/wsl](https://ubuntu.com/desktop/wsl)
* Or just search **Ubuntu 24.04.1 LTS** in the Microsoft Store

---

## 2. Install and Use micromamba (Recommended over conda)

### Install micromamba (see separate notes for details)

Docs:
[https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html](https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html)

---

## 3. Recommended Notebook Workflow: Cursor + Detached Jupyter Server

### Run Jupyter in Linux (WSL), connect from Cursor

```bash
micromamba activate mldata_env
jupyter notebook --no-browser --port=8888
```

Copy the output link (like `http://localhost:8888/?token=xxxx`)
Then in **Cursor → Select Kernel → Enter an existing Jupyter Server**, paste it in.

---

## 4. Automate Jupyter Startup in WSL

### Recommended Setup (verified stable):

Add to your `~/.bashrc`:

```bash
# ~/.bashrc

# === Debug: confirm .bashrc is loading ===
echo "✅ .bashrc is running"

# Enable bash completion
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi

# Add local bin to PATH
export PATH="$HOME/bin:$PATH"

# === micromamba initialization ===
# !! This block is managed by 'micromamba shell init' !!
export MAMBA_EXE='/home/zixuan/bin/micromamba'
export MAMBA_ROOT_PREFIX='/home/zixuan/.local/share/mamba'
__mamba_setup="$("$MAMBA_EXE" shell hook --shell bash --root-prefix "$MAMBA_ROOT_PREFIX" 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__mamba_setup"
else
    alias micromamba="$MAMBA_EXE"  # fallback
fi
unset __mamba_setup
# === end micromamba initialize ===

# === Auto-start Jupyter notebook in WSL ===
if [[ "$WSL_DISTRO_NAME" ]]; then
    echo "📢 Detected WSL: $WSL_DISTRO_NAME"
    if ! pgrep -f "jupyter-notebook" > /dev/null; then
        echo "🚀 Launching Jupyter Notebook with mldata_env..."
        (micromamba activate mldata_env && nohup jupyter notebook --no-browser --port=8888 &)
    else
        echo "🔄 Jupyter is already running"
    fi
fi
```

This will automatically launch Jupyter and your `mldata_env` every time you open a WSL terminal—no more typing!

---

## 5. Windows ↔ Linux File Sharing Tips

### Key Rule: Avoid directly processing large files from `/mnt/c/...` in WSL

| Task                            | Recommended Way                                      |
| ------------------------------- | ---------------------------------------------------- |
| Project work (scripts, models)  | Store in `/home/zixuan/your_project`                 |
| Raw data (.csv, .mzML)          | Copy from Windows into Linux paths before processing |
| Copy files Win → Linux          | Use: `cp -r /mnt/c/... ~/your_path`                  |
| Access Windows Desktop from WSL | Path: `/mnt/c/Users/YourUsername/Desktop/`           |

---

## 6. Tips for Snakemake / DIA-NN / Proteomics Scripts

* Run Snakemake workflows on the Linux side for better performance
* Do `.raw` → `.mzML` conversion early, and store results in Linux
* If Windows generates large output, move to Linux and clean up after

---

## 7. Common Commands Cheat Sheet

```bash
# Activate your environment
micromamba activate mldata_env

# Launch Jupyter
jupyter notebook --no-browser --port=8888

# Check if copy worked
du -sh ~/01_mldata

# Copy files from Windows to Linux
cp -r /mnt/c/Users/cecilia/Desktop/transfer_test/01_mldata ~/01_mldata

# Check paths
ls /mnt/c/Users/
ls ~/01_mldata
```

---

## Recommended Toolkit

| Tool             | Purpose                                    |
| ---------------- | ------------------------------------------ |
| Cursor           | AI-powered code editing & Notebook support |
| micromamba       | Lightweight environment manager            |
| Jupyter Notebook | Compute backend, integrates with Cursor    |
| WSL2 + Ubuntu    | Robust Linux terminal and software support |


