# Sysmon Configuration
## Installation

1. Download Sysmon from Microsoft Sysinternals:
   https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
2. Extract the zip and open PowerShell as Administrator
3. Install with default config:
```powershell
sysmon64 -accepteula -i
```

4. Or install with a config file directly:
```powershell
sysmon64 -accepteula -i C:\sysmonconfig.xml
```

---

## Verify Sysmon is Running
```powershell
Get-Service Sysmon64
sysmon64 -c
```

## Version
```powershell
(Get-Item "$env:windir\sysmon64.exe").VersionInfo.ProductVersion
```

## Configuration Used
**Olaf Hartong's Sysmon Modular Config**

- Source: https://github.com/olafhartong/sysmon-modular
- It Provides modular, well-maintained ruleset that balances 
  noise reduction with high-fidelity detection.

## Apply Configuration
```powershell
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig.xml" -OutFile "C:\sysmonconfig.xml"

sysmon64 -c C:\sysmonconfig.xml

sysmon64 -c
```

## Key Event IDs Captured

| EventCode | Description |
|-----------|-------------|
| 1 | Process Creation |
| 2 | File Creation Time Changed |
| 3 | Network Connection |
| 4 | Sysmon Service State Changed |
| 5 | Process Terminated |
| 7 | Image Loaded |
| 10 | ProcessAccess |
| 11 | File Created |
| 12 | Registry Key Created/Deleted |
| 13 | Registry Value Set |
| 17 | Pipe Created |
| 22 | DNS Query |
| 25 | Process Tampering |
| 26 | File Delete Logged |
| 29 | File Executable Detected |
