# Active Directory Runbook

**Name of the new hire:** Toby Flenderson  
**Role at StackFull Software:** Social Media Associate  
**Department:** HR

---

This runbook outlines a series of tasks related to user and group management, file sharing, OU creation, GPO configuration, and system monitoring for a Windows domain environment.

---

## 🧩 Full Setup Process

### Join the Computer to the Domain
Log in to the computer using the username `administrator` and the password `Pa$$w0rd`.

Open the Control Panel and navigate to System and Security > System.  
![Step 1 - Control Panel](Active-Directory-Runbook-Images/image1.png)

Click on “Change settings” next to the computer name.  
![Step 1 - Change settings](Active-Directory-Runbook-Images/image2.png)

In the System Properties window, click on the “Change” button.  
![Step 1 - System Properties](Active-Directory-Runbook-Images/image3.png)

Select the “Domain” option, enter `contoso.com`, and click “OK”.  
![Step 1 - Enter Domain](Active-Directory-Runbook-Images/image4.png)

Provide the domain administrator credentials when prompted.  
![Step 1 - Credentials](Active-Directory-Runbook-Images/image5.png)

Restart the computer.  
![Step 1 - Restart](Active-Directory-Runbook-Images/image6.png)

---

### Create a User for the New Hire
Log in to the server and open **Active Directory Users and Computers**.  
![Step 2 - ADUC Search](Active-Directory-Runbook-Images/image7.png)

Click `contoso.com`, then the `Users` folder.  
![Step 2 - Domain Selected](Active-Directory-Runbook-Images/image8.png)

Create a user for Toby Flenderson.  
![Step 2 - Users Folder](Active-Directory-Runbook-Images/image9.png)

Enter account details and a password.  
![Step 2 - Account Details](Active-Directory-Runbook-Images/image10.png)

Click “Finish”.  
![Step 2 - Finish](Active-Directory-Runbook-Images/image11.png)

---

### Create a Group for the Department
Open `Computer Management > Local Users and Groups > Groups`.  
![Step 3 - Local Users and Groups](Active-Directory-Runbook-Images/image12.png)

Right-click to create a new group named `HR`.  
![Step 3 - New Group](Active-Directory-Runbook-Images/image13.png)

Set the group name and confirm.  
![Step 3 - Group Name](Active-Directory-Runbook-Images/image14.png)

Open the group and add the new user.  
![Step 3 - Group Properties](Active-Directory-Runbook-Images/image15.png)  
![Step 3 - Add User](Active-Directory-Runbook-Images/image16.png)  
![Step 3 - Confirm Add](Active-Directory-Runbook-Images/image17.png)

---

### Create a Department Share
Open File Explorer and navigate to a suitable location.  
![Step 4 - Explorer](Active-Directory-Runbook-Images/image18.png)  
![Step 4 - Location](Active-Directory-Runbook-Images/image19.png)

Right-click the folder > `Properties > Sharing > Advanced Sharing`.  
![Step 4 - Properties](Active-Directory-Runbook-Images/image20.png)  
![Step 4 - Sharing Tab](Active-Directory-Runbook-Images/image21.png)

Assign the share name and permissions.  
![Step 4 - Share Name](Active-Directory-Runbook-Images/image22.png)  
![Step 4 - Permissions](Active-Directory-Runbook-Images/image23.png)  
![Step 4 - Share Created](Active-Directory-Runbook-Images/image24.png)

Create `test.txt` inside the share.  
![Step 4 - Test File](Active-Directory-Runbook-Images/image25.png)

---

### Create an Organizational Unit (OU)
Open ADUC.  
![Step 5 - ADUC](Active-Directory-Runbook-Images/image26.png)

Right-click the domain > `New > Organizational Unit`.  
![Step 5 - New OU](Active-Directory-Runbook-Images/image27.png)  
![Step 5 - OU Name](Active-Directory-Runbook-Images/image28.png)

Move user, group, and computer objects into the OU.  
![Step 5 - Move Objects](Active-Directory-Runbook-Images/image29.png)

Create or link a GPO to the OU.  
![Step 5 - GPO Settings](Active-Directory-Runbook-Images/image30.png)  
![Step 5 - Link GPO](Active-Directory-Runbook-Images/image31.png)  
![Step 5 - Confirm GPO](Active-Directory-Runbook-Images/image32.png)

---

### Apply Group Policy Configuration
#### Display a Startup Message
Open GPMC.  
![Step 6 - Open GPMC](Active-Directory-Runbook-Images/image33.png)

Navigate to `Computer Configuration > Windows Settings > Security Options`.  
![Step 6 - Security Options](Active-Directory-Runbook-Images/image34.png)

Enable UAC.  
![Step 6 - UAC Enabled](Active-Directory-Runbook-Images/image35.png)  
![Step 6 - Apply GPO](Active-Directory-Runbook-Images/image36.png)

#### Restrict CMD
Go to `User Configuration > Administrative Templates > System`.  
![Step 6 - Admin Templates](Active-Directory-Runbook-Images/image37.png)  
![Step 6 - Block CMD](Active-Directory-Runbook-Images/image38.png)

#### Add Logon Script
Navigate to `User Configuration > Scripts (Logon/Logoff)` > `Logon`.  
![Step 6 - Logon Script](Active-Directory-Runbook-Images/image39.png)

Click `Show Files`, add `.bat` file.  
![Step 6 - Script Folder](Active-Directory-Runbook-Images/image40.png)

Click `Add` and choose script.  
![Step 6 - Add Script](Active-Directory-Runbook-Images/image41.png)

#### Disable the Run Menu
Go to `User Configuration > Administrative Templates > Start Menu and Taskbar`.  
![Step 6 - Start Menu Settings](Active-Directory-Runbook-Images/image42.png)  
![Step 6 - Remove Run](Active-Directory-Runbook-Images/image43.png)

---

### Check Login History
Open Event Viewer > `Windows Logs > Security`.  
![Step 7 - Event Viewer](Active-Directory-Runbook-Images/image44.png)  
![Step 7 - Successful Login](Active-Directory-Runbook-Images/image45.png)

---

### Check Latest Installed Program
```powershell
Get-WmiObject -Class Win32_Product |
  Sort-Object InstallDate -Descending |
  Select-Object Name, Version, InstallDate -First 1
```
![Step 8 - Installed Program](Active-Directory-Runbook-Images/image46.png)

---

### List Running Services
```powershell
Get-Service |
  Where-Object {$_.Status -eq "Running"} |
  Out-File "running_services.txt"
```
![Step 9 - Running Services](Active-Directory-Runbook-Images/image47.png)

---

This concludes the full setup. The steps above ensure domain security, efficient onboarding, and proper system monitoring.
