# CRAN (Comprehensive R Archive Network):
- CRAN is a network of servers that host the R programming language and its associated packages. 
- CRAN is like the "App Store" for the R programming language. If R is your phone, CRAN is where you download different "apps" (packages) to make it more powerful. These apps can help you with data analysis, machine learning, statistics, and much more. It’s a huge collection of user-contributed packages that you can easily install and use, so you don’t have to write everything from scratch. CRAN makes R easier and more powerful to use!

# The Tutorial of Downloading R

**R 4.5 is part of this cran40 repository, which is the most recent release as of April 15, 2025.**

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





