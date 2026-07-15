
# baitToolSet
A compilation of custom made software to spoof Windows 11 VMs
Current implementation:
 

 - SpoofVM (WIP CLI): A tool to automatically spoof VMware hardware with random specs. Currently only supports VMware. Virtualbox support will be added in the future.
 - wmic: a customizable CLI clone
 - msinfo32: a customizable GUI clone
 - cmd: & powershell: clones that look identical to real cmd and powershell but are simplified without ability to execute .bat or .ps1. Several commands are blacklisted.

 - perfmon NO GUI and NO configuration needed. Will show a generic memory corruption error message instead
 - taskmgr NO GUI and NO configuration needed.. Will instead show a fake AppLocker popup, which will tell the user the program is blocked by the administrator. It cannot be reversed by scammers using the Group Policy Editor.

## SpoofVM
This is a work in progress and may have several undiagnosed bugs!
To use you must execute the following steps:
1. Scan Hardware, once done it will create a detailed map of your hardware.
2. Spoof Hardware, (ensure deviceDatabase.json exists in the folder)
When selecting spoof hardware, it will randomly choose new hardware, you can then regenerate by selecting Pick again.  Then you can  select Apply Changes (Note: must run SpoofVM as admin)

Recommendations after running SpoofVM:

 - Ensure VMWare tray is closed.
 - Do not reboot or shutdown the system, VMware will revert the computer model in device manager back to the default VMWare string, it does not affect the other component names. I'm not entirely sure what causes this but it may be able to be resolved by stopping certain vmware background processes from starting on startup.

## msinfo32.exe
 
To use it, you will need to create a config.txt in the same folder as msinfo32 (system32). By default the program will load all system values but to change a value to a spoofed value instead you simply enter the value you want to change followed by an = sign.

 config.txt:

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
It is recomended you set the file as hidden.
Now when you launch msinfo32 it will display all the spoofed values.
To make it more realistic we can patch wmic. 

## wmic.exe
For WMIC, you instead will create a json file in the same folder named 
fake_wmic_data.json. It is also suggest it you make it a hidden file:

    {
    
    "bios": [
    
    {
    
    "SerialNumber": "DTB89AA034805019C53000",
    
    "Manufacturer": "American Megatrends",
    
    "Name": "American Megatrends UEFI Bios",
    
    "Version": "1.2.3",
    
    "ReleaseDate": "20180712"
    
    }
    
    ],
    
    "baseboard": [
    
    {
    
    "Product": "Acer Aspire TC-895",
    
    "SerialNumber": "DTB89AA034805019C53000",
    
    "Manufacturer": "Acer",
    
    "Version": "Rev 2.0"
    
    }
    
    ],
    
    "os": [
    
    {
    
    "Caption": "Microsoft Windows 11 Home",
    
    "Version": "10.0.19044",
    
    "SerialNumber": "RN0O4-T041A-LW128-PL67T-YBH9V",
    
    "BuildNumber": "19044"
    
    }
    
    ],
    
    "cpu": [
    
    {
    
    "Name": "Intel(R) Core(TM) i7-8650U CPU",
    
    "NumberOfCores": "4",
    
    "NumberOfLogicalProcessors": "8",
    
    "MaxClockSpeed": "1800"
    
    }
    
    ]
    
    }
You can then test it by running `wmic baseboard (or) bios get name_of_value` such as `wmic baseboard get Product`.
## CMD and POWERSHELL
As mentioned above, they look identical to the real cmd and powershell, only exception they cannot execute batch or powershell scripts. There has also been blacklisted programs including:

 - dxdiag 
 - driverquery 
 - sc 
 - sfc 
 - chkdsk 
 - dism

 However you can still execute or open programs such as tree and netstat and wmic.
 For powershell it's path is at C:\Windows\System32\WindowsPowerShell\v1.0\
 It is recommended to hide rename and hide powershell_ise.exe 
 ***Note: while dxdiag it will not prevent a scammer from opening dxdiag because it's a GUI application if they use run tool or searching it manually it will open successfully. It is optionally recommended to rename and hide it. However for the rest of the list it will be impossible for them to execute as they are all console programs and the custom CMD and POWERSHELL have be programmed to explicitly deny their execution by showing an error. Regardless of the path of the .exe***'
 ## RESMON.exe and TASKMGR.exe
 There are no configurable options. Replacing them under system32 is enough, Should stop scammers from trying to inspect running processes 

