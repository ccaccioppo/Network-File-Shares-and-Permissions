# Network-File-Shares-and-Permissions

<p align="center">
<img src="https://i.imgur.com/AeiqMDZ.png" alt="Traffic Examination"/>
</p>

<h1>Network-File-Shares-and-Permissions</h1>

In this lab, we’ll explore how to share resources across a network. We’ll create files and set up permissions to control access, allowing us to grant read or write access to specific users and groups, or even restrict access entirely. <br />

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
First, log in to DC-1 using the domain admin account (mydomain.com\ken_admin). Then, log in to Client-1 as a regular user (mydomain<someuser>). Once you're on DC-1, go to the C:\ drive and create four new folders: read-access, write-access, no-access, and accounting.
</p>
<br />

<p>
<img src="https://i.imgur.com/YpWvuuh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
-On DC-1, set up the following permissions and share the folders accordingly:

-For the read-access folder, grant the Domain Users group Read permissions.

-For the write-access folder, give the Domain Users group Read/Write permissions.

-For the no-access folder, assign Read/Write permissions exclusively to the Domain Admins group.

-As for the accounting folder, we’ll hold off on setting permissions for now.

</p>
<br />

<p>
<img src="https://i.imgur.com/mJLXlBj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/Uuy43Na.pngg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On Client-1, log in with a standard user account and open File Explorer. In the search bar, type \\dc-1 to browse the shared folders. Try accessing each folder to test the permissions:

-As a regular user, you should be able to open the read-access folder and view its contents, but you won’t be able to make any changes.

-You should have full control over the write-access folder, meaning you can create, edit, and delete files as needed.

-When attempting to open the no-access folder, you’ll be denied entry since it’s restricted to Domain Admins only.
</p>
<br />

<p>
<img src="https://i.imgur.com/xsdCaQp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, launch Active Directory Users and Computers (ADUC). Create a new organizational unit (OU) called _GROUPS. Inside this _GROUPS OU, set up a new security group named ACCOUNTANTS.
</p>
<br />

<p>
<img src="https://i.imgur.com/cZo9Poi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Head back to ADUC on DC-1 and add a few domain users to the newly created ACCOUNTANTS group. To do this, simply right-click the ACCOUNTANTS group, choose Properties, go to the Members tab, and include the users you want. While you’re there, don’t forget to grant the ACCOUNTANTS group read/write permissions for the accounting file as well. 
</p>
<br />

<p>
<img src="https://i.imgur.com/HzkNmDO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Restart the Client1 VM and log in using the account you added to the ACCOUNTANTS group. Open File Explorer and type \\dc-1 in the address bar to access the shared folders on DC-1. Try opening the accounting folder. Since the user is now part of the group with the correct permissions, you should be able to access it without any issues.
</p>
<br />
