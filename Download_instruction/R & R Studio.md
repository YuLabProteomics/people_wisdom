# CRAN (Comprehensive R Archive Network):
- CRAN is a network of servers that host the R programming language and its associated packages. 
- CRAN is like the "App Store" for the R programming language. If R is your phone, CRAN is where you download different "apps" (packages) to make it more powerful. These apps can help you with data analysis, machine learning, statistics, and much more. It’s a huge collection of user-contributed packages that you can easily install and use, so you don’t have to write everything from scratch. CRAN makes R easier and more powerful to use!

# The Tutorial of Downloading R

**R 4.5 is part of this cran40 repository, which is the most recent release as of April 15, 2025.**

---

# 1. Download Micromamba and then create an environment to download R and R studio

## Why Using a Separate Micromamba Environment for R and RStudio is Better

### **Advantages:**
1. **Environment Isolation**
   - R and RStudio are isolated from your Python environments, preventing dependency conflicts.
   - No interference with global packages or other environments (`scfm_env` remains untouched).

2. **Easy Management**
   - You can easily update, remove, or reinstall the R environment:
     ```bash
     micromamba remove -n r_env --all
     ```
   - This does not affect your Python setups.

3. **Version Control**
   - R and RStudio versions can be independently managed:
     ```bash
     micromamba update -n r_env r-base rstudio
     ```
   - Downgrading or switching versions is straightforward.

4. **Consistent Dependency Management**
   - Micromamba handles all dependencies consistently through `conda-forge`, avoiding system-level conflicts.

### **Problems Without Isolation:**
1. **Global Pollution**
   - Installing R globally affects all environments, leading to potential conflicts.

2. **Version Conflicts**
   - R and Python might depend on different versions of system libraries, causing compatibility issues.

3. **Dependency Hell**
   - Updating one package may break others, especially with R's heavy dependencies on C++ and system libraries.

4. **Hard to Rollback**
   - In a global setup, if something breaks, it’s hard to revert. With Micromamba, you can easily roll back.


**Code for downloading**
```bash
micromamba create -n mldata_env r-base r-essentials 

micromamba activate mldata_env
```

- R-base: Core r environment.
- R-essentials: Includes RStudio and some commonly used r packages

**Code for starting**
```
R # To start R

rstudio # To use Rstudio

```

**When using R**
```bash
install.packages("tidyverse")
install.packages("ggplot2")
install.packages("data.table")
```

- Input "68" in the selection
- Set default CRAN mirrow - MI
```bash
options(repos = c(CRAN = "https://cran.mtu.edu/"))
```
- Let the setting takes effect permanently.
```bash
cat('options(repos = c(CRAN = "https://cran.mtu.edu/"))\n', 
    file = file.path(Sys.getenv("HOME"), ".Rprofile"), 
    append = TRUE)
```

---


## Official Website

https://www.r-project.org/

- Click "download R", then you need to choose the CRAN Mirror

## Choice of CRAN Mirror
- Geographic Proximity: Closer mirrors tend to be faster (A server mirror that is geographically closer).
- Network Speed: Some universities have faster infrastructure.
- Reliability: Some mirrors are maintained better than others.

Since we are in Umass Chan Medical School, MA, the best CRAN mirrors for us would be:

✅ Top Recommended Mirrors (Closest to Worcester):
1. MBNI, University of Michigan, Ann Arbor, MI
https://repo.miserver.it.umich.edu/cran/
- Very reliable and quite close to Massachusetts.

2. Duke University, Durham, NC
https://archive.linux.duke.edu/cran/
- Good infrastructure, fast connection from the East Coast.

3. Indiana University
http://ftp.ussg.iu.edu/CRAN/
- Consistently well-maintained.

## Following the instructions, I will use downloading R for Linux (Ubuntu) as an example.
- Check the information of Ubuntu in your computer
```bash
lsb_release -a
```
- Output may look like:
```bash
zixuan_ye@wanglab-A16:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 24.04.2 LTS
Release:	24.04
Codename:	noble
```
- The official website is explaining how to install the latest version of R (version 4.5) on Ubuntu LTS (Long Term Support) releases. It highlights:

