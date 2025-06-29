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
Log in to the domain controller or management workstation.

Open the **Active Directory Users and Computers** console.  
![Step](Active-Directory-Runbook-Images/image6.png)

In the left pane, expand your domain (e.g., `contoso.com`) and click on the **Users** folder.  
![Step](Active-Directory-Runbook-Images/image7.png)

Right-click the **Users** folder and choose **New > User**.  
![Step](Active-Directory-Runbook-Images/image8.png)

Enter the user’s first name, last name, and a unique username (e.g., tflenderson).  
![Step](Active-Directory-Runbook-Images/image9.png)

Set an initial password and configure password policies such as requiring change on next login.  
![Step](Active-Directory-Runbook-Images/image10.png)

Click **Finish** to create the account.  
![Step](Active-Directory-Runbook-Images/image11.png)

---

### Step 3: Create a Security Group
Open the **Computer Management** console.  
![Step](Active-Directory-Runbook-Images/image12.png)

Expand **System Tools > Local Users and Groups > Groups**.  
![Step](Active-Directory-Runbook-Images/image13.png)

Right-click **Groups** and choose **New Group**.  
![Step](Active-Directory-Runbook-Images/image14.png)

Enter a group name (e.g., `HR`), and add the new user created in Step 2 by clicking **Add...**  
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
To automatically map the HR share for users when they log in, configure a logon script through Group Policy.

1. Open Group Policy Management Editor.
2. Navigate to: **User Configuration > Windows Settings > Scripts (Logon/Logoff)**.  
![Step](Active-Directory-Runbook-Images/image40.png)

3. Double-click **Logon**, then click **Add**.  
![Step](Active-Directory-Runbook-Images/image41.png)

4. Click **Browse...** and copy your `.bat` script that maps the share (e.g., `net use H: \servername\HR`).  
![Step](Active-Directory-Runbook-Images/image42.png)

5. Select the script and click **OK**.  
![Step](Active-Directory-Runbook-Images/image43.png)

6. Confirm the script is listed and click **Apply** to save.  
![Step](Active-Directory-Runbook-Images/image44.png)

7. Close the dialog and return to Group Policy Management.  
![Step](Active-Directory-Runbook-Images/image45.png)

8. The mapped drive will be created for the user at next login.  
![Step](Active-Directory-Runbook-Images/image46.png))

---

### Step 11: Disable Run Menu via Policy
To restrict access to the Run command for users, configure the appropriate policy setting in Group Policy.

1. In Group Policy Management Editor, navigate to:
   **User Configuration > Administrative Templates > Start Menu and Taskbar**  
![Step](Active-Directory-Runbook-Images/image47.png)

2. Locate and double-click **Remove Run menu from Start Menu**.  
![Step](Active-Directory-Runbook-Images/image48.png)

3. In the policy settings window, set the option to **Enabled**.  
![Step](Active-Directory-Runbook-Images/image49.png)

4. Click **OK** to apply the setting and close the dialog.  
![Step](Active-Directory-Runbook-Images/image50.png)

---

### Step 12: Final GPO and OU Verification
Review the overall GPO configuration and ensure policies are linked to the correct OU.

1. Open Group Policy Management and verify GPO linkage under the OU.  
![Step](Active-Directory-Runbook-Images/image51.png)

2. Ensure that the correct users, computers, and groups reside in the OU and inherit the intended settings.  
![Step](Active-Directory-Runbook-Images/image52.png)

---

### Step 13: Additional Screens and Validation Logs
These screenshots provide final confirmation of task execution and expected outcomes.

GPO link confirmation:  
![Step](Active-Directory-Runbook-Images/image53.png)

Logon script execution success:  
![Step](Active-Directory-Runbook-Images/image54.png)

Policy application results:  
![Step](Active-Directory-Runbook-Images/image55.png)

Folder mapping on login:  
![Step](Active-Directory-Runbook-Images/image56.png)

OU structure accuracy:  
![Step](Active-Directory-Runbook-Images/image57.png)

Successful login timestamps:  
![Step](Active-Directory-Runbook-Images/image58.png)

Service monitoring output - part 1:  
![Step](Active-Directory-Runbook-Images/image59.png)

Service monitoring output - part 2:  
![Step](Active-Directory-Runbook-Images/image60.png)

Final script execution:  
![Step](Active-Directory-Runbook-Images/image61.png)

Overall configuration summary:  
![Step](Active-Directory-Runbook-Images/image62.png)
