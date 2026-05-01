# Baseline — Normal Behavior Snapshot

**Date captured:** April 24, 2026
**Status:** No attacks running, clean machine
**Observation period:** Before any ATT&CK simulations

---

## 1. Event Codes Present (Sysmon)
```splunk
index=main sourcetype="WinEventLog:Sysmon"
| stats count by EventCode
| sort - count
```
> Screenshot: `screenshots/baseline-eventcodes.png`

---

## 2. Normal Processes (EventCode 1)
```splunk
index=main sourcetype="WinEventLog:Sysmon"
| stats count by Image
| sort - count
```
> Screenshot: `screenshots/baseline-processes.png`

Key observations:
- Most common process: `svchost.exe`
- No suspicious processes observed at baseline

---

## 3. Normal Parent-Child Relationships
```splunk
index=main sourcetype="WinEventLog:Sysmon"
| stats count by ParentImage, Image
| sort - count
```
> Screenshot: `screenshots/baseline-parentchild.png`

Key observations:
- `services.exe` spawns `svchost.exe` — normal
- `explorer.exe` spawns browser and system tools — normal

---

## 4. Normal Network Connections (EventCode 3)
```splunk
index=main sourcetype="WinEventLog:Sysmon" EventCode=3
| stats count by Image, DestinationIp, DestinationPort
| sort - count
```
> Screenshot: `screenshots/baseline-network.png`

Key observations:
- Chrome making HTTPS connections (port 443) — normal
- svchost connecting to Microsoft IPs — normal

---

## 5. Normal PowerShell Activity (EventCode 4104)
```splunk
index=main sourcetype="WinEventLog:PowerShell" EventCode=4104
| stats count by ScriptBlockText
| sort - count
```
> Screenshot: `screenshots/baseline-powershell.png`

---

## 6. Normal DNS Queries (EventCode 22)
```splunk
index=main sourcetype="WinEventLog:Sysmon" EventCode=22
| stats count by Image, QueryName
| sort - count
```
> Screenshot: `screenshots/baseline-dns.png`

---

## Baseline Summary

| Metric | Value |
|--------|-------|
| Observation period | Before simulations |
| Machine state | Idle / normal usage |
| Attacks running | None |
| Sysmon config | Olaf Hartong Modular |
