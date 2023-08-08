<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Starting this lab by creating two virtual machines (VMs) in Microsoft Azure; one domain controller (DC-1) (Windows Server 2022) and one client PC (Client-1) (Windows 10). Established both VMs on the same virtual network. Assigned a static IP address and enabled ICMPv4 inbound traffic rules on the domain controller. Next, ensured that we are able to ping the domain controller from the client PC. Now that a connection has been established between both VMs, we are able to proceed with installing Active Directory on DC-1. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Installed Active Directory on DC-1. Once installed and a domain name has been created (I named the domain 'mydomain.com'), go to the 'Active Directory Users and Computers' and create two organizational units titles ' _EMPLOYEES' and '_ADMINS'. Created a new admin account by adding a new user under the '_ADMINS' folder (I just used my own name). Go to the account properties and make the user a member of the 'Domain Admins' security group. After that, log out of DC-1 and log back in using the new admin account (for example, the login I created was mydomain.com\d-wells).


The next step was to join Client-1 to the domain. But before that, because Microsoft Azure VMs were used for this lab, the DNS server for Client-1 had to be changed to DC-1's private IP address. Once the DNS settings were changed, we are able to go into Client-1 and join it to the domain. Log into Client-1 as the admin user that was created on DC-1. This confirms that all domain user accounts that are created will now be able to log into Client-1.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Logged into DC-1 on the admin account and ran a script in Powershell ISE to create 1000 user accounts with a set password. Then, used the log in credentials of a few scripted user accounts to log into Client-1. 

*On one instance of this lab, I ran into an error where Client-1 would only allow administrator accounts to remote log-in but not other users. I resolved this by: Log onto admin account -> right click Start -> Computer Management -> Local Users and Groups -> Groups -> double click Remote Desktop Users -> Add 'Domain Users'. Here's a good guide on that process: https://support.ncomputing.com/portal/en/kb/articles/how-to-add-a-new-user-and-configure-remote-desktop-user-s-group-settings-on-windows-server-2016
</p>
<br />
