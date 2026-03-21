
# SOCHoneypotLab

<h1>Implementing a SOC and Honeypot in Azure</h1>



<h2>Description</h2>
This project simulates a basic Security Operations Center (SOC) using Microsoft Sentinel and a publicly exposed Windows virtual machine acting as a honeypot.

The system was intentionally configured to attract malicious traffic, allowing me to monitor and analyze real-world attack attempts. I focused on detecting RDP brute force activity by collecting Windows Event Logs, ingesting them into Azure Log Analytics, and visualizing the data in Microsoft Sentinel.

A custom PowerShell script was used to extract attacker IP addresses, enrich them with geolocation data, and display attack origins on a global map.

This project demonstrates how SOC environments detect and analyze authentication-based attacks.


<h2>Languages and Utilities Used</h2>

- Azure Virtual Machines </b>
- Microsoft Sentinel (SIEM) </b>
- Log Analytics </b> 


<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>SOC Workflow & Implementation:</h2>



To begin, I created a virtual machine on Azure to be used as a honeypot. 
<img width="1598" height="721" alt="hpotvmex" src="https://github.com/user-attachments/assets/208d54b6-0b60-4174-9eed-fc6d4a08930b" />


Configured authentication credentials and network security rules to expose the VM to the public internet.

Connected via RDP and disabled host-based firewall protections to simulate a vulnerable target.
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

<h2>Detection Logic</h2>

To detect RDP brute-force activity, I analyzed failed login attempts collected from the honeypot and ingested into Azure Log Analytics.

Using KQL, I parsed data from a custom log table (FAILED_RDP_WITH_GEO_CL) to extract fields such as timestamp, username, source IP address, and geographic information.

By examining repeated login failures from the same IP address over short periods, I identified patterns consistent with automated brute-force attacks.

This approach demonstrates how authentication logs can be used in a SOC environment to detect suspicious login behavior and identify potential threats.


<h2>Key Results</h2>

- Detected thousands of RDP brute force login attempts from external IP addresses
- Identified repeated failed login attempts during brute force activity
- Observed attack patterns targeting common usernames such as "Administrator"
- Visualized global attack distribution using Microsoft Sentinel Workbooks


<h2>Analysis & SOC Perspective</h2>

The observed attack patterns indicate automated brute-force activity targeting exposed RDP services.

Repeated failed login attempts from the same IP and frequent targeting of usernames such as "Administrator" suggest scripted attacks rather than manual intrusion attempts.

From a SOC perspective, this activity can be detected using authentication logs and correlated across time to identify abnormal login behavior.

Recommended mitigation strategies include:

- Enforcing account lockout policies after repeated failed attempts  
- Enabling multi-factor authentication (MFA)  
- Restricting RDP access to trusted IP ranges  
- Blocking or rate-limiting suspicious source IP addresses  

These controls significantly reduce the effectiveness of brute-force attacks and limit exposure of publicly accessible systems.




