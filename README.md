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


<h3> Creating the Domain Controller Machine on Virtual Box</h3>
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


<h3> Configuring the Domain Controller: Routing and hostname</h3>
<br/>


- Now with the domain controller being installed and being a fully operational virtual machine, we can now configure and add new roles and features to support the lab diagram and enterprise environment.
- the first step is to configure the internal network adapter, to provide interconnectivity in the network.
- within Windows server, open change adapter options


<p align="center">
 <br/> 
<img src="https://i.imgur.com/gOLqVEg.png"/> 
<br/>This screenshot shows the the two adapters made during our VM creation, with them being distinctly named

- We now need to assign an IP addressing scheme onto the internal VNIC adapter. by right clicking and selecting properties on the internal VNIC, we can fill in the following information.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/DOAUGkO.png"/> 
<br/>This screenshot shows the internal adapter properties and IP addressing scheme. 

- The default gateway will be left blank, as the DC itself will be the default gateway. And the DNS server will be pointing to the DC itself again, as for later in the lab, active directory will be installed along with DNS services.
- The next step is to rename the pc to help with future identification and troubleshooting.
- by right-clicking the Windows start menu, then clicking system, and selecting rename this PC, we can enter a new hostname. In our case, the hostname was changed to DC for simplicity, and for following the diagram naming conventions.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/oe9b1Mk.png"/> 
<br/>This screenshot shows the renaming process of the machine

<h3> Configuring the Domain Controller: Adding Active Directory Domain Services</h3>
<br/>

- With hostname and routing configured on the DC, we can now start adding roles and features to start implementing Active Directory.
- On the server manager dashboard, click add roles and features, select the DC, choose to install Active Directory Domain Services, and confirm the installation.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/zUw9Avi.png"/> 
<br/>This screenshot shows the summary of options selected for adding AD DS.

- after AD DS has been installed, the server must be promoted to a domain controller for post-deployment configuration.


<p align="center">
 <br/> 
<img src="https://i.imgur.com/F5N5aP0.png"/> 
<br/>This screenshot shows the option to promote the server to a domain controller.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/ZgzDC09.png"/> 
<br/>This screenshot shows the summary of options within the Active Directory Domain Services Configuration Wizard.

- After configuration and reset of the server, the active directory domain services feature should be added

<p align="center">
 <br/> 
<img src="https://i.imgur.com/pf9FULw.png"/> 
<br/>This screenshot shows the new login prompt for the server highlighting the domain name as the prefix to the Adminstrator account.

 <h3> Adding a Dedicated Admins Organizational Unit (OU) </h3>

 - By adding this OU it will make the categorization and management of different types of users easier to manage as a systems administrator working in this domain.
 - In server manager, browse to manage | active directory users and computers | mydomain.com.
 - right click mydomain.com and select new organizational unit, and name it accordingly

<p align="center">
 <br/> 
<img src="https://i.imgur.com/rxNM7sR.png"/> 
<br/>This screenshot shows the _Admins OU being created within our domain.

- Now we can create a user within this OU and give them admin permissions.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/bdEM3Om.png"/> 
<br/>This screenshot shows our personal user being created within the OU.

- Now we must add this user to the domain admins group in active directory to actually give them admin permissions.
- Right-click the user and click properties, and click members of.
- add them to domain admins by name-checking, then click apply.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/64xpocW.png"/> 
<br/>This screenshot shows our user being added to a member of the default admin group in active directory.

<h3> Configuring the Domain Controller: Adding RAS and NAT</h3>
<br/>

- The purpose of RAS and NAT is to help clients of the domain have a virtual private network while having access to the internet. This will allow all private IP addresses to be translated out to public IP address when trying to communicate to the internet.
- Again by going to manage, and add roles and features, we can begin the process of installing RAS and NAT.

<p align="center">
 <br/> 
<img src="https://i.imgur.com/oKnztcC.png"/> 
<br/>This screenshot shows all of the following options selected when installing RAS/NAT. 


- Now to manage this new feature, we can navigate to tools | routing and remote access | right-clicked DC local | configure
- In the configuration wizard, selected the nat option
<p align="center">
 <br/> 
<img src="https://i.imgur.com/bEYTZ9e.png"/> 
<br/>This screenshot shows the NAT option that needs to be selected. 
  
- Selected the public NIC interface
<p align="center">
 <br/> 
<img src="https://i.imgur.com/4HuaW1M.png"/> 
<br/>This screenshot shows the the public interface we created earlier being selected. 

- Selected finish 
- Now that RAS and NAT has been configured properly, client machines will be able to access the internet, however DHCP still needs to be configured for proper ip adressing in the private address space.


<h3> Configuring the Domain Controller: Adding DHCP</h3>
<br/>

- Dynamic Host Configuration Protocol (DHCP) will help in the process of confiuring this enviornment and making all machines have proper netowrking. DHCP automatically assigns IP address and other communciation parameters to specified devies to specified address spaces. 

<!--
 ```diff
 
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
