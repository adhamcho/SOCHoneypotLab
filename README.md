
# SOCHoneypotLab

<h1>Implementing a SOC and Honeypot in Azure</h1>



<h2>Description</h2>
This project simulates a basic Security Operations Center (SOC) using Microsoft Sentinel and a publicly exposed Windows virtual machine acting as a honeypot.

The system was intentionally configured to attract malicious traffic, allowing me to monitor and analyze real-world attack attempts. I focused on detecting RDP brute force activity by collecting Windows Event Logs, ingesting them into Azure Log Analytics, and visualizing the data in Microsoft Sentinel.

A custom PowerShell script was used to extract attacker IP addresses, enrich them with geolocation data, and display attack origins on a global map.

This project helped me understand how real-world SOC environments detect and analyze authentication-based attacks.


<h2>Languages and Utilities Used</h2>

- Azure Virtual Machines </b>
- Microsoft Sentinel (SIEM) </b>
- Log Analytics </b> 


<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>



To begin, I created a virtual machine on Azure to be used as a honeypot. 
<img width="1598" height="721" alt="hpotvmex" src="https://github.com/user-attachments/assets/208d54b6-0b60-4174-9eed-fc6d4a08930b" />


I created a username and password, and a network group to allow all ports to access the VM, in order to be open to the public internet. 

I connected to my VM using RDP and disabled all firewalls.
![image](https://github.com/user-attachments/assets/d3a8a8e9-5bd4-4d0f-b572-a4f91ac6ff26)





I implemented a PowerShell script to extract failed RDP login attempts from Windows Event Viewer and enrich attacker data with geolocation information.

![image](https://github.com/user-attachments/assets/eb92d024-a13b-49c1-9c5f-97989f4e2918)

These logs show repeated failed login attempts, indicating a brute force attack. 
Multiple attempts targeting usernames such as "Administrator" suggest automated attack behavior from external sources.



![image](https://github.com/user-attachments/assets/3634ba09-1182-4eb1-b761-c9bba5833f5b)
Logs were ingested into Azure Log Analytics and parsed using a custom KQL query to extract fields such as timestamp, username, source IP, and geographic data.



Using Microsoft Sentinel as my SIEM, I created a workbook for my world map.


![image](https://github.com/user-attachments/assets/da2824e9-5595-4591-b84a-a0ac99f93989)


This visualization highlights the global distribution of RDP brute force attacks targeting the honeypot. 
The data demonstrates how exposed systems are continuously scanned and attacked by automated sources across multiple regions.


<h2>Key Results</h2>

- Detected thousands of RDP brute force login attempts from external IP addresses
- Identified repeated failed login attempts during brute force activity
- Observed attack patterns targeting common usernames such as "Administrator"
- Visualized global attack distribution using Microsoft Sentinel Workbooks

<h2>Analysis & SOC Perspective</h2>

- Repeated failed authentication attempts are commonly associated with brute force attacks  
- Repeated login attempts against "Administrator" suggest automated attack scripts  
- A SOC analyst could create alerts for repeated failed login attempts from the same IP  
- Enforcing account lockout policies or MFA would significantly reduce attack success  




