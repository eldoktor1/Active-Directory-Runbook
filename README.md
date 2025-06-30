
# Active Directory Runbook

**New Hire:** Toby Flenderson  
**Role:** Social Media Associate  
**Department:** HR  
**Company:** StackFull Software

This runbook outlines the process of onboarding a new employee by configuring Active Directory (AD) settings, creating user and group objects, managing file shares, applying Group Policy Objects (GPOs), and auditing system activities. It is designed for IT admins managing a domain environment.

---

## Step 1: Join the Computer to the Domain

Join the computer to the `contoso.com` domain using administrator credentials.

1. Log in using `administrator / Pa$$w0rd`.
2. Open **Control Panel > System and Security > System**.
3. Click on **Change settings** next to the computer name.
4. In **System Properties**, click **Change**.
5. Select **Domain**, enter `contoso.com`, and click **OK**.
6. Enter domain admin credentials when prompted.
7. Restart the computer.

![Step 1](Active-Directory-Runbook-Images/image1.png)
![Step 2](Active-Directory-Runbook-Images/image2.png)
![Step 3](Active-Directory-Runbook-Images/image3.png)
![Step 4](Active-Directory-Runbook-Images/image4.png)
![Step 5](Active-Directory-Runbook-Images/image5.png)
![Step 6](Active-Directory-Runbook-Images/image6.png)

---

## Step 2: Create a User for the New Hire

Switch to the server and create a user account for Toby Flenderson.

1. Log in as domain admin.
2. Open **Active Directory Users and Computers**.
3. Navigate to `contoso.com > Users`.
4. Right-click > **New > User** and input user details.
5. Set a secure password and click **Finish**.

![Step 7](Active-Directory-Runbook-Images/image7.png)
![Step 8](Active-Directory-Runbook-Images/image8.png)
![Step 9](Active-Directory-Runbook-Images/image9.png)

---

## Step 3: Create a Group with the Department Name

1. Open **Computer Management** > **Local Users and Groups > Groups**.
2. Right-click and choose **New Group**.
3. Name the group (e.g., `HR`) and create it.
4. Double-click the group and add Toby as a member.

![Step 10](Active-Directory-Runbook-Images/image10.png)
![Step 11](Active-Directory-Runbook-Images/image11.png)
![Step 12](Active-Directory-Runbook-Images/image12.png)

---

## Step 4: Create a Department Share

1. On the server, open **File Explorer** and create a folder (e.g., `\Server\HR`).
2. Right-click > **Properties > Sharing** tab > **Share**.
3. Set share name and configure **permissions** for the HR group.
4. Allow read/write access.
5. Inside the share, create a text file called `test.txt`.

![Step 13](Active-Directory-Runbook-Images/image13.png)
![Step 14](Active-Directory-Runbook-Images/image14.png)
![Step 15](Active-Directory-Runbook-Images/image15.png)
![Step 16](Active-Directory-Runbook-Images/image16.png)
![Step 17](Active-Directory-Runbook-Images/image17.png)

---

## Step 5: Create an Organizational Unit (OU)

1. In **Active Directory Users and Computers**, right-click the domain > **New > Organizational Unit**.
2. Name it `HR`.
3. Move the relevant user, group, and computer objects into this OU.

![Step 18](Active-Directory-Runbook-Images/image18.png)
![Step 19](Active-Directory-Runbook-Images/image19.png)
![Step 20](Active-Directory-Runbook-Images/image20.png)
![Step 21](Active-Directory-Runbook-Images/image21.png)

---

## Step 6: Link and Edit Group Policy Object (GPO)

### a. Link an Existing GPO

1. Right-click the `HR` OU > **Link an Existing GPO**.
2. Select the appropriate policy and click **OK**.

![Step 22](Active-Directory-Runbook-Images/image22.png)
![Step 23](Active-Directory-Runbook-Images/image23.png)

---

### b. Display a Startup Message

1. Open **Group Policy Management Editor**.
2. Go to: `Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options`.
3. Enable **"User Account Control: Run all administrators in Admin Approval Mode"**.

![Step 24](Active-Directory-Runbook-Images/image24.png)
![Step 25](Active-Directory-Runbook-Images/image25.png)
![Step 26](Active-Directory-Runbook-Images/image26.png)

---

### c. Disable Command Prompt Access

1. Navigate to `User Configuration > Policies > Administrative Templates > System`.
2. Enable **"Prevent access to the command prompt"**.

![Step 27](Active-Directory-Runbook-Images/image27.png)
![Step 28](Active-Directory-Runbook-Images/image28.png)
![Step 29](Active-Directory-Runbook-Images/image29.png)

---

### d. Add a Login Script to Map the Share

1. Go to: `User Configuration > Policies > Windows Settings > Scripts (Logon/Logoff)`.
2. Open **Logon**, click **Show Files**, and place your `.bat` script.
3. Click **Add** and select the login script.

![Step 30](Active-Directory-Runbook-Images/image30.png)
![Step 31](Active-Directory-Runbook-Images/image31.png)
![Step 32](Active-Directory-Runbook-Images/image32.png)
![Step 33](Active-Directory-Runbook-Images/image33.png)

---

### e. Disable "Run" from Start Menu

1. Navigate to: `User Configuration > Policies > Administrative Templates > Start Menu and Taskbar`.
2. Enable **"Remove Run menu from Start Menu"**.

![Step 34](Active-Directory-Runbook-Images/image34.png)
![Step 35](Active-Directory-Runbook-Images/image35.png)

---

## Step 7: Check Event Viewer for Last Login

Use Event Viewer on the domain server to check the last successful login for the new hire.

![Step 36](Active-Directory-Runbook-Images/image36.png)

---

## Step 8: Use PowerShell to View the Latest Installed Program

Use PowerShell to list the most recently installed software:

```powershell
Get-WmiObject -Class Win32_Product | Sort-Object InstallDate -Descending | Select-Object Name, InstallDate -First 1
```

![Step 37](Active-Directory-Runbook-Images/image37.png)

---

## Step 9: Write a PowerShell Script to List Running Services

Save the following PowerShell script as `running_services.ps1`:

```powershell
Get-Service | Where-Object {$_.Status -eq 'Running'} | Out-File "C:\running_services.txt"
```

![Step 38](Active-Directory-Runbook-Images/image38.png)

---

## Summary

This runbook streamlines Active Directory onboarding and management tasks. By automating user/group provisioning, enforcing policies via GPOs, and auditing system activity with PowerShell, this workflow ensures a secure, organized, and scalable domain environment.
