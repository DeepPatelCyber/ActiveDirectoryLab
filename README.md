<h1>Active Directory Enterprise Environment Homelab</h1>

 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)

<h2>Description</h2>
Active Directory, developed by Microsoft, is a powerful directory service that provides centralized user management, security tools, and simplified administrative tasks within a network enterprise environment. It is vastly used in many organizations within their computerized infrastructure and networks. Knowledge of Windows Server and Active Directory is vital in terms of information technology.  
<br />
<br />

In this active directory lab, the goal is to create, simulate, and administrate an active directory domain at a similar scale to that of an enterprise environment. Since it is a virtual environment, virtual NICs will need to be managed correctly in order to allow for connectivity and proper routing of traffic. Then further services and features such as NAT and DHCP can be utilized to help with the administration of the environment. A PowerShell script was created and utilized in order to populate the domain with over 1000 users to help further simulate the scale of the project. Client machines were made for users to log in and authenticate against the domain.   

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Windows Server 2019 </b>

<h2> High-Level Diagram of Active Directory lab:</h2>

<p align="center">
 <br/> 
<img src="https://i.imgur.com/PIgcSCz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
 
The diagram above outlines the main components of the lab:  <br/>
- Oracle Virtual Box, with Windows Server and Windows 10 Virtual machines
- DC (Server 19) with two virtual NICs, one for the internal network, and one for the public internet
- IP addressing Scheme: 172.16.0.1/24
- Services and Features: Active Directory Domain Services, Remote Access Server (RAS), Network Address Translation (NAT), and Dynamic Host Configuration Protocol (DHCP)

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
