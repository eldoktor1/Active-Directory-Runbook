# Active Directory Runbook

**New Hire:** Toby Flenderson  
**Role:** Social Media Associate  
**Department:** HR  
**Company:** StackFull Software

---

## Step 1: Join the Computer to the Domain

Join the computer to the `contoso.com` domain using administrator credentials.

Log in using `administrator / Pa$$w0rd`, go to **Control Panel > System > Change settings**, and add the computer to the domain.

![Step 1](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image1.png?raw=true)
![Step 2](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image2.png?raw=true)
![Step 3](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image3.png?raw=true)
![Step 4](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image4.png?raw=true)
![Step 5](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image5.png?raw=true)
![Step 6](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image6.png?raw=true)

---

## Step 2: Create a User for the New Hire

Create a new user account for Toby Flenderson in **Active Directory Users and Computers** under the `Users` folder.

![Step 7](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image7.png?raw=true)
![Step 8](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image8.png?raw=true)
![Step 9](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image9.png?raw=true)

---

## Step 3: Create a Group with the Department Name

Open **Computer Management**, create a new group named `HR`, and add Toby to this group.

![Step 10](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image10.png?raw=true)
![Step 11](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image11.png?raw=true)
![Step 12](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image12.png?raw=true)

---

## Step 4: Create a Department Share

Create a folder on the server, share it as `HR`, grant access to the group, and create a `test.txt` file inside.

![Step 13](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image13.png?raw=true)
![Step 14](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image14.png?raw=true)
![Step 15](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image15.png?raw=true)
![Step 16](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image16.png?raw=true)
![Step 17](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image17.png?raw=true)

---

## Step 5: Create an Organizational Unit (OU)

In **Active Directory**, create a new Organizational Unit named `HR` and move the user, group, and computer into it.

![Step 18](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image18.png?raw=true)
![Step 19](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image19.png?raw=true)
![Step 20](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image20.png?raw=true)
![Step 21](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image21.png?raw=true)

---

## Step 6: Link and Edit Group Policy Object (GPO)

This step involves editing Group Policy settings applied to the new OU.


---

### a. Link an Existing GPO

Link an existing GPO to the `HR` OU.

![Step 22](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image22.png?raw=true)
![Step 23](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image23.png?raw=true)

---

### b. Display a Startup Message

Edit the GPO to show a startup message by enabling **Admin Approval Mode**.

![Step 24](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image24.png?raw=true)
![Step 25](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image25.png?raw=true)
![Step 26](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image26.png?raw=true)

---

### c. Disable Command Prompt Access

Restrict access to the Command Prompt by enabling the **Prevent access to the command prompt** policy.

![Step 27](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image27.png?raw=true)
![Step 28](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image28.png?raw=true)
![Step 29](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image29.png?raw=true)

---

### d. Add a Login Script to Map the Share

Add a logon script to map the department share using Group Policy.

![Step 30](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image30.png?raw=true)
![Step 31](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image31.png?raw=true)
![Step 32](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image32.png?raw=true)
![Step 33](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image33.png?raw=true)

---

### e. Disable 'Run' from Start Menu

Disable the **Run** option from the Start menu through Group Policy.

![Step 34](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image34.png?raw=true)
![Step 35](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image35.png?raw=true)

---

## Step 7: Check Event Viewer for Last Login

Use **Event Viewer** to find the last login of the new hire.

![Step 36](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image36.png?raw=true)

---

## Step 8: Use PowerShell to View the Latest Installed Program

Run the following PowerShell command:
```powershell
Get-WmiObject -Class Win32_Product | Sort-Object InstallDate -Descending | Select-Object Name, InstallDate -First 1
```

![Step 37](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image37.png?raw=true)

---

## Step 9: Write a PowerShell Script to List Running Services

Use this PowerShell command:
```powershell
Get-Service | Where-Object {$_.Status -eq 'Running'} | Out-File "C:\\running_services.txt"
```

![Step 38](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image38.png?raw=true)

---

## Summary

This runbook helps standardize new user onboarding and Active Directory setup across departments.


---
