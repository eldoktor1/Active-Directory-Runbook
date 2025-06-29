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

Once successfully joined, you will be prompted to restart the system to apply changes. Restart the computer to complete the process.

---

### Step 2: Create a New User in Active Directory
Log in to the domain controller or a computer with administrative tools.

Open the **Active Directory Users and Computers** console.  
![Search and Launch ADUC](Active-Directory-Runbook-Images/image6.png)

Expand your domain (e.g., `contoso.com`) and navigate to the **Users** container.  
![Select Domain in ADUC](Active-Directory-Runbook-Images/image7.png)

Right-click the **Users** container and choose **New > User**.  
![New User Wizard Start](Active-Directory-Runbook-Images/image8.png)

Enter the user's first name, last name, and user logon name (e.g., tflenderson).  
![Fill in User Info](Active-Directory-Runbook-Images/image9.png)

Set an initial password and configure appropriate password options.  
![Set Password and Policies](Active-Directory-Runbook-Images/image10.png)

Click **Finish** to complete user creation.  
![Finish User Wizard](Active-Directory-Runbook-Images/image11.png)

You should now see the newly created user listed in the **Users** container.

---

### Step 3: Create a Security Group
To manage permissions using security groups, create a new group in Active Directory.

Open the **Active Directory Users and Computers** console.  
![Open ADUC](Active-Directory-Runbook-Images/image12.png)

Navigate to the **Users** container under your domain.  
![Navigate to Users Container](Active-Directory-Runbook-Images/image13.png)

Right-click **Users**, choose **New > Group**.  
![Create New Group Dialog](Active-Directory-Runbook-Images/image14.png)

Enter the group name (e.g., `HR`) and ensure the group scope is set to **Global**, and type is **Security**.  
![Group Settings and Confirmation](Active-Directory-Runbook-Images/image15.png)

Once created, double-click the new group, go to the **Members** tab, and click **Add** to include the user you created in Step 2.

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
![Open GPMC Editor](Active-Directory-Runbook-Images/image40.png)

2. Navigate to **User Configuration > Windows Settings > Scripts (Logon/Logoff)**.  
![Navigate to Logon Scripts](Active-Directory-Runbook-Images/image41.png)

3. Double-click **Logon**, then click **Add**.  
![Click Add Logon Script](Active-Directory-Runbook-Images/image42.png)

4. Click **Browse...**, copy your `.bat` file to the window, and select it. The script should include something like:  
```bat
net use H: \servername\HR
```
![Browse to Script File](Active-Directory-Runbook-Images/image43.png)

5. Confirm that the script is listed and click **OK**.  
![Script Added Confirmation](Active-Directory-Runbook-Images/image44.png)

6. Click **Apply**, then close the dialog.  
![Apply Script Settings](Active-Directory-Runbook-Images/image45.png)

7. At next login, the HR share will be mapped automatically for users.  
![Login Mapping Result](Active-Directory-Runbook-Images/image46.png)

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
These screenshots validate earlier configuration steps:

**GPO link confirmation (Step 6):**  
![GPO Link Confirmed](Active-Directory-Runbook-Images/image53.png)

**Logon script trigger at login (Step 10):**  
![Logon Script Triggered](Active-Directory-Runbook-Images/image54.png)

**Policy result for user (Step 6):**  
![GPResult for User](Active-Directory-Runbook-Images/image55.png)

**HR share mapped on login (Step 10):**  
![Mapped Drive Visible](Active-Directory-Runbook-Images/image56.png)

**OU and group structure validation (Step 5):**  
![OU Structure Verified](Active-Directory-Runbook-Images/image57.png)

**Successful login event (Step 7):**  
![Login Log in Event Viewer](Active-Directory-Runbook-Images/image58.png)

**Running services check - part 1 (Step 9):**  
![Running Services Page 1](Active-Directory-Runbook-Images/image59.png)

**Running services check - part 2 (Step 9):**  
![Running Services Page 2](Active-Directory-Runbook-Images/image60.png)

**Manual logon script verification (Step 10):**  
![Manual Logon Script Execution](Active-Directory-Runbook-Images/image61.png)

**Final configuration summary (Step 12):**  
![Final System Check](Active-Directory-Runbook-Images/image62.png)
