# Atomic Red Team Setup

## Installation
```powershell
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing)

Install-AtomicRedTeam -getAtomics -Force
```

---

## Add Defender Exclusions
```powershell
Add-MpPreference -ExclusionPath "C:\AtomicRedTeam"
Add-MpPreference -ExclusionPath "C:\Users\$env:USERNAME\AppData\Local\Temp"

# Verify
Get-MpPreference | Select-Object ExclusionPath
```

---

## Import Module
```powershell
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
```

---

## Persist Module Across Sessions
```powershell
notepad $PROFILE
```
Add this line to the file and save:
```powershell
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1"
```

---

## Run a Test
```powershell
Invoke-AtomicTest T1059.001
```
