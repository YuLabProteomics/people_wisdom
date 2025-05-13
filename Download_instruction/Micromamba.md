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


