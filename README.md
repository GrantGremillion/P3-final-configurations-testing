<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Final Configurations + Testing Active Directory Features</h1>
This tutorial will be for finalizing some AD configurations and experimenting with some of it's features<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Configuring Lockout Group Policy
- Lockout Policy Testing
- Reseting User Passwords
- Enabling/Disabling User Accounts


<h2>Configuring Lockout Group Policy</h2>

![image](https://github.com/user-attachments/assets/553278c7-2301-4d54-bdde-132faf7929f1)


<p>
We will first need to make a configuration change that will lock users out of their account if they fail too many password attempts. To do this, we will need to access the Group Policy Management Console. We can get their by right clicking start > Run and typing gpmc.msc > Ok. Expand the tabs on the left until you find the Default Domain Policy under Forest > Domains > mydomain.com. Right click it and then Edit. Now, find the Account lockout policy through Policies > Windows Settings > Security Settings > Account Policies. 
</p>
<br />

![image](https://github.com/user-attachments/assets/949da7b0-849d-4d48-a05c-94824c96e153)

<p>
Edit the values on the right side of the window to match the following:

Account lockout duration : 30 minutes

Account lockout threshold: 5 invalid logon attempts

Reset account lockout counter after: 10 minutes
</p>
<br />

<h2>Lockout Policy Testing</h2>

![image](https://github.com/user-attachments/assets/c79ce139-2dfb-477a-9ec8-4edcaaf98329)

<p>
In order for the changes we made to take effect, we need to log into the client VM using admin credentials anf then open the command prompt and run gpupdate /force. Once that has finished, we can logout of the vm and attempt to log back in as a regular user but purposfully use the wrong password over and over again until we are locked out. You should eventually get a message that looks like this: 
</p>
<br />

![image](https://github.com/user-attachments/assets/a301283e-ca63-48d3-866c-a36ece925191)


<p>
Now, in order to unlock the account, we can go back to the domain controller vm and unlock the users account from within the Active Directory Users and Computers Window. Double click the user and under the Account tab, check the box that says "Unlock account" > Apply > Ok. When we try to log back into the client vm with the user account, we should be able to log in again. 
</p>
<br />

<h2>Reseting User Passwords</h2>

![image](https://github.com/user-attachments/assets/79656941-fb05-49b9-9459-967544575493)


<p>
The user's password can also be reset if they forget it by right clicking the user and selecting reset password. Try changing the user's password and re-logging back in with the new password now.
</p>
<br />

<h2>Enabling/Disabling User Accounts</h2>

<p>
Another feature of admins is the ability to enable and disable user accounts. This can be done by simply right clicking the user and selecting enable/disable account. This feature is usually used in a case where someone retires from the company or is fired. Now, try to login to the non-admin user account after disabling the account. You should see a message that says the account is disabled:
</p>
<br />

![image](https://github.com/user-attachments/assets/7cfbbbd7-aae9-43e6-9dd6-51fe9d602530)

<p>
Lastly, as an admin in the domain controller VM, re-enable the account again and try to log back in as the user. 
</p>
<br />

<p>
Congratulations! You have finished the walkthrough for setting up Active Directory in an Azure Virtual Enviornment.
</p>
<br />

