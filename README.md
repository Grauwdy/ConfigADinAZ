<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Configurations in Azure</h1>
This lab serves as a sequel to the previous one where I set up Active Directory and established a domain controller. Now, the focus shifts to configuring Active Directory, facilitating the integration of a client into the domain, and crafting user accounts. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (21H2)

<h2>Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/PGR0bEi.png" height="80%" width="80%" alt="Configuration Steps"/>
<img src="https://i.imgur.com/WiCs7bJ.png" height="80%" width="80%" alt="Configuration Steps"/>
</p>
<p>With Active Directory now on the domain controller VM, let's create new Organizational Units (OUs) and Users:</p>

<ol>
  <li>Open the Active Directory Users and Computers console.</li>
  <li>Right-click on the domain (like alaingarciadomain.com) and create a new Organizational Unit (OU). I made two: _EMPLOYEES and _ADMINS, with a naming scheme for a future PowerShell script.</li>
  <li>Inside the _ADMINS OU, create a new User, say, alain garcia. This user gets admin privileges via a Security Group.</li>
  <li>To grant admin powers, right-click on the user, go to Properties, click Member Of, then Add to join the relevant security group. In my case, alain joins the Domain Admins group.</li>
</ol>

<p>Moving forward, changes will happen through Alain's account. Logging off as labuser and logging in as alain_admin from now on. Let the admin tasks begin!</p>
<br />

<p>
<img src="https://i.imgur.com/6Y5WonS.png" height="80%" width="80%" alt="Configuration Steps"/>
</p>
<p>
Before the client can join the domain, it is important to configure the DNS settings first. The DNS server has to pointing to the domain controller's private IP address. On the Azure portal, open the Networking tab and click on Network Interface. In the DNS servers, enter the domain controller's private IP address and save the changes. Restart the client VM in order to ensure the DNS changes are saved. 
</p>
<br />

<p>
<img src="https://i.imgur.com/tX4khLw.png" height="80%" width="80%" alt="Configuration Steps"/>
<img src="https://i.imgur.com/z1kq1Gv.png" height="80%" width="80%" alt="Configuration Steps"/>
<img src="https://i.imgur.com/DkPUJNR.png" height="80%" width="80%" alt="Configuration Steps"/>
</p>
<p>Now, let's get the client VM on board and join the domain. Here's the process:</p>

<ol>
  <li>In the System menu of the client VM, click on "Rename this PC (advanced)" and then "Change."</li>
  <li>Enter the domain and necessary credentials to allow the client to join the domain. For this lab, I'm logging in as Jane Doe.</li>
  <li>Ensure that the login credentials are input within the context of the domain path.</li>
  <li>The client should now be successfully part of the domain.</li>
</ol>

<p>Check on the domain controller, and the client should now appear in the Computers section within the Active Directory Users and Computers panel. The integration is complete!</p>

<br />

<p>
<img src="https://i.imgur.com/nkPK6ny.png" height="80%" width="80%" alt="Configuration Steps"/>
</p>
<p>Before users in the domain can utilize the client computer, Remote Desktop needs to be enabled for non-administrative users. Follow these steps:</p>

<ol>
  <li>While logged in as the administrator (in my case, Jane), open System Properties.</li>
  <li>Click on Remote Desktop and select users who can remotely access this PC.</li>
  <li>Allow Domain Users access to Remote Desktop.</li>
</ol>

<p>Now, non-administrative users can log in to Client-1 using Remote Desktop. Typically, a Group Policy can achieve the same result and facilitate changes across multiple systems simultaneously. However, for the purposes of this lab, we won't be using Group Policy for this specific adjustment.</p>

<br />

<p>
<img src="https://i.imgur.com/HrI6BTq.png" height="80%" width="80%" alt="Configuration Steps"/>
<img src="https://i.imgur.com/c7LaN48.png" height="80%" width="80%" alt="Configuration Steps"/>
</p>
<p>
Creating users can be done manually or through the use of a script. For this lab, I will be using a PowerShell script. The PowerShell script can be found <a href="https://github.com/AsiaPonder001/BunchofUsers/blob/main/README.md?plain=1)"> here. </a> On the domain controller, open PowerShell ISE as an administrator (and make sure you are logged in with an admin account on the domain controller). Create a new file and paste the script into ISE console. Run the script and observe the accounts being created. 
</p>
<br />

<p>
<img src="https://i.imgur.com/4ELhiF6.png" height="80%" width="80%" alt="Configuration Steps"/>
</p>
<p>
After creating the users, Client-1 can now be signed in as one of the new users that were created from the PowerShell script. Pick a name and simply sign in to the client with the context of the domain. In my case, it is alaingarciadomain.com\gadusu.woker.
</p>
<br />

<h2>Lessons Learned</h2>

Completing this lab taught me the ropes of setting up Active Directory and smoothly incorporating clients into the domain. Creating users and handling permissions underscored the practical side of Active Directory, showing that it's not as complex as it may appear during menu navigation.

This lab serves as a springboard for me to explore DNS settings in more depth and witness file permissions in action in upcoming labs. I'm eager to tackle these topics hands-on and deepen my understanding of the broader system administration landscape.






