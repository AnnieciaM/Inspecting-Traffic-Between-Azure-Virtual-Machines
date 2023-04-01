<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1 Create File Shares
- Step 2 Set Permissions
- Step 3 Attempt to access file shares
- Step 4 Create Security Groups

<h2>Actions and Observations</h2>
STEP 1 - CREATE FILE SHARES
<p>
<img src="https://i.imgur.com/htYYeNk.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From DC-1 VM open the C-drive create new folders called Read-Access, Write-Access, and No-Access.

</p>
<br />

STEP 2 - SET PERMISSIONS
<p>
<img src="https://i.imgur.com/https://i.imgur.com/JbF7c3Z.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once new folders are created, right click on each one, properties, sharing and give them permissions within the share folder. (Read-Access- group- domain users- read only, Write-Access- group- domain users- read/write, and No-Access- group- domain admins- read/write).

</p>
<br />
STEP 3 - ATTEMPT TO ACCESS FILE SHARES
<p>
<img src="https://i.imgur.com/L9h5SHR.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to Client-1 VM as Bad.hega and type \\dc-1 in file explorer. That will show you all the shared files that were created in DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/kMwEF97.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Clicked on No-Access folder to check permissions. Windows will not allow access to the folder. Permissions are working correctly here. 
</p>
<br />

<p>
<img src="https://i.imgur.com/HiysZG8.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After clicking Read-Access folder and trying to create a text file this notification popped up. Permissions set to only read and not write or create folders/documents. The permissions are working correctly. 
</p>
<br />

<p>
<img src="https://i.imgur.com/ixGKFiN.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Clicked on the Write-Access folder. Created a text file and named it test. The permissions are working correctly for this folder. This folder has read & write permissions. 
</p>
<br />

STEP 4 - CREATE SECURITY GROUP
<p>
<img src="https://i.imgur.com/0congzZ.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/fapYMKp.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
From DC-1 Active Directory Users and Computers right click mydomain.com, new then organizational unit. Then create a new unit called _SECURITY_GROUPS.
</p>
<br />

<p>
<img src="https://i.imgur.com/vfq2Zvj.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/XNMUhux.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once _SECURITY_GROUPS is created right click, new and then group. Create a new group called ACCOUNTANTS.
</p>
<br />

<p>
<img src="https://i.imgur.com/6EFifqm.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right click on ACCOUNTANTS, share then give ACCOUNTANTS permission to read and write.
</p>
<br />

<p>
<img src="https://i.imgur.com/qVs2chD.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Switch back to Client-1 VM and see if they are allowed access but bad.hega doesn't have access. The permissions are correct.
</p>
<br />

<p>
<img src="https://i.imgur.com/EZglXYb.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Go back to DC-1 VM and click on ACCOUNTANTS and add bad.heda as a user. Bad.hega the user logged in to Client-1 VM now has access to the accounting share files.
</p>
<br />

<p>
<img src="https://i.imgur.com/efBM6Vd.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Switched back to Client-1 VM and as you can see Bad.heda now can open the accounting file. Permissions are correct.
</p>
<br />
