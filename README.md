# Active Directory Runbook

**Name of the new hire:** Toby Flenderson  
**Role at StackFull Software:** Social Media Associate  
**Department:** HR

---

This runbook outlines a series of tasks related to user and group management, file sharing, OU creation, GPO configuration, and system monitoring for a Windows domain environment.

---

## 🧩 Full Setup Process

### Step 1: Join the Computer to the Domain
Log in using the local administrator account (`administrator` / `Pa$$w0rd`).

Open Control Panel > System and Security > System.  
![Step](Active-Directory-Runbook-Images/image1.png)

Click "Change settings" to open System Properties.  
![Step](Active-Directory-Runbook-Images/image2.png)

In the Computer Name tab, click "Change..."  
![Step](Active-Directory-Runbook-Images/image3.png)

Select "Domain" and enter `contoso.com`.  
![Step](Active-Directory-Runbook-Images/image4.png)

Enter domain credentials when prompted.  
![Step](Active-Directory-Runbook-Images/image5.png)

---

### Step 2: Create a New User in Active Directory
On the server, open **Active Directory Users and Computers**.  
![Step](Active-Directory-Runbook-Images/image6.png)

Navigate to `contoso.com > Users`.  
![Step](Active-Directory-Runbook-Images/image7.png)

Right-click the Users folder and select `New > User`.  
![Step](Active-Directory-Runbook-Images/image8.png)

Enter the user's full name and username.  
![Step](Active-Directory-Runbook-Images/image9.png)

Set the password and configure user must change password options.  
![Step](Active-Directory-Runbook-Images/image10.png)

Click Finish to complete user creation.  
![Step](Active-Directory-Runbook-Images/image11.png)

---

### Step 3: Create a Security Group
In Computer Management, expand Local Users and Groups > Groups.  
![Step](Active-Directory-Runbook-Images/image12.png)

Right-click Groups and select New Group.  
![Step](Active-Directory-Runbook-Images/image13.png)

Name the group (e.g., HR).  
![Step](Active-Directory-Runbook-Images/image14.png)

Add the new user to the group.  
![Step](Active-Directory-Runbook-Images/image15.png)

---

### Step 4: Create a Network Share
On the file server, create a new folder.  
![Step](Active-Directory-Runbook-Images/image16.png)

Right-click the folder and go to Properties.  
![Step](Active-Directory-Runbook-Images/image17.png)

Go to the Sharing tab and click Advanced Sharing.  
![Step](Active-Directory-Runbook-Images/image18.png)

Enable sharing and set a name.  
![Step](Active-Directory-Runbook-Images/image19.png)

Click Permissions and grant access to the HR group.  
![Step](Active-Directory-Runbook-Images/image20.png)

Create a test file in the share to verify access.  
![Step](Active-Directory-Runbook-Images/image21.png)

---

### Step 5: Create an OU and Move Objects
Open Active Directory Users and Computers.  
![Step](Active-Directory-Runbook-Images/image22.png)

Right-click the domain and choose New > Organizational Unit.  
![Step](Active-Directory-Runbook-Images/image23.png)

Name the OU appropriately and click OK.  
![Step](Active-Directory-Runbook-Images/image24.png)

Move the user and group objects into the new OU.  
![Step](Active-Directory-Runbook-Images/image25.png)

---

### Step 6: Apply GPO Settings to the OU
Open Group Policy Management. Create and link a new GPO to the HR OU.

#### Set a Startup Message
Edit the GPO > Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options.  
![Step](Active-Directory-Runbook-Images/image26.png)

Double-click the setting for login messages.  
![Step](Active-Directory-Runbook-Images/image27.png)

Enter and apply the desired login message.  
![Step](Active-Directory-Runbook-Images/image28.png)

#### Disable Command Prompt
Navigate to: User Configuration > Admin Templates > System > Prevent access to command prompt.  
![Step](Active-Directory-Runbook-Images/image29.png)

Enable the policy and apply changes.  
![Step](Active-Directory-Runbook-Images/image30.png)

#### Add a Logon Script
Under User Configuration > Windows Settings > Scripts (Logon/Logoff), select Logon.  
![Step](Active-Directory-Runbook-Images/image31.png)

