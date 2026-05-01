# Splunk Detection Lab

[![MITRE ATT&CK](https://img.shields.io/badge/-MITRE%20ATT%26CK-FF0000?&style=for-the-badge&logoColor=white)](https://attack.mitre.org/)
[![Splunk](https://img.shields.io/badge/-Splunk-000000?&style=for-the-badge&logo=Splunk&logoColor=white)](https://www.splunk.com/)

## Objective
Built a home SOC lab to simulate real-world attacks using Atomic Red Team 
and detect them using Splunk Enterprise. Focused on MITRE ATT&CK techniques, 
SPL query writing, and threat hunting methodology — directly applying skills 
from the eCTHP certification in a practical environment.

---

## Lab Architecture

| Component | Role | Details |
|-----------|------|---------|
| Windows 10 | Victim machine | Sysmon + Splunk Forwarder + Atomic Red Team |
| Ubuntu Server | SIEM | Splunk Enterprise |
| Host Machine | SOC Analyst | Splunk dashboard via port 8000 |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Splunk Enterprise | Log ingestion, SPL queries, alerting |
| Sysmon | Endpoint telemetry |
| Atomic Red Team | MITRE ATT&CK simulation |
| Windows Defender | Endpoint protection |

---

## Techniques Detected

| ATT&CK ID | Technique | Tactic | Report |
|-----------|-----------|--------|--------|
| T1059.001 | PowerShell | Execution | [View Report](./Detections/T1059.001.md) |
| T1059.003 | Windows Command Shell | Execution | [View Report](./Detections/T1059.003.md) |
| T1547.001 | Registry Run Keys / Startup Folder | Persistence | [View Report](./Detections/T1547.001.md) |

---

## Next Steps (Soon!)
- [ ] Add Splunk SOAR for automated alert response
- [ ] Build Gmail alerting playbook
- [ ] Add more ATT&CK techniques
