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

------------------------------------

<p>Login to DC-1 and install Active Directory Domain Services</p>
<p>Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is)</p>
<p>Restart and then log back into DC-1 as user: mydomain.com\labuser</p>

<h3>Create a Domain Admin user within the domain</h3>

------------------------------------

<p>In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”</p>
<p>Create a new OU named “_ADMINS”</p>
<p>Create a new employee named “Jane Doe” (same password) with the username of “jane_admin” / Cyberlab123!</p>
<p>Add jane_admin to the “Domain Admins” Security Group</p>
<p>Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin”</p>
<p>User jane_admin as your admin account from now on</p>


<h3>Join Client-1 to your domain (mydomain.com)</h3>

------------------------------------

<p>Login to Client-1 as the original local admin (labuser) and join it to the domain (computer will restart)</p>
<p>Login to the Domain Controller and verify Client-1 shows up in ADUC</p>
<p>Create a new OU named “_CLIENTS” and drag Client-1 into there</p>


<h3>Setup Remote Desktop for non-administrative users on Client-1</h3>

------------------------------------

<p>Log into Client-1 as mydomain.com\jane_admin</p>
<p>Open system properties</p>
<p>Click “Remote Desktop”</p>
<p>Allow “domain users” access to remote desktop</p>
<p>You can now log into Client-1 as a normal, non-administrative user now</p>
<p>Normally you’d want to do this with Group Policy that allows you to change MANY systems at once (maybe a future lab)</p>


<h3>Create a bunch of additional users and attempt to log into client-1 with one of the users</h3>

------------------------------------

<p>Login to DC-1 as jane_admin</p>
<p>Open PowerShell_ise as an administrator</p>
<p>Create a new File and paste the contents of the script into it</p>
<p>Run the script and observe the accounts being created</p>
<p>When finished, open ADUC and observe the accounts in the appropriate OU　(_EMPLOYEES)</p>
<p>attempt to log into Client-1 with one of the accounts (take note of the password in the script)</p>


<h3>Dealing with Account Lockouts</h3>

------------------------------------

<p>Get logged into dc-1</p>
<p>Pick a random user account you created previously</p>
<p>Attempt to log in with it 10 times with a bad password</p>

<p>Configure Group Policy to Lockout the account after 5 attempts:</p>



<p>Attempt to log in with it 6 times with a bad password</p>

<p>Observe that the account has been locked out within Active Directory</p>
<p>Unlock the account</p>
<p>Reset the password</p>
<p>Attempt to login with it</p>

<h3>Enabling and Disabling Accounts</h3>

------------------------------------

<p>Disable the same account in Active Directory</p>
<p>Attempt to login with it, observe the error message</p>
<p>Re-enable the account and attempt to login with it.</p>

<h3>Observing Logs</h3>

------------------------------------

<p>Observe the logs in the Domain Controller</p>
<p>Observe the logs on the client Machine</p>

