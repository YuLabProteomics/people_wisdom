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


# **Micromamba Installation Guide (Linux Intel (x86_64))**

Follow these steps to install and configure **Micromamba** on your Linux system.

---

## **Step 1: Download the Latest Version**
Navigate to your `Downloads` folder and download the latest Micromamba binary:
```bash
cd ~/Downloads
curl -Ls https://micro.mamba.pm/api/micromamba/linux-64/latest | tar -xvj bin/micromamba
````

---

## **Step 2: Move the Binary and Set Permissions**

Move `micromamba` to `~/.local/bin` and set execute permissions:

```bash
mkdir -p ~/.local/bin
mv ~/Downloads/bin/micromamba ~/.local/bin/
chmod +x ~/.local/bin/micromamba
```

---

## **Step 3: Add to PATH**

Ensure Micromamba is added to your PATH in `.bashrc`:

```bash
if ! grep -q 'export PATH="$HOME/.local/bin:$PATH"' ~/.bashrc; then
    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
fi
```

---

## **Step 4: Initialize Micromamba Shell**

Initialize the shell to enable `micromamba` commands:

```bash
micromamba shell init -s bash -r ~/.local/micromamba
```

---

## **Step 5: Update Old Paths (if any)**

If there are old paths in `.bashrc`, replace them with the new path:

```bash
sed -i 's|/home/zixuan_ye/Downloads/bin/micromamba|/home/zixuan_ye/.local/bin/micromamba|g' ~/.bashrc
```

---

## **Step 6: Reload Shell Configuration**

Apply the changes by reloading your shell:

```bash
source ~/.bashrc
```

---

## **Step 7: Run Shell Hook**

Enable Micromamba shell functionalities:

```bash
eval "$(micromamba shell hook --shell bash)"
```

---

## **Step 8: Verify Installation**

Check the Micromamba version to confirm installation:

```bash
micromamba --version
```

---

## **Optional: Create and Activate a Test Environment**

Test the installation by creating and activating a new environment:

```bash
micromamba create -n test_env python=3.10 -y
micromamba activate test_env
```

To deactivate the environment, simply run:

```bash
micromamba deactivate
```

---


