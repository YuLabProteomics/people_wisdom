# Why Use Mamba or Micromamba Instead of Conda for Research?

## **Advantages Comparison**
| Feature           | conda           | mamba               | micromamba            |
|------------------|-----------------|---------------------|-----------------------|
| Speed             | Slow            | Fast                | Faster                |
| Dependency Solving | Sometimes fails | More stable         | More stable           |
| Memory Usage      | High            | Medium              | Low                   |
| Installation Complexity | Requires Python  | Needs `conda` environment | Standalone, no Python dependency |
| Ideal Environment | Local development, lab | HPC, Cloud        | Docker, HPC           |

## **Licensing Issues**
- `conda` is owned by Anaconda, Inc., and **requires a commercial license** for enterprise use.
- `mamba` and `micromamba` are developed by the Mamba Community under **BSD 3-Clause License**, fully open-source and **no commercial restrictions**.
- To completely avoid licensing issues:
  1. Switch to `conda-forge`:
     ```bash
     micromamba config set channels conda-forge
     micromamba config set channel_priority strict
     ```
  2. Avoid using the `defaults` channel (Anaconda's official mirror).

---

# The Tutorial of Downloading Micromamba

# Official Website
https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html

**Unitil 05/13/2025, the latest version of micromamba is 2.1.1.**

---

# What is `conda-forge`?

`conda-forge` is a **community-driven repository of Conda packages**. It is an alternative to the default `conda` channel, managed by contributors worldwide, who maintain and update software packages for scientific computing, data science, machine learning, bioinformatics, and more.


## Why Use `conda-forge` with Micromamba?

When you use `micromamba` to install packages, it looks for these packages in different "channels." The default channel is `defaults`, maintained by Anaconda, Inc., but it is often slower to update and has fewer specialized packages.

### Key Benefits of `conda-forge`:
1. **Faster Updates**  
   - Packages on `conda-forge` are updated more frequently than the default `conda` channel.
   - You get the latest versions of packages, often within days of release.

2. **Wider Variety of Packages**  
   - Many specialized scientific and bioinformatics tools are only available on `conda-forge`.
   - Examples include:
     - `snakemake`: Workflow management
     - `pyro-ppl`: Probabilistic programming in Python
     - `scanpy`: Single-cell RNA analysis
     - `jupyterlab`: Latest version for interactive computing

3. **Better Compatibility**  
   - `conda-forge` maintains tighter version control, which means dependencies are resolved more smoothly.
   - Cross-platform compatibility is better, supporting Linux, macOS, and Windows without additional configuration.

4. **Strict Dependency Resolution**  
   - When you configure `micromamba` to prioritize `conda-forge`, it uses **strict dependency resolution**.  
   - This avoids version conflicts and ensures that package versions are fully compatible.

## How to Configure `conda-forge` in Micromamba?

- To make `conda-forge` the **default source**, you can configure it once:

```bash
micromamba config append channels conda-forge
micromamba config set channel_priority strict
```
- This configuration makes sure every time you install packages, they are fetched from `conda-forge` first.

---

# Installation script (for Linux Intel (x86_64))

```bash

#!/bin/bash

# =====================
# Micromamba Setup Script
# =====================

# Paths
WORKSTATION_PATH="$HOME/.local/share/mamba/envs"
DEFAULT_PATH="$HOME/.local/micromamba/envs"
MICROMAMBA_BIN="$HOME/.local/bin/micromamba"

# =====================
# Step 1: Clean up old installations
# =====================
rm -rf ~/.local/bin/micromamba
rm -rf ~/Downloads/bin/micromamba
rm -rf ~/.local/micromamba
rm -rf ~/.local/share/mamba
sed -i '/# >>> mamba initialize >>>/,/# <<< mamba initialize <<</d' ~/.bashrc
sed -i '/micromamba/d' ~/.bashrc
sed -i '/MAMBA_ROOT_PREFIX/d' ~/.bashrc
sed -i '/MAMBA_EXE/d' ~/.bashrc

# =====================
# Step 2: Download Micromamba
# =====================
cd ~/Downloads                       
curl -Ls https://micro.mamba.pm/api/micromamba/linux-64/latest | tar -xvj bin/micromamba
mkdir -p ~/.local/bin
mv ~/Downloads/bin/micromamba ~/.local/bin/
chmod +x ~/.local/bin/micromamba

# =====================
# Step 3: Add to PATH if not already
# =====================
if ! grep -q 'export PATH="$HOME/.local/bin:$PATH"' ~/.bashrc; then
    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
fi

# =====================
# Step 4: Detect Workstation or Local Environment
# =====================
if [ -d "$WORKSTATION_PATH" ]; then
    export MAMBA_ROOT_PREFIX="$HOME/.local/share/mamba"
    echo 'export MAMBA_ROOT_PREFIX="$HOME/.local/share/mamba"' >> ~/.bashrc
    micromamba config prepend envs_dirs ~/.local/share/mamba/envs
else
    export MAMBA_ROOT_PREFIX="$HOME/.local/micromamba"
    echo 'export MAMBA_ROOT_PREFIX="$HOME/.local/micromamba"' >> ~/.bashrc
    micromamba config prepend envs_dirs ~/.local/micromamba/envs
fi

# =====================
# Step 5: Initialize Micromamba shell
# =====================
if ! grep -q 'micromamba shell hook' ~/.bashrc; then
    echo 'eval "$(micromamba shell hook --shell bash)"' >> ~/.bashrc
fi
source ~/.bashrc
hash -r

# =====================
# Step 6: Configure conda-forge
# =====================
micromamba config append channels conda-forge
micromamba config set channel_priority strict

# =====================
# Step 7: Create and activate Python 3.12 environment
# =====================
micromamba create -n test_env python=3.12 -y

# Activate environment
eval "$(micromamba shell hook --shell bash)"
micromamba activate test_env

# =====================
# Step 8: Test Installation
# =====================
echo "Testing Micromamba installation..."
if micromamba env list | grep -q "test_env"; then
    echo "test_env is successfully created."
else
    echo "test_env creation failed. Exiting..."
    exit 1
fi

if which python | grep -q "test_env"; then
    echo "Python is correctly installed in test_env."
    python --version
else
    echo "Python installation failed. Exiting..."
    exit 1
fi

# =====================
# Step 9: Final check
# =====================
echo "All installations and configurations are complete."
echo "To activate the environment, run:"
echo "    micromamba activate test_env"
echo "To deactivate, run:"
echo "    micromamba deactivate"

```

- In the section of downloading Micromamba, check the official website and choose the right curl according to the CPU architecture type.
- Method of Application:
1. Copy the script above and paste in the editor in the terminal.
```
nano setup_micromamba.sh
```
2. Grant execution authority.
```
chmod +x setup_micromamba.sh
```
3. Run
```
./setup_micromamba.sh
```
4. Output may look like:
```bash
test_env is successfully created.
Python is correctly installed in test_env.
Python 3.12.10
All installations and configurations are complete.
To activate the environment, run:
    micromamba activate test_env
To deactivate, run:
    micromamba deactivate
```

