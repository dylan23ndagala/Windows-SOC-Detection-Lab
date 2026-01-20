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
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/18720e23dd3b7b8abbc8e49a00b1851279a4c6b9/PE%20Search%20In%20Splunk.png" width="400"><br>
      <sub>I used this command "net localgroup administrators attacker1 /add" to simulate privielge escalation to the admin group and this splunk search displays that new member was added</sub>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/18720e23dd3b7b8abbc8e49a00b1851279a4c6b9/PE%20Splunk%20Log%20Success.png" width="400"><br>
      <sub>Splunk Log providing complete detail that this attack was confirmed privilee escalation</sub>
    </td>
  </tr>
</table>

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
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/c85c969ff1a07cdccf001f8e86e29bb31a2e53bb/DeletionA4%20%231.png" width="400"><br>
      <sub>In a similar situation I used the Windows vm to delete the persistence1 account</sub>
    </td>
    <td align="center">
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/c85c969ff1a07cdccf001f8e86e29bb31a2e53bb/DeletionA4%20%232.png" width="400"><br>
      <sub>Log shows that indeed an account was created by a user who was on the windows device</sub>
    </td>
  </tr>
</table>

---

## Alerts Implemented
Two automated SOC alerts were created to allow detection for known vulnerabilities:

- Brute Force Authentication Detection  
- Privilege Escalation (Admin Group Modification)  

---

## Alert Validation
I tested the Brute Force alert and it was validated by re-running the  attack scenario and confirming successful alert triggering within the scheduled execution window.

Screenshots of created and triggered alerts are below:
<table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/c85c969ff1a07cdccf001f8e86e29bb31a2e53bb/Alert%20Creation%20BF.png" width="400"><br>
      <sub>The alert I created for Brute Force Attacks</sub>
    </td>
    </td>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/49812d84148eb7851a94e92bb30397e3a3125790/Alert%20Creation%20PE.png" width="400"><br>
      <sub>The alert I created for Privilege Escalation</sub>
    </td>
  <table align="center">
  <tr>
    <td align="center">
      <img src="https://github.com/dylan23ndagala/Windows-SOC-Detection-Lab/blob/49812d84148eb7851a94e92bb30397e3a3125790/Triggered%20BF%20Alert.png" width="400"><br>
      <sub>Successful Alert Detection for Brute Force Attack logs</sub>
    </td>
    </td>
  </tr>
</table>



---

## Skills Demonstrated
- SIEM deployment and configuration  
- Windows Security Event analysis  
- SOC detection logic  
- Alert tuning and validation  
- Incident-style documentation  

---

## Conclusion
This lab demonstrates end-to-end SOC functionality, including log ingestion, threat detection, alerting, and validation. The project emphasizes practical SOC workflows rather than isolated event analysis. I was able to accurately identify 5 different real world attacks and what they would like from a SIEM like Splunk. This lab ultimately improved my skills and abilties to identify and use SIEM logs properly to strengthen my blue-team abilties and respond to an attack on an enviornment responsibly.
