# Active Directory Runbook

**Name of the new hire:** Toby Flenderson  
**Role at StackFull Software:** Social Media Associate  
**Department:** HR

---

The following runbook outlines a series of steps to be executed in order to perform various tasks related to user and group management, file sharing, organizational unit (OU) creation, Group Policy Object (GPO) configuration, and system monitoring. These steps are aimed at setting up and managing a domain environment, ensuring security measures are in place, and enabling efficient user management.

---

## 🖥️ Step 1: Join the Computer to the Domain
1. Log in as `administrator` and navigate to `System > About > Rename this PC (advanced)`.
2. Click "Change" to update the domain membership.
3. Enter `contoso.com` and provide credentials.
4. Restart the system.

![Step 1a](Active-Directory-Runbook-Images/image3.png)  
![Step 1b](Active-Directory-Runbook-Images/image4.png)  
![Step 1c](Active-Directory-Runbook-Images/image5.png)  
![Step 1d](Active-Directory-Runbook-Images/image6.png)

---

## 👤 Step 2: Create a User for the New Hire
1. Open **Active Directory Users and Computers**.
2. Go to `contoso.com > Users`, right-click > `New > User`.
3. Fill out the new user form.
4. Set password options and click `Finish`.

![Step 2a](Active-Directory-Runbook-Images/image7.png)  
![Step 2b](Active-Directory-Runbook-Images/image8.png)  
![Step 2c](Active-Directory-Runbook-Images/image9.png)  
![Step 2d](Active-Directory-Runbook-Images/image10.png)

---

## 👥 Step 3: Create a Group with the Department Name
1. In ADUC, right-click `Users` > `New > Group`.
2. Name the group `HR`.
3. Open the group, click `Members > Add`, and select the new user.

![Step 3a](Active-Directory-Runbook-Images/image11.png)  
![Step 3b](Active-Directory-Runbook-Images/image12.png)

---

## 📁 Step 4: Create a Share on the Server
1. On the server, create a folder.
2. Right-click > `Properties > Sharing > Advanced Sharing`.
3. Set permissions for the `HR` group.
4. Create a test file in the share.

![Step 4a](Active-Directory-Runbook-Images/image13.png)  
![Step 4b](Active-Directory-Runbook-Images/image14.png)  
![Step 4c](Active-Directory-Runbook-Images/image15.png)

---

## 🗂️ Step 5: Create an Organizational Unit (OU)
1. In ADUC, right-click domain > `New > Organizational Unit`.
2. Name the OU `HR`, click OK.
3. Move user and group into the OU.

![Step 5a](Active-Directory-Runbook-Images/image16.png)  
![Step 5b](Active-Directory-Runbook-Images/image17.png)

---

## 🛡️ Step 6: Configure Group Policy
### A. Display a Startup Message
1. Open GPMC.
2. Create/Edit GPO linked to `HR` OU.
3. Navigate to `Computer Configuration > Policies > Windows Settings > Security Options`.
4. Enable UAC policy.

![Step 6a](Active-Directory-Runbook-Images/image18.png)  
![Step 6b](Active-Directory-Runbook-Images/image19.png)

### B. Restrict Command Prompt
Navigate to:  
`User Configuration > Policies > Administrative Templates > System > Prevent access to command prompt`

![Step 6c](Active-Directory-Runbook-Images/image20.png)

### C. Add a Logon Script
1. Go to `User Configuration > Windows Settings > Scripts (Logon/Logoff)`.
2. Add a `.bat` file to map the shared drive.

![Step 6d](Active-Directory-Runbook-Images/image21.png)  
![Step 6e](Active-Directory-Runbook-Images/image22.png)

### D. Disable Run Menu
`User Configuration > Administrative Templates > Start Menu and Taskbar > Remove Run menu`

![Step 6f](Active-Directory-Runbook-Images/image23.png)

---

## 📊 Step 7: Check Last Login via Event Viewer
1. Open Event Viewer.
2. Navigate to `Windows Logs > Security`.
3. Filter for successful logons for the new user.

![Step 7](Active-Directory-Runbook-Images/image24.png)

---

## 💻 Step 8: Use PowerShell to Check Latest Installed Program
```powershell
Get-WmiObject -Class Win32_Product |
  Sort-Object InstallDate -Descending |
  Select-Object Name, Version, InstallDate -First 1
```

![Step 8](Active-Directory-Runbook-Images/image25.png)

---

## ⚙️ Step 9: List Running Services with PowerShell
```powershell
Get-Service |
  Where-Object {$_.Status -eq "Running"} |
  Out-File "running_services.txt"
```

![Step 9](Active-Directory-Runbook-Images/image26.png)

---

By following these steps, the runbook ensures secure onboarding, proper group and file access, centralized configuration management, and ongoing monitoring of a Windows domain environment.
