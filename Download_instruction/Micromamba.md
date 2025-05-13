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

## Official Website
https://mamba.readthedocs.io/en/latest/installation/micromamba-installation.html

## Micromamba Installation: Official vs. Optimized Method (Use Optimized Method)

### 1. Official Method (From website)

```bash
./bin/micromamba shell init -s bash -r ~/micromamba
source ~/.bashrc
````

#### How It Works:

1. Initializes Micromamba and writes configuration to `~/.bashrc`.
2. Uses `~/micromamba` as the root environment for storing packages and caches.
3. Runs `source ~/.bashrc` to load changes.

#### Pros:

* Simple and straightforward (just two commands).
* Officially recommended by Micromamba documentation.
* Automatically writes to `.bashrc` for persistent activation.

#### Cons:

* Path is hard-coded to `~/Downloads/bin/micromamba`.
* If you move the binary, it will break the path.
* Difficult to clean up: You have to manually find and delete `.bashrc` entries.
* May cause infinite loops if re-initialized multiple times.


### 2. Optimized Method (Standardized Path and Cleaner Setup)

```bash
# Step 1: Download and move to ~/.local/bin
cd ~/Downloads
curl -Ls https://micro.mamba.pm/api/micromamba/linux-64/latest | tar -xvj bin/micromamba

mkdir -p ~/.local/bin
mv ~/Downloads/bin/micromamba ~/.local/bin/
chmod +x ~/.local/bin/micromamba

# Step 2: Update PATH
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Step 3: Initialize shell
eval "$(micromamba shell hook --shell bash)"
```

#### How It Works:

1. Downloads `micromamba` and moves it to `~/.local/bin` (standard user path).
2. Updates `~/.bashrc` to include this path.
3. Initializes shell with the correct binary path.

#### Pros:

* Standardized path (`~/.local/bin`), avoids dependency on `~/Downloads`.
* No infinite loops during `source ~/.bashrc`.
* Easy cleanup — just delete `~/.local/bin/micromamba`.
* Follows Linux best practices for user-installed binaries.

#### Cons:

* Requires a few extra steps to move and configure the path.
* Users need to be comfortable with `chmod` and `PATH`.


### Comparison Table

|                      | Official Method             | Optimized Method                 |
| -------------------- | --------------------------- | -------------------------------- |
| Installation Path    | `/Downloads/bin/micromamba` | `~/.local/bin/micromamba`        |
| Loop Issues          | Possible infinite loops     | Completely avoids loops          |
| Path Configuration   | Hard-coded, fragile         | Dynamically managed in PATH      |
| Cleanup Difficulty   | Hard to clean up            | Easy, just delete the binary     |
| Compatibility        | Might break if moved        | Works seamlessly across sessions |
| Linux Best Practices | No                          | Yes                              |



