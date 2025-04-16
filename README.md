<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Understanding Network File Shares & User Permissions</h1>
This tutorial will walk through how to configure network file share permissions and how they affect users in Active Directory.<br/>

<h2>Prerequisites</h2>
Configure an on-premises Active Directory within Azure VMs using my previous project as a reference --> https://github.com/BrianRivera22/configure_AD/blob/main/README.md

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

1) 

2) 

3) 


<h2>Deployment and Configuration Steps</h2>

<h4>1. </h4>
<p>
<img src="https://github.com/BrianRivera22/network_file_shares/blob/main/Network%20File%20Shares%20%26%20User%20Permissions/1.png"/>
</p>
<p>
In dc-1, login as an admin and create four folders in the C-drive.

Right click on each folder and click properties. Within properties, click share and configure the share settings

Folder: “read-access”, Group: “Domain Users”, Permission: “Read” Folder: “write-access”, Group: “Domain Users”, Permissions: “Read/Write” Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write” We will skip the "accounting" folder for now.

<p>
<img src="https://github.com/BrianRivera22/network_file_shares/blob/main/Network%20File%20Shares%20%26%20User%20Permissions/2.png"/>
</p>
<p>
Within client-1, log in as any user and go to Start -> Run -> \\dc-1

This will open the shared folders and notice that they the permissions are enforced.

<p>
<img src="https://github.com/BrianRivera22/network_file_shares/blob/main/Network%20File%20Shares%20%26%20User%20Permissions/3.png"/>
</p>
<p>
Back in dc-1, in Active Directory Users and Computers, create an OU named "_GROUPS" (You can skip this step, but it's good practice for organizational purposes) 

Create a new group named "ACCOUNTANTS" within "_GROUPs"

<p>
<img src="https://github.com/BrianRivera22/network_file_shares/blob/main/Network%20File%20Shares%20%26%20User%20Permissions/4.png"/>
</p>
<p>
Here, I am showing two different ways to make a user (ben.cab)


  
On the right, within "_EMPLOYEES", you can also make a user a member of the group "ACCOUNTANTS"

<p>
<img src="https://github.com/BrianRivera22/network_file_shares/blob/main/Network%20File%20Shares%20%26%20User%20Permissions/5.png"/>
</p>
<p>
Back in dc-1, go to the "accounting" only folder and change the share properties. Add the group "ACCOUNTANTS" in the share settings.

Back in client-1, log in as the user that was added to the ACCOUNTANTS group and access the accounting folder


<b>This concludes the tutorial!</b>
