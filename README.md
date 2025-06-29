# Active Directory Runbook

**Name of the new hire:** Toby Flenderson  
**Role at StackFull Software:** Social Media Associate  
**Department:** HR

---

This runbook documents the steps required to provision a new user in Active Directory, apply security group permissions, create network shares, enforce group policy, and validate the outcome through logs and PowerShell.

Each section is directly aligned with a screenshot from the original `.docx` document.

---

## Join the computer to the domain
1. Log in as local administrator (`administrator` / `Pa$$w0rd`)
2. Open Control Panel > System and Security > System
3. Click Change settings > Change...
4. Select domain and enter `contoso.com`
5. Enter domain credentials
6. Restart the machine

![image1](Active-Directory-Runbook-Images/image1.png)
![image2](Active-Directory-Runbook-Images/image2.png)
![image3](Active-Directory-Runbook-Images/image3.png)
![image4](Active-Directory-Runbook-Images/image4.png)
![image5](Active-Directory-Runbook-Images/image5.png)

## Create a new user
1. Open Active Directory Users and Computers (ADUC)
2. Navigate to the Users container
3. Right-click > New > User
4. Enter name: Toby Flenderson
5. Set a password (require change at next login)
6. Finish wizard

![image6](Active-Directory-Runbook-Images/image6.png)
![image7](Active-Directory-Runbook-Images/image7.png)
![image8](Active-Directory-Runbook-Images/image8.png)
![image9](Active-Directory-Runbook-Images/image9.png)
![image10](Active-Directory-Runbook-Images/image10.png)
![image11](Active-Directory-Runbook-Images/image11.png)

## Create a group named HR
1. Open Computer Management
2. Expand Local Users and Groups > Groups
3. Right-click > New Group
4. Name: HR
5. Add Toby Flenderson to the group

![image12](Active-Directory-Runbook-Images/image12.png)
![image13](Active-Directory-Runbook-Images/image13.png)
![image14](Active-Directory-Runbook-Images/image14.png)
![image15](Active-Directory-Runbook-Images/image15.png)

## Create a share for HR
1. Create a folder named `HR_Share`
2. Right-click > Properties > Sharing > Advanced Sharing
3. Enable sharing, name: `HRShare`
4. Permissions: remove Everyone, add HR group, Full Control
5. Create a test file in the folder

![image16](Active-Directory-Runbook-Images/image16.png)
![image17](Active-Directory-Runbook-Images/image17.png)
![image18](Active-Directory-Runbook-Images/image18.png)
![image19](Active-Directory-Runbook-Images/image19.png)
![image20](Active-Directory-Runbook-Images/image20.png)
![image21](Active-Directory-Runbook-Images/image21.png)

## Create an Organizational Unit
1. In ADUC, right-click domain > New > Organizational Unit
2. Name: HR
3. Move user and group into the OU

![image22](Active-Directory-Runbook-Images/image22.png)
![image23](Active-Directory-Runbook-Images/image23.png)
![image24](Active-Directory-Runbook-Images/image24.png)
![image25](Active-Directory-Runbook-Images/image25.png)

## Apply Group Policy to HR OU
**Logon Banner**
- GPMC > New GPO > Edit
- Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options
- Configure interactive logon message

![image26](Active-Directory-Runbook-Images/image26.png)
![image27](Active-Directory-Runbook-Images/image27.png)
![image28](Active-Directory-Runbook-Images/image28.png)

**Disable CMD prompt**
- User Configuration > Admin Templates > System > Prevent access to the command prompt

![image29](Active-Directory-Runbook-Images/image29.png)
![image30](Active-Directory-Runbook-Images/image30.png)

**Map network drive via script**
- User Configuration > Windows Settings > Scripts (Logon/Logoff)
- Add script:
```bat
net use H: \\servername\HR
```

![image31](Active-Directory-Runbook-Images/image31.png)
![image32](Active-Directory-Runbook-Images/image32.png)
![image33](Active-Directory-Runbook-Images/image33.png)

**Remove Run menu**
- User Configuration > Admin Templates > Start Menu and Taskbar > Remove Run menu from Start Menu

![image34](Active-Directory-Runbook-Images/image34.png)
![image35](Active-Directory-Runbook-Images/image35.png)

## Check login logs
- Open Event Viewer > Security Logs
- Filter for Event ID 4624

![image36](Active-Directory-Runbook-Images/image36.png)
![image37](Active-Directory-Runbook-Images/image37.png)

## PowerShell: Most recently installed program
```powershell
Get-WmiObject -Class Win32_Product |
Sort-Object InstallDate -Descending |
Select-Object Name, Version, InstallDate -First 1
```
![image38](Active-Directory-Runbook-Images/image38.png)

## PowerShell: Running services
```powershell
Get-Service |
Where-Object {$_.Status -eq "Running"} |
Out-File "running_services.txt"
```
![image39](Active-Directory-Runbook-Images/image39.png)

## Confirm GPO drive mapping
![image40](Active-Directory-Runbook-Images/image40.png)
![image41](Active-Directory-Runbook-Images/image41.png)
![image42](Active-Directory-Runbook-Images/image42.png)
![image43](Active-Directory-Runbook-Images/image43.png)
![image44](Active-Directory-Runbook-Images/image44.png)
![image45](Active-Directory-Runbook-Images/image45.png)
![image46](Active-Directory-Runbook-Images/image46.png)

## Confirm GPO disables Run menu
![image47](Active-Directory-Runbook-Images/image47.png)
![image48](Active-Directory-Runbook-Images/image48.png)
![image49](Active-Directory-Runbook-Images/image49.png)
![image50](Active-Directory-Runbook-Images/image50.png)

## Final OU & GPO validation
![image51](Active-Directory-Runbook-Images/image51.png)
![image52](Active-Directory-Runbook-Images/image52.png)

## Validation screenshots
![image53](Active-Directory-Runbook-Images/image53.png)
![image54](Active-Directory-Runbook-Images/image54.png)
![image55](Active-Directory-Runbook-Images/image55.png)
![image56](Active-Directory-Runbook-Images/image56.png)
![image57](Active-Directory-Runbook-Images/image57.png)
![image58](Active-Directory-Runbook-Images/image58.png)
![image59](Active-Directory-Runbook-Images/image59.png)
![image60](Active-Directory-Runbook-Images/image60.png)
![image61](Active-Directory-Runbook-Images/image61.png)
![image62](Active-Directory-Runbook-Images/image62.png)
