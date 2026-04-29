# Atomic Red Team Setup

## Installation
```powershell
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing)

Install-AtomicRedTeam -getAtomics
```

## Issues Encountered & Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| `Invoke-AtomicTest` not recognized | Module not imported | Run `Import-Module` command |
| `PSSecurityException` | Execution policy restricted | `Set-ExecutionPolicy Bypass` |
| Atomics folder not found | `-getAtomics` incomplete | `Install-AtomicRedTeam -getAtomics -Force` |
| Windows Defender blocked files | AV flagged attack simulations | Add exclusion via `Add-MpPreference` |

## Fix Execution Policy
```powershell
Set-ExecutionPolicy Bypass -Scope CurrentUser -Force
```

## Import Module
```powershell
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
```

## Add Defender Exclusions
```powershell
Add-MpPreference -ExclusionPath "C:\AtomicRedTeam"
Add-MpPreference -ExclusionPath "C:\Users\$env:USERNAME\AppData\Local\Temp"

# Verify
Get-MpPreference | Select-Object ExclusionPath
```

## Re-download Atomics After Exclusion
```powershell
Install-AtomicRedTeam -getAtomics -Force
```

## Add to PowerShell Profile (Persist Across Sessions)
```powershell
notepad $PROFILE
# Add this line:
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1"
```

## Run a Test
```powershell
Invoke-AtomicTest T1059.001
```
