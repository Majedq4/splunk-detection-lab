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
> Screenshot: <img width="2555" height="567" alt="image" src="https://github.com/user-attachments/assets/bdbc1dd0-99a1-4721-8a40-075de5175013" />

---

## 2. Normal Processes (EventCode 1)
```splunk
index=main sourcetype="WinEventLog:Sysmon"
| stats count by Image
| sort - count
```
> Screenshot: <img width="2557" height="741" alt="image" src="https://github.com/user-attachments/assets/d70ee6e3-e80b-4b37-9840-2e64befefae7" />

---

## 3. Normal Parent-Child Relationships
```splunk
index=main sourcetype="WinEventLog:Sysmon"
| stats count by ParentImage, Image
| sort - count
```
> Screenshot: <img width="2549" height="744" alt="image" src="https://github.com/user-attachments/assets/c23fa0f8-8a87-4c09-b739-719e142cba08" />

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
> Screenshot: <img width="2551" height="739" alt="image" src="https://github.com/user-attachments/assets/95b06afc-8743-4d1c-883b-f5ef8be9de1e" />

Key observations:
- Defender making HTTPS connections (443) to Microsoft IPs — normal
- svchost.exe handling DNS via 1.1.1.1 — normal
- OneDrive syncing to Microsoft cloud — normal
- VirtualBox internal network traffic (10.0.2.x) — normal
- No unexpected outbound connections observed

---

## 5. Normal DNS Queries (EventCode 22)
```splunk
index=main sourcetype="WinEventLog:Sysmon" EventCode=22
| stats count by Image, QueryName
| sort - count
```
> Screenshot: <img width="2537" height="735" alt="image" src="https://github.com/user-attachments/assets/60d9ac45-0305-472a-b941-dfd94923e4e9" />

---

## Baseline Summary

| Metric | Value |
|--------|-------|
| Machine state | Normal usage |
| Attacks running | None |
