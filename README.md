# Windows SOC Detection Lab Using Splunk SIEM

## Overview
This project demonstrates the design and implementation of a small-scale Security Operations Center (SOC) lab using Splunk SIEM. The lab focuses on ingesting Windows Security Event Logs, simulating common attack techniques, and detecting malicious behavior through correlation searches and alerts.

---

## Lab Architecture
- SIEM: Splunk Enterprise (Ubuntu VM)
- Endpoint: Windows 10 VM
- Log Collection: Splunk Universal Forwarder
- Network: VirtualBox Host-Only Network
<br/>

## Lab Setup
- Confirm Splunk Download and Functioning on Ubuntu VM and Splunk Universal Forwader is Downloaded on Windows 10 VM
- Ensure port 9997 is open to receive data
- Ensuring I can see Windows logs
<br/>
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/90b590af1b12f66008ceae5b3b6b2d09adba3d2c/univdownloadW10.png" width="400"><br>
      <sub>Windows VM Successful Installation</sub>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/90b590af1b12f66008ceae5b3b6b2d09adba3d2c/Splunk_Home_Page_Success_01.png" width="400"><br>
      <sub>Ubuntu Successful Installation</sub>
    </td>
    <table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/a744f00316ccb12e22f57b1c15af6c16924fcaa5/Port%209997%20working.png" width="400"><br>
      <sub>Port 9997 open</sub>
    </td>
    <table align="center">
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/a744f00316ccb12e22f57b1c15af6c16924fcaa5/Windows%20Logs%20showing.png" width="400"><br>
      <sub>Windows Logs working and showing in Splunk</sub>
    </td>
  </tr>
</table>


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
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/6a10d24f3d1b898680ddbd293f6cd0481e733460/Failed%20Login.png" width="400"><br>
      <sub>Purposely typing wrong password into Windows Endpoint Device</sub>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/6a10d24f3d1b898680ddbd293f6cd0481e733460/BruteforceA1%20%231.png" width="400"><br>
      <sub>Using Splunk SIEM on Ubuntu and searching for failed attempts (11 failed attempts found)</sub>
    </td>
  </tr>
   <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/6a10d24f3d1b898680ddbd293f6cd0481e733460/BruteForceA1%20%232.png" width="400"><br>
      <sub>Splunk Providing additonal details from the attack attempt</sub>
    </td>
  </tr>
</table>

[Successful Login After Failures (Account Compromise)]
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/6a10d24f3d1b898680ddbd293f6cd0481e733460/AccountCompA2%231.png" width="400"><br>
      <sub>Using a similar search, This is what it would look like if the account was compromised and the brute force attack worked</sub>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/6a10d24f3d1b898680ddbd293f6cd0481e733460/AccountCompA2%20%232.png" width="400"><br>
      <sub>Splunk providing more detail for which account was compromised</sub>
    </td>
  </tr>
</table>

[Privilege Escalation]


[Unauthorized Account Creation]
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/a744f00316ccb12e22f57b1c15af6c16924fcaa5/UnAuthAccCreationA3%20%231.png" width="400"><br>
      <sub>Using Windows Vm to simulate an attacker making account named persistence1</sub>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/a744f00316ccb12e22f57b1c15af6c16924fcaa5/UnAuthAccCreationA3%20%232.png" width="400"><br>
      <sub>Searching with code 4720 and a log is shown indicacting a new account was made</sub>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/a744f00316ccb12e22f57b1c15af6c16924fcaa5/UnAuthAccCreationA3%20%233.png" width="400"><br>
      <sub>Log shows that indeed an account was created by a user who was on the windows device</sub>
    </td>
  </tr>
</table>

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