Which Ubuntu versions are currently supported:

- 24.04 ("noble")

- 22.04 ("jammy")

- 20.04 ("focal")

The architecture types:

- amd64: 64-bit architecture (Intel & AMD processors)

- arm64: ARM architecture (e.g., M1/M2 Mac, AWS Graviton)

- i386: Older 32-bit architecture (less common now)

**Explanation of Architecture Types：**

When you install software (like R), you need to match it to your computer's architecture. Architecture describes the way your computer's processor is designed. Here’s the breakdown:

1️⃣ **amd64 (x86_64)
- **Type:** 64-bit  
- **Processors:** Intel and AMD 64-bit processors.  
- **Common Machines:** Most modern laptops and desktops (e.g., Dell, Lenovo, HP).  
- **Why "amd64"?** The name comes from AMD, who first developed the 64-bit version of the x86 architecture. But it works for both Intel and AMD processors.  
- **Ubuntu Versions Supported:** All LTS versions (24.04, 22.04, 20.04).  

**Example:**  
If your computer is a typical Windows laptop, Ubuntu desktop, or Linux server, you are most likely running `amd64`.  


2️⃣ **arm64**
- **Type:** 64-bit for ARM processors.  
- **Processors:** ARM-based processors (like M1, M2, AWS Graviton).  
- **Common Machines:**  
  - Apple Silicon Macs (M1, M2, M3)  
  - Raspberry Pi 4  
  - AWS Graviton servers  
  - Many Android devices  

**Example:**  
If you have a new MacBook with an M1 or M2 chip, you are running `arm64`. If you are using a Raspberry Pi 4, it's also `arm64`.  


3️⃣ **i386**
- **Type:** 32-bit (Older technology, from the 90s and early 2000s).  
- **Processors:** Intel 80386 and compatible.  
- **Common Machines:** Very old desktops and laptops.  
- **Why It's Rare:** Most modern operating systems have stopped supporting 32-bit because almost all hardware now is 64-bit.  

**Example:**  
If you have an old PC from before 2010, it might be `i386`.  


🔍 **How to Check Your Architecture?**
You can check your architecture with the following command:  

```bash
uname -m
```
If it says x86_64, you are using amd64.
If it says aarch64, you are using arm64.
If it says i686 or i386, you are using i386.


### 🔄 **When to Choose Root vs. User?**
| 📝 **Operation Type**                 | 🛡️ **Permission Level** | 💡 **Reason**                                                        |
|--------------------------------------|-------------------------|----------------------------------------------------------------------|
| **System-wide software installation** | `Root (sudo)`          | Needs write access to `/usr/bin/`, `/usr/lib/`, and other system directories. |
| **R, Docker, Java installations**    | `Root (sudo)`          | These tools manage dependencies and are installed system-wide.       |
| **Network configuration, firewall settings** | `Root (sudo)`  | Changing network settings or firewall rules requires admin rights.   |
| **Python/R package installation**    | `User`                 | Use `pip install --user` or `install.packages()` to install locally. |
| **Editing local configuration files** | `User`                 | Modifying `~/.bashrc`, `~/.profile`, etc., only affects the user space. |

**Summary:**
- For **system-wide tools** (e.g., R, Docker): → **Root (sudo)**  
- For **Python/R packages** or **personal configuration**: → **User** 

In that case, I chose Root.

Here is the code to install R according to the website until 05/12/2025:
```bash
# update indices
apt update -qq
# install two helper packages we need
apt install --no-install-recommends software-properties-common dirmngr
# add the signing key (by Michael Rutter) for these repos
# To verify key, run gpg --show-keys /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc 
# Fingerprint: E298A3A825C0D65DFD57CBB651716619E084DAB9
wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
# add the repo from CRAN -- lsb_release adjusts to 'noble' or 'jammy' or ... as needed
add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
# install R itself
sudo apt install --no-install-recommends r-base
```

