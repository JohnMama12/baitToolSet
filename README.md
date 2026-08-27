# 🛡️ baitToolSet

> A suite of custom Windows 11 binaries designed to defeat tech support scammer reconnaissance by spoofing system specs and blocking diagnostic tools.

[![Platform](https://img.shields.io/badge/Platform-Windows%2011-blue.svg)](https://www.microsoft.com/windows)
[![Status](https://img.shields.io/badge/Status-Work%20in%20Progress-orange.svg)](#)
[![Support](https://img.shields.io/badge/Support-VMware%20Only%20(VirtualBox%20TODO)-purple.svg)](#)


> **Disclaimer:** This tool set does **not** 100% guarantee your VM will remain undetected, as spoofing the installed software list is currently unsupported.

---

## ✨ Included Tools

| Component | Type | Description |
| :--- | :--- | :--- |
| **SpoofVM** | CLI | Automatically spoofs VMware hardware profiles using randomized system specs. |
| **msinfo32.exe** | GUI Clone | Customizable System Information viewer that reads spoofed values from a config file. |
| **wmic.exe** | CLI Clone | Customizable `wmic` replacement reading from dynamic JSON data. |
| **cmd / powershell** | Shell Clones | Visual clones with script execution disabled (`.bat`/`.ps1`) and blacklisted commands. |
| **perfmon.exe** | Binary | Triggers a fake memory corruption error instead of launching performance metrics. |
| **taskmgr.exe** | Binary | Triggers a fake, non-reversible AppLocker administrative block message. |

---

## 🚀 Usage & Configuration

### 1. SpoofVM (WIP)
-   Save a VMware Snapshot to roll back when needed in case you want to change back to another config
 

> Run `SpoofVM` with **Administrator privileges**.

1. Execute **Scan Hardware** to build a detailed hardware map of your target environment.
2. Ensure `deviceDatabase.json` is located in the working directory.
3. Select **Spoof Hardware** to randomly pull hardware definitions. Click **Pick again** to regenerate values if desired.
4. Select **Apply Changes**.

**Post-Spoofing Recommendations:**
- Close the **VMware Tray** application after applying changes.
- **Avoid Rebooting/Shutting Down:** VMware may reset the default system model string in Device Manager upon boot (other spoofed components will remain intact).
- Save another post change VMware Snapshot to roll back when needed

---

### 2. msinfo32.exe

Place your `config.txt` file in the same directory as the executable (`C:\Windows\System32`). It is strongly recommended to set `config.txt` as a **hidden file**.

**Sample `config.txt` Structure:**
```ini
BIOS Version/Date=American Megatrends Inc. R01-A3, 07/12/2018
Processor=Intel(R) Core(TM) i7-8700, 2500 Mhz, 2 Core(s), 1 Logical Processor(s)
BaseBoard Manufacturer=American Megatrends Inc.
BaseBoard Product=AT6W1
BaseBoard Version=1.1.3
OS Manufacturer=Microsoft Corporation
System Manufacturer=Acer, Inc.
System Model=Acer Aspire TC-895
System SKU=0000000000000000
Installed Physical Memory (RAM)=8.00 GB
Total Physical Memory=7.78 GB
Windows Directory=C:\WINDOWS
System Directory=C:\WINDOWS\system32
Boot Device=\Device\HarddiskVolume1\
BIOS Mode=UEFI
Locale=United States
```

## **TODO:**

 - Add Installed Software list spoofing
 -  Add Virtual Box Support
