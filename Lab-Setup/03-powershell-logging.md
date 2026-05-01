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

## Registry Keys Modified
HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging
→ EnableScriptBlockLogging = 1
HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging
→ EnableModuleLogging = 1
HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\Transcription
→ EnableTranscripting = 1

## Verify in Splunk
```splunk
index=main sourcetype="WinEventLog:PowerShell" EventCode=4104
| stats count by host
```
