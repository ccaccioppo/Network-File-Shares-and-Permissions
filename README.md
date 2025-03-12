# Network-File-Shares-and-Permissions

<p align="center">
<img src="https://i.imgur.com/AeiqMDZ.png" alt="Traffic Examination"/>
</p>

<h1>Network-File-Shares-and-Permissions</h1>

In this lab, we will share resources over a network by creating files and configuring permissions to allow read, write, or deny access for individual users and groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Domain Controller/Client Machine)
- Remote Desktop
- Shared Network Files

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- A Virtual Machine used as a Domain Controller with AD DS
- A Virtual Machine used as a Client 

<h2>Lab Steps</h2>

<p>
<img src="https://i.imgur.com/IX7eI1M.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log into DC-1 using the domain admin account (mydomain.com\ken_admin) and into Client-1 as a normal user (mydomain<someuser>). On DC-1, navigate to the C:\ drive and create four folders named read-access, write-access, no-access, and accounting.
</p>
<br />

<p>
<img src="https://i.imgur.com/YpWvuuh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, configure the following permissions and share the folders:
For the read-access folder, assign the Domain Users group the Read permission.
For the write-access folder, assign the Domain Users group Read/Write permissions.
For the no-access folder, assign the Domain Admins group Read/Write permissions.
Skip setting permissions for the accounting folder for now.  
</p>
<br />

<p>
<img src="https://i.imgur.com/mJLXlBj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Uuy43Na.pngg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, log in as a normal user and open File Explorer. In the search bar, type \\dc-1 to view the shared folders. Attempt to access each folder:
As a normal user, you should be able to open the read-access folder but only view its contents (no modifications allowed).
You should have full access to the write-access folder, allowing you to create, edit, and delete files.
Access to the no-access folder will be denied, as it is restricted to Domain Admins.
</p>
<br />

<p>
<img src="https://i.imgur.com/xsdCaQp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, open Active Directory Users and Computers (ADUC) and create a new organizational unit (OU) named _GROUPS. Within the _GROUPS OU, create a new security group named ACCOUNTANTS.
</p>
<br />

<p>
<img src="https://i.imgur.com/cZo9Poi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Return to ADUC on DC-1 and add some domain users to the newly created ACCOUNTANTS group. To do this, right-click the ACCOUNTANTS group, select Properties, navigate to the Members tab, and add the desired users. Also give the ACCOUNTANTS group read/write permissions for the accounting file now. 
</p>
<br />

<p>
<img src="https://i.imgur.com/HzkNmDO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Restart and then log in to the Client1 VM as the user you added to the ACCOUNTANTS group. Navigate to the shared folder on DC-1 by typing \\dc-1 in File Explorer. Attempt to access the accounting folder. It should now be accessible since the user is part of the group with permissions.
</p>
<br />
