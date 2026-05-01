# PowerShell Logging Configuration

## What Was Enabled

| Setting | Description |
|---------|-------------|
| Script Block Logging | Captures every command and script executed (EventCode 4104) |
| Module Logging | Captures module-level activity (EventCode 4103) |
| Transcription Logging | Saves full PowerShell sessions to disk |

## Why This Matters
Without these settings enabled, PowerShell activity is largely
invisible to a SIEM. Script Block Logging in particular is critical
for detecting fileless attacks, encoded commands, and malicious
downloads via `iex`/`iwr`.

---

## Commands Used

### Script Block Logging
```powershell
$basePath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
If (!(Test-Path $basePath)) { New-Item $basePath -Force }
Set-ItemProperty -Path $basePath -Name "EnableScriptBlockLogging" -Value 1
```

### Module Logging
```powershell
$modulePath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging"
If (!(Test-Path $modulePath)) { New-Item $modulePath -Force }
Set-ItemProperty -Path $modulePath -Name "EnableModuleLogging" -Value 1
```

### Transcription Logging
```powershell
$transcriptPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription"
If (!(Test-Path $transcriptPath)) { New-Item $transcriptPath -Force }
Set-ItemProperty -Path $transcriptPath -Name "EnableTranscripting" -Value 1
Set-ItemProperty -Path $transcriptPath -Name "OutputDirectory" -Value "C:\PSTranscripts"
```

---

## Verify Settings Applied
```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
```

Expected output:
EnableScriptBlockLogging : 1

---

## Verify in Splunk
```splunk
index=main sourcetype="WinEventLog:PowerShell" EventCode=4104
| stats count by host
```
