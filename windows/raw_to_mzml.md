---

# `raw_to_mzml.bat` Usage Guide (with path arguments)

## File Content (`raw_to_mzml.bat`)

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

---

## Method 1: Run from PowerShell or Command Prompt

1. Open PowerShell or CMD.

2. Navigate to the directory where the `.bat` file is located:

   ```powershell
   cd "C:\Users\cecilia.DESKTOP-8JQ74OI\Documents\01_mldata"
   ```

3. Run the script with two arguments: the input folder containing `.raw` files and the output folder for `.mzML`:

   ```powershell
   .\raw_to_mzml.bat "C:\path\to\raw" "C:\path\to\mzML"
   ```

---

## Method 2: Drag-and-Drop Arguments (GUI method)

1. Drag the input and output folders into the command window after typing the `.bat` file name.
2. The folder paths will be automatically passed as arguments to the script.

---

## Notes

* `%~1` and `%~2` represent the first and second arguments passed to the script.
* If arguments are missing, the script will print usage instructions and exit.
* The path to `msconvert.exe` is hardcoded; you may adjust it if the location changes.
* This script is reusable across multiple projects. Simply pass different folders as arguments without modifying the script itself.

---

# `raw_to_mzml.bat` 使用说明（支持路径参数）

## 文件内容（`raw_to_mzml.bat`）

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

---

## 使用方式一：命令行调用

1. 打开 PowerShell 或 CMD。

2. 切换到 `.bat` 文件所在目录，例如：

   ```powershell
   cd "C:\Users\cecilia.DESKTOP-8JQ74OI\Documents\01_mldata"
   ```

3. 执行转换命令：

   ```powershell
   .\raw_to_mzml.bat "C:\path\to\raw" "C:\path\to\mzML"
   ```

   替换路径为你项目实际的原始和输出文件夹。

---

## 使用方式二：通过拖拽传参

1. 将两个文件夹（raw 输入目录 和 mzML 输出目录）拖入命令行窗口。
2. 将拖入的路径粘贴到命令中作为参数运行，或创建快捷方式以便图形界面使用。

---

## 说明

* `%~1` 和 `%~2` 分别为脚本运行时传入的第一个、第二个参数。
* 若参数缺失，脚本会提示用法并退出。
* `msconvert.exe` 路径已写死为解压目录下的固定位置，可根据实际情况调整。
* 脚本适用于批量项目重用，无需每次修改文件内容。
