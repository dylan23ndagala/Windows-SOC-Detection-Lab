# Windows SOC Detection Lab Using Splunk SIEM

## Overview
This project demonstrates the design and implementation of a small-scale Security Operations Center (SOC) lab using Splunk SIEM. The lab focuses on ingesting Windows Security Event Logs, simulating common attack techniques, and detecting malicious behavior through correlation searches and alerts.

---

## Lab Architecture
- SIEM: Splunk Enterprise (Ubuntu VM)
- Endpoint: Windows 10 VM
- Log Collection: Splunk Universal Forwarder
- Network: VirtualBox Host-Only Network

Confirm Splunk and Splunk Unviersal Forwader is Downloaded: <br/>


---

## Detection Testing
The following attack scenarios were simulated and detected:

- Brute-force authentication attacks  
- Successful login following failed attempts  
- Privilege escalation via administrator group modification  
- Unauthorized account creation  
- Account deletion (anti-forensics)  

---

## Detection Evidence
Detailed detection logic and screenshots for each simulated attack are available below:

[Brute-Force Authentication]

[Successful Login After Failures]

[Privilege Escalation]

[Unauthorized Account Creation]

[Account Deletion]


---

## Alerts Implemented
Two automated SOC alerts were created:

- Brute Force Authentication Detection  
- Privilege Escalation (Admin Group Modification)  

---

## Alert Validation
Both alerts were validated by re-running the corresponding attack scenarios and confirming successful alert triggering within the scheduled execution window.

Screenshots of triggered alerts are below



---

## Skills Demonstrated
- SIEM deployment and configuration  
- Windows Security Event analysis  
- SOC detection logic  
- Alert tuning and validation  
- Incident-style documentation  

---

## Conclusion
This lab demonstrates end-to-end SOC functionality, including log ingestion, threat detection, alerting, and validation. The project emphasizes practical SOC workflows rather than isolated event analysis.
