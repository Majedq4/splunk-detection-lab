# Splunk Setup

## Architecture
- Splunk Universal Forwarder installed on Windows 10 VM
- Forwards logs to Splunk Enterprise on Ubuntu Server via port 9997
- SOC Analyst accesses Splunk Web from host machine on port 8000

## Verify Forwarder is Running
```powershell
Get-Service SplunkForwarder

type "C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf"
```

## Index Used
- `main`

## Data Sources Collected

| Source | Sourcetype | Key Event IDs |
|--------|-----------|---------------|
| Sysmon | WinEventLog:Sysmon | 1,3,7,8,10,11,12,13,22 |
| PowerShell | WinEventLog:PowerShell | 4103, 4104 |
| Windows Defender | WinEventLog:Microsoft-Windows-Windows Defender | 1116, 1117, 5001 |

## Verify Logs Reaching Splunk
```splunk
index=main sourcetype="WinEventLog:Sysmon"
```

## Ubuntu Server Checks
```bash
# Check Splunk is running
sudo /opt/splunk/bin/splunk status

# Check receiving port 9997 is active
sudo /opt/splunk/bin/splunk list forward-server

# Check receiving config via Splunk Web
# Settings → Forwarding and Receiving → Receive Data
```
