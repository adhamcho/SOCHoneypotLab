<<<<<<< HEAD
# SOCHoneypotLab
=======
<h1>Implementing a SOC and Honeypot in Azure</h1>



<h2>Description</h2>
In this project I setup Azure Sentinel (SIEM) and connected it to a live virtual machine acting as a honey pot. I observed live attacks (RDP Brute Force) from all around the world. I used a custom PowerShell script to look up the attackers Geolocation information and plot it on the Azure Sentinel Map.
<br />


<h2>Languages and Utilities Used</h2>

- Azure Virtual Machines </b>
- Microsoft Sentinel (SIEM) </b>
- Log Analytics </b> 


<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>



To begin, I created a virtual machine on Azure to be used as a honeypot. 
![image](https://github.com/user-attachments/assets/9bde243a-0dd5-4111-a275-5c4a6b0451ed)



I created a username and password, and a network group to allow all ports to access the VM, in order to be open to the public internet. 

I connected to my VM using RDP and disabled all firewalls.
![image](https://github.com/user-attachments/assets/d3a8a8e9-5bd4-4d0f-b572-a4f91ac6ff26)





I downloaded a Powershell script to use in Powershell ISE, which extracts RDP failed login logs from Windows Event Viewer and the attacker’s GEO locations.

![image](https://github.com/user-attachments/assets/eb92d024-a13b-49c1-9c5f-97989f4e2918)

(My Powershell ISE log) 



![image](https://github.com/user-attachments/assets/3634ba09-1182-4eb1-b761-c9bba5833f5b)
Logs are being exported to Log Analytics workspace on Microsoft Azure with the raw data organized with a custom query for readability



Using Microsoft Sentinel as my SIEM, I create a workbook for my world map.

![image](https://github.com/user-attachments/assets/87320945-2517-43b4-be4b-e7983471f5b5)


This World Map shows where in the world attacks are coming from, according to the geo data from the logs. 



