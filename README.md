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
<img src="https://i.imgur.com/PIgcSCz.png" height="80%" width="80%" />
<br />
<br />
 
The diagram above outlines the main components of the lab:  <br/>
- Oracle Virtual Box, with Windows Server and Windows 10 Virtual machines
- DC (Server 19) with two virtual NICs, one for the internal network, and one for the public internet
- IP addressing Scheme: 172.16.0.1/24
- Services and Features: Active Directory Domain Services, Remote Access Server (RAS), Network Address Translation (NAT), and Dynamic Host Configuration Protocol (DHCP)

<h2> Procedures:</h2>

<h3> Installation of Oracle Virtual Box</h3>

If Virtual Box is not already installed onto your home-lab equipment, installation of this software is key due to the nature of virtualizing the environment. 



1. navigate to the official website of Oracle Virtual Box and install Virtual Box and Virtual Box extension pack.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/LhKecD8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />


<h3> Installation of Operating System iso Files</h3>

- Navigate to the official Microsoft page to retrieve the Windows 10 iso file. https://www.microsoft.com/en-us/software-download/windows10

<p align="center">
 <br/> 
<img src="https://i.imgur.com/PdVTqaB.png" height="80%" width="80%"/> 

- When prompted, select, "Create installation media for another PC."

<p align="center">
 <br/> 
<img src="https://i.imgur.com/LH5jQPJ.png" height="80%" width="80%"/> 


 <br/> 
 
- Navigate to the official Microsoft page to retrieve the Windows Server 2019 iso file and select the os and iso options just like with the previous steps. https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019


<h3> Creating the Virtual Machines on Virtual Box</h3>
<br/>

- With all items installed, we can now create the environment.
- With Oracle Virtual Box opened, we can click the "New" button and start to create our virtual machines.
- Let's start with the creation of the Windows server 2019 VM.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/T4QRuVn.png"/> 
<br/>The VM options should appear similar to this, given your home lab resources

- according to the diagram and goals of this lab, the Windows Server VM needs two virtual NICs to be configured to allow for proper internal traffic flow and internet connectivity.
- Two adapters (virtual NICs) need to be configured on this VM, within the adapter settings of the machine.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/CeX0WJk.png"/> 
<br/>This screenshot shows the settings of adapter 1 and it being attacked to NAT, as it is the public-facing VNIC 

<p align="center">
 <br/> 
<img src="https://i.imgur.com/d2QLAxq.png"/> 
<br/>This screenshot shows the settings of adapter 2 and it being attacked to the internal network, as it is the internal-facing VNIC 

- Now the Windows Server 2019 VM can be powered on, and the OS can be installed with default settings. 
 
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
