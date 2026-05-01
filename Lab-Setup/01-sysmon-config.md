# Sysmon Configuration

## Version
```powershell
(Get-Item "$env:windir\sysmon64.exe").VersionInfo.ProductVersion
```

## Verify Sysmon is Running
```powershell
Get-Service Sysmon64
sysmon64 -c
```

## Configuration Used
**Olaf Hartong's Sysmon Modular Config**

- Source: https://github.com/olafhartong/sysmon-modular
- Reason: Provides modular, well-maintained ruleset that balances 
  noise reduction with high-fidelity detection. Well suited for 
  home lab and detection engineering environments.

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
| 3 | Network Connection |
| 7 | Image Loaded |
| 8 | CreateRemoteThread |
| 10 | ProcessAccess |
| 11 | File Created |
| 12 | Registry Key Created/Deleted |
| 13 | Registry Value Set |
| 22 | DNS Query |
