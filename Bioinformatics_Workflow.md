# Modern Bioinformatics Workflow Setup 

## Purpose

This guideline is designed for researchers who want to analyze biological data efficiently and reproducibly using their personal Windows machines. It provides a clear and sustainable way to set up a computational workflow for proteomics or other omics data using **WSL (Windows Subsystem for Linux)**, **Micromamba**, and **Snakemake**.

---

## Why This Setup?

| Feature                 | Benefit                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **WSL + Ubuntu**        | Brings a real Linux environment to your Windows laptop. Compatible with most bioinformatics tools without needing a separate Linux machine. |
| **Micromamba**          | Lightweight and fast environment manager (like Conda but better). Perfect for isolating Python environments.                                |
| **Snakemake**           | A powerful workflow system to organize multi-step analysis and avoid repeating steps. Fully automatable and reproducible.                   |
| **Soft links**          | Save storage space and avoid duplicating large datasets.                                                                                    |
| **One-command startup** | You can start your entire project with one terminal command: open the environment, project folder, and editor.                              |

---

## Step-by-Step Setup

### 1. Enable WSL & Install Ubuntu

* Open PowerShell (Admin):

```powershell
wsl --install -d Ubuntu
```

* Restart when prompted.

### 2. Install Micromamba

In Ubuntu terminal:

```bash
mkdir -p ~/micromamba/bin
curl -Ls https://micro.mamba.pm/api/micromamba/linux-64/latest -o ~/micromamba/bin/micromamba
chmod +x ~/micromamba/bin/micromamba
```

### 3. Add Micromamba to Shell

Add to `~/.bashrc`:

```bash
export MAMBA_EXE="$HOME/micromamba/bin/micromamba"
export MAMBA_ROOT_PREFIX="$HOME/micromamba"
eval "$(micromamba shell hook --shell bash)"
```

Then reload:

```bash
source ~/.bashrc
```

### 4. Create the Python Environment

Save this as `create_env.sh`:

```bash
#!/bin/bash
set -e

env_name="pdata_env"
python_version="3.12"

export MAMBA_EXE="$HOME/.local/bin/micromamba"
export MAMBA_ROOT_PREFIX="$HOME/micromamba"
eval "$($MAMBA_EXE shell hook --shell bash)"

if ! micromamba env list | grep -q "$env_name"; then
    micromamba create -y -n "$env_name" python="$python_version"
fi

# Install PyTorch (GPU if available, else CPU)
if command -v nvidia-smi &>/dev/null; then
    micromamba run -n "$env_name" pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
else
    micromamba run -n "$env_name" pip install torch torchvision torchaudio
fi

# Install other packages
micromamba run -n "$env_name" pip install \
  numpy pandas matplotlib seaborn tqdm scikit-learn statsmodels \
  h5py networkx pyro-ppl pysam snakemake \
  pyteomics lxml biopython joblib

# Test imports
echo "Testing imports..."
modules=(torch numpy pandas snakemake pyteomics lxml Bio)
for mod in "${modules[@]}"; do
    echo -n "import $mod: "
    micromamba run -n "$env_name" python -c "import $mod" && echo "OK" || echo "FAILED"
done

# Test CUDA availability
echo -n "torch.cuda.is_available(): "
micromamba run -n "$env_name" python -c "import torch; print(torch.cuda.is_available())"
```

Run it with:

```bash
bash create_env.sh
```

### 5. Set up project and data linking

Save this as `setup_env_and_link.sh`:

```bash
#!/bin/bash
set -e

REPO_DIR="/mnt/c/Users/cecilia.DESKTOP-8JQ74OI/Documents/GitHub/01_mldata"
DATA_DIR="/mnt/d/research_backup/01_mldata_20250804"
LINK_NAME="mldata_data"
ENV_NAME="pdata_env"
PYTHON_VERSION="3.12"
MAMBA_URL="https://micro.mamba.pm/api/micromamba/linux-64/latest"

# Check micromamba
if ! command -v micromamba &>/dev/null; then
  echo "Installing micromamba..."
  mkdir -p ~/micromamba/bin
  curl -Ls $MAMBA_URL -o ~/micromamba/bin/micromamba
  chmod +x ~/micromamba/bin/micromamba
  export PATH=~/micromamba/bin:$PATH
fi

export MAMBA_EXE=~/micromamba/bin/micromamba
export MAMBA_ROOT_PREFIX=~/micromamba
eval "$($MAMBA_EXE shell hook --shell bash)"

# Check environment
if ! micromamba env list | grep -q "$ENV_NAME"; then
  echo "Creating micromamba environment: $ENV_NAME"
  micromamba create -y -n "$ENV_NAME" python="$PYTHON_VERSION"
fi

# Check snakemake
if ! micromamba run -n "$ENV_NAME" snakemake --version &>/dev/null; then
  echo "Installing packages..."
  bash create_env.sh
else
  echo "Snakemake already installed in $ENV_NAME"
fi

# Create symlink
cd "$REPO_DIR"
if [ ! -L "$LINK_NAME" ]; then
  echo "Creating symlink: $LINK_NAME → $DATA_DIR"
  ln -s "$DATA_DIR" "$LINK_NAME"
else
  echo "Symlink already exists: $LINK_NAME"
fi

echo -e "\n✅ Environment is ready!"
echo "➡ micromamba activate $ENV_NAME"
echo "➡ cd $REPO_DIR"
echo "➡ snakemake -j4"
```

Then run:

```bash
bash setup_env_and_link.sh
```

---

## Quick Start Command: `openmldata`

Add this to `~/.bashrc`:

```bash
alias openmldata="micromamba activate pdata_env && cd ~/github/01_mldata && cursor ."
```

Then in WSL terminal, run:

```bash
openmldata
```

This will:

* Activate your bioinformatics environment
* Enter your project folder
* Launch the Cursor editor

---

## 6. How to Back Up Your Data (Safely, Automatically, and Cleanly)

### 🧬 What to Back Up

| Type               | Location                                                   | Strategy                    |
|--------------------|------------------------------------------------------------|-----------------------------|
| Code               | GitHub repo                                                | Use `git push` regularly    |
| Data (raw/intermediate) | External hard drive (e.g. `D:/research_backup`) and cloud copy | Use `rsync`, nightly schedule |

---

### 🕐 Automate with Cron (every day at 2:00 AM)

Edit your crontab by running:

```bash
crontab -e
```

Then add this line at the bottom:

```cron
0 2 * * * bash /home/zixuan/scripts/cron_backup.sh
```

---

### ✅ This setup will:

* Back up your entire code and data every night
* Store backups in **two separate drives**
* Automatically clean backups older than **2 weeks**
* Let you sleep peacefully knowing everything is versioned and protected


