<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

<h3>Setup Domain Controller in Azure</h3>

-------------------------------

<h4>Create a Resource Group</h4>
<p>Create a Virtual Network and Subnet</p>
<p>Create the Domain Controller VM (Windows Server 2022) named “DC-1”</p>
<p>- Username: labuser</p>
<p>- Password: Cyberlab123!</p>
<p>After VM is created, set Domain Controller’s NIC Private IP address to be static</p>
<p>Log into the VM and disable the Windows Firewall (for testing connectivity)</p>

<h3>Setup Client-1 in Azure</h3>

------------------------------------

<h4>Create the Client VM (Windows 10) named “Client-1”</h4>
<p>- Username: labuser</p>
<p>- Password: Cyberlab123!</p>
<p>Attach it to the same region and Virtual Network as DC-1</p>
<p>After VM is created, set Client-1’s DNS settings to DC-1’s Private IP address</p>
<p>From the Azure Portal, restart Client-1</p>
<p>Login to Client-1</p>
<p>Attempt to ping DC-1’s private IP address</p>
<p>Ensure the ping succeeded</p>
<p>From Client-1, open PowerShell and run ipconfig /all</p>
<p>The output for the DNS settings should show DC-1’s private IP Address</p>

<h3>Install Active Directory</h3>

------------------------------------\

Login to DC-1 and install Active Directory Domain Services
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)
Restart and then log back into DC-1 as user: mydomain.com\labuser

<>h3Create a Domain Admin user within the domain</h3>

------------------------------------

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
Create a new OU named “_ADMINS”
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin” / Cyberlab123!
Add jane_admin to the “Domain Admins” Security Group
Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”
User jane_admin as your admin account from now on


Join Client-1 to your domain (mydomain.com)

