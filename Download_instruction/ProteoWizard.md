# What is ProteoWizard?

**ProteoWizard** is an open-source, cross-platform software toolkit designed for mass spectrometry (MS) data processing. It includes a suite of tools and libraries that support reading, writing, and converting vendor-specific raw data formats into open, standardized formats such as **mzML**, **mzXML**, and **MGF**.

The most widely used component is:

* **`msconvert`** – a command-line and graphical utility used to convert proprietary raw MS files into open formats suitable for downstream analysis.

---

# Why Use ProteoWizard?

| Reason                                         | Description                                                                                                                                                        |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Standardization**                            | Converts vendor-specific `.raw` files to open formats like **mzML**, allowing compatibility with a wide range of downstream tools (e.g., DIA-NN, OpenMS, Skyline). |
| **Cross-platform support**                     | Works on Windows, Linux, and macOS.                                                                                                                                |
| **Preprocessing capabilities**                 | Enables operations such as **centroiding**, **peak picking**, scan filtering, and data compression during conversion.                                              |
| **Scriptable for automation**                  | The `msconvert` command-line tool integrates easily into high-throughput workflows or pipelines.                                                                   |
| **Open data compatibility**                    | Facilitates data sharing and reuse by transforming data into open formats used across different platforms and research labs.                                       |
| **Optimized for Linux and analysis pipelines** | Saving files as **mzML** ensures compatibility with Linux-based tools and simplifies integration into reproducible analysis workflows.                             |

---

# ProteoWizard CLI + `raw_to_mzml.bat` Usage Guide

This guide explains how to download and set up the ProteoWizard command-line tool (`msconvert.exe`) and how to use a custom batch script (`raw_to_mzml.bat`) to convert Thermo `.raw` files into `.mzML` format.

---

## Part 1: Download and Prepare ProteoWizard (CLI Only)

### Step 1: Download the CLI package