Click Add and then Browse.  
![Step](Active-Directory-Runbook-Images/image32.png)

Choose your `.bat` file that maps the share and apply it.  
![Step](Active-Directory-Runbook-Images/image33.png)

#### Remove the Run Menu
Under User Configuration > Admin Templates > Start Menu and Taskbar > Remove Run menu.  
![Step](Active-Directory-Runbook-Images/image34.png)

Enable the policy.  
![Step](Active-Directory-Runbook-Images/image35.png)

---

### Step 7: Review Login Events
Open Event Viewer > Windows Logs > Security.  
![Step](Active-Directory-Runbook-Images/image36.png)

Filter for Event ID 4624 (successful logon). Look for the new user’s logins.  
![Step](Active-Directory-Runbook-Images/image37.png)

---

### Step 8: Use PowerShell to Check Software Installations
Use the following PowerShell command to identify the most recently installed application:

```powershell
Get-WmiObject -Class Win32_Product |
  Sort-Object InstallDate -Descending |
  Select-Object Name, Version, InstallDate -First 1
```

![Step](Active-Directory-Runbook-Images/image38.png)

---

### Step 9: List Running Services with PowerShell
Use this PowerShell script to list all currently running services and export to a text file:

```powershell
Get-Service |
  Where-Object {$_.Status -eq "Running"} |
  Out-File "running_services.txt"
```

![Step](Active-Directory-Runbook-Images/image39.png)

---

### Step 10: Map the HR Share via GPO Script
Go to the Logon script settings in GPO:

1. Open the GPO editor and go to User Configuration > Windows Settings > Scripts (Logon/Logoff).  
![Step](Active-Directory-Runbook-Images/image40.png)

2. Double-click Logon and click Add.  
![Step](Active-Directory-Runbook-Images/image41.png)

3. Click Browse and select the `.bat` script to map the HR share.  
![Step](Active-Directory-Runbook-Images/image42.png)

4. Confirm the script is listed.  
![Step](Active-Directory-Runbook-Images/image43.png)

5. Apply the changes and exit the editor.  
![Step](Active-Directory-Runbook-Images/image44.png)

6. The script should now run when the user logs in.  
![Step](Active-Directory-Runbook-Images/image45.png)

7. Verify success in the resulting script summary.  
![Step](Active-Directory-Runbook-Images/image46.png)

---

### Step 11: Disable Run Menu via Policy
1. In GPO Editor, go to User Configuration > Administrative Templates > Start Menu and Taskbar.  
![Step](Active-Directory-Runbook-Images/image47.png)

2. Double-click “Remove Run menu from Start Menu”.  
![Step](Active-Directory-Runbook-Images/image48.png)

3. Set the policy to Enabled and click OK.  
![Step](Active-Directory-Runbook-Images/image49.png)

4. The policy should now reflect as Enabled.  
![Step](Active-Directory-Runbook-Images/image50.png)

---

### Step 12: Final GPO and OU Verification
1. Use Group Policy Management to review policy links and inheritance.  
![Step](Active-Directory-Runbook-Images/image51.png)

2. Verify the correct OU structure and policy application.  
![Step](Active-Directory-Runbook-Images/image52.png)

---

### Step 13: Additional Screens and Validation Logs
These screenshots validate various final outcomes:

- GPO link confirmation
- Logon script execution success
- Policy application results
- Folder mapping on login
- OU structure accuracy
- Successful login timestamps
- Service monitoring outputs

Each image represents the output or screen state following the actions configured earlier.

![Step](Active-Directory-Runbook-Images/image53.png)
![Step](Active-Directory-Runbook-Images/image54.png)
![Step](Active-Directory-Runbook-Images/image55.png)
![Step](Active-Directory-Runbook-Images/image56.png)
![Step](Active-Directory-Runbook-Images/image57.png)
![Step](Active-Directory-Runbook-Images/image58.png)
![Step](Active-Directory-Runbook-Images/image59.png)
![Step](Active-Directory-Runbook-Images/image60.png)
![Step](Active-Directory-Runbook-Images/image61.png)
![Step](Active-Directory-Runbook-Images/image62.png)