* Go to the official [ProteoWizard GitHub Releases](https://proteowizard.sourceforge.io/download.html)
* Find and download:

  ```
  Windows 64-bit tar.bz2 (able to convert vendor files except T2D)
  ```

  Example filename:

  ```
  pwiz-bin-windows-x86_64-vc143-release-3_0_25143_fc4aaea.tar.bz2
  ```

---

### Step 2: Extract the files using 7-Zip

1. Install [7-Zip](https://www.7-zip.org/)

2. Open PowerShell and navigate to the folder where you downloaded the `.tar.bz2` file:

   ```powershell
   cd "C:\Users\cecilia.DESKTOP-8JQ74OI\Documents\proteowizard"
   ```

3. Extract the `.tar.bz2` file in two steps:

   ```powershell
   & "C:\Program Files\7-Zip\7z.exe" x "pwiz-bin-windows-x86_64-...tar.bz2" -aoa
   & "C:\Program Files\7-Zip\7z.exe" x "pwiz-bin-windows-x86_64-...tar" -aoa
   ```

4. After extraction, you will find `msconvert.exe` in the extracted folder.

---

## Part 2: Create and Use `raw_to_mzml.bat`

### File Content: `raw_to_mzml.bat`

```bat
@echo off
set RAW_DIR=%~1
set OUT_DIR=%~2

if "%RAW_DIR%"=="" (
  echo Please provide input and output folders!
  echo Usage: raw_to_mzml.bat "C:\path\to\raw" "C:\path\to\mzML"
  pause
  exit /b
)

"C:\Users\cecilia.DESKTOP-8JQ74OI\Documents\proteowizard\msconvert.exe" "%RAW_DIR%\*.raw" --mzML --outdir "%OUT_DIR%" --filter "peakPicking true 1-"
pause
```

Place this `.bat` file somewhere convenient (e.g., in your project folder).

---

## Part 3: How to Use the Script

### Method 1: Run via Terminal (PowerShell or CMD)

```powershell
cd "C:\path\to\folder\containing\raw_to_mzml.bat"
.\raw_to_mzml.bat "C:\path\to\raw" "C:\path\to\mzML"
```

* The first argument is the input directory with `.raw` files
* The second argument is the output directory for `.mzML` files

---

### Method 2: Drag-and-Drop Style (GUI)

* Drag the `.raw` folder and the output folder onto the `.bat` file or into the command line after calling the script.
* The script accepts those folders as arguments and runs automatically.

---

## Notes

* `%~1` and `%~2` are the first and second arguments passed to the script.
* If no arguments are provided, the script will show usage instructions and exit.
* The path to `msconvert.exe` is hardcoded and should be updated if your directory changes.
* This script works across projects without modification—just pass different folder paths when running.

---

# ProteoWizard CLI + `raw_to_mzml.bat` 使用说明

本教程介绍如何下载和配置 ProteoWizard 的命令行工具 `msconvert.exe`，并通过自定义脚本 `raw_to_mzml.bat` 将 Thermo `.raw` 文件批量转换为 `.mzML` 格式。

---

## 第一部分：下载并准备 ProteoWizard（命令行版本）

### 步骤 1：下载 CLI 压缩包

1. 打开 ProteoWizard 的 GitHub 发布页面：
   [https://github.com/ProteoWizard/pwiz/releases/latest](https://proteowizard.sourceforge.io/download.html)

2. 下载以下文件（带 tar.bz2 后缀的版本）：

   ```
   Windows 64-bit tar.bz2 (able to convert vendor files except T2D)
   ```

   示例文件名：

   ```
   pwiz-bin-windows-x86_64-vc143-release-3_0_25143_fc4aaea.tar.bz2
   ```

---

### 步骤 2：使用 7-Zip 解压两次

1. 安装 [7-Zip](https://www.7-zip.org/)

2. 打开 PowerShell，切换到压缩包所在目录，例如：

   ```powershell
   cd "C:\Users\cecilia.DESKTOP-8JQ74OI\Documents\proteowizard"
   ```

3. 解压 `.tar.bz2`：

   ```powershell
   & "C:\Program Files\7-Zip\7z.exe" x "pwiz-bin-...tar.bz2" -aoa
   & "C:\Program Files\7-Zip\7z.exe" x "pwiz-bin-...tar" -aoa
   ```

4. 解压完成后，将看到 `msconvert.exe` 所在的文件夹。

---

## 第二部分：编写并使用 `raw_to_mzml.bat` 脚本

### `raw_to_mzml.bat` 文件内容

```bat
@echo off
set RAW_DIR=%~1
set OUT_DIR=%~2

if "%RAW_DIR%"=="" (
  echo Please provide input and output folders!
  echo Usage: raw_to_mzml.bat "C:\path\to\raw" "C:\path\to\mzML"
  pause
  exit /b
)

"C:\Users\cecilia.DESKTOP-8JQ74OI\Documents\proteowizard\msconvert.exe" "%RAW_DIR%\*.raw" --mzML --outdir "%OUT_DIR%" --filter "peakPicking true 1-"
pause
```

你可以将该文件保存为 `raw_to_mzml.bat`，放在项目根目录或任意位置。

---

## 第三部分：脚本使用方法

### 方法一：通过终端（PowerShell 或 CMD）

```powershell
cd "C:\路径\到\bat文件所在目录"
.\raw_to_mzml.bat "C:\路径\到\raw文件夹" "C:\路径\到\mzML输出文件夹"
```

* 第一个参数是 `.raw` 文件所在文件夹
* 第二个参数是 `.mzML` 输出目录

---

### 方法二：拖拽传参（图形界面方式）

* 将 `.raw` 文件夹 和输出文件夹依次拖入 `.bat` 文件或命令行窗口
* 系统会自动将路径作为参数传入脚本运行

---

## 说明

* `%~1` 和 `%~2` 分别是传入脚本的第一个和第二个参数
* 若未提供参数，脚本会提示正确的使用方法并退出
* `msconvert.exe` 的路径已写死，如有变动请自行修改
* 脚本可复用于多个项目，只需每次传入不同路径即可，无需修改脚本内容

---
