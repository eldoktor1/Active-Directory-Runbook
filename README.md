**Name of new hire:** Toby Flenderson  
**Role at StackFull Software:** Social Media Associate  
**Department:** HR

---

1. Log in using the local administrator account (username: administrator, password: Pa$$w0rd).

![image1](Active-Directory-Runbook-Images/image1.png)

2. Go to Control Panel > System and Security > System.

![image2](Active-Directory-Runbook-Images/image2.png)

3. Click Change settings.

![image3](Active-Directory-Runbook-Images/image3.png)

4. Click Change.

![image4](Active-Directory-Runbook-Images/image4.png)

5. Join the domain "contoso.com" and provide domain credentials.

![image5](Active-Directory-Runbook-Images/image5.png)

6. Open Active Directory Users and Computers.

![image6](Active-Directory-Runbook-Images/image6.png)

7. Go to Users > right-click > New > User.

![image7](Active-Directory-Runbook-Images/image7.png)

8. Create a user with the following name: Toby Flenderson.

![image8](Active-Directory-Runbook-Images/image8.png)

9. Username: tflenderson.

![image9](Active-Directory-Runbook-Images/image9.png)

10. Set password: Pa$$w0rd. Uncheck "User must change password at next logon."

![image10](Active-Directory-Runbook-Images/image10.png)

11. Click Finish.

![image11](Active-Directory-Runbook-Images/image11.png)

12. On the local machine, open Computer Management.

![image12](Active-Directory-Runbook-Images/image12.png)

13. Expand Local Users and Groups > Groups.

![image13](Active-Directory-Runbook-Images/image13.png)

14. Create a new group named HR.

![image14](Active-Directory-Runbook-Images/image14.png)

15. Add the newly created user to the HR group.

![image15](Active-Directory-Runbook-Images/image15.png)

16. On the file server, create a new folder named HR_Share.

![image16](Active-Directory-Runbook-Images/image16.png)

17. Right-click folder > Properties.

![image17](Active-Directory-Runbook-Images/image17.png)

18. Go to the Sharing tab > Advanced Sharing.

![image18](Active-Directory-Runbook-Images/image18.png)

19. Check "Share this folder" and name it "HRShare."

![image19](Active-Directory-Runbook-Images/image19.png)

20. Click Permissions.

![image20](Active-Directory-Runbook-Images/image20.png)

21. Remove Everyone. Add HR. Grant Full Control.

![image21](Active-Directory-Runbook-Images/image21.png)

22. In ADUC, right-click domain > New > Organizational Unit.

![image22](Active-Directory-Runbook-Images/image22.png)

23. Name the OU "HR."

![image23](Active-Directory-Runbook-Images/image23.png)

24. Move the user and group into the HR OU.

![image24](Active-Directory-Runbook-Images/image24.png)

![image25](Active-Directory-Runbook-Images/image25.png)

25. In Group Policy Management, right-click the OU > Create a GPO named "HR_GPO."

![image26](Active-Directory-Runbook-Images/image26.png)

26. Edit the GPO.

![image27](Active-Directory-Runbook-Images/image27.png)

27. Go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options.

28. Enable interactive logon message.

![image28](Active-Directory-Runbook-Images/image28.png)

29. Navigate to User Configuration > Administrative Templates > System.

![image29](Active-Directory-Runbook-Images/image29.png)

30. Enable "Prevent access to command prompt."

![image30](Active-Directory-Runbook-Images/image30.png)

31. Go to User Configuration > Windows Settings > Scripts > Logon.

![image31](Active-Directory-Runbook-Images/image31.png)

32. Add the following batch file:
```bat
net use H: \\servername\HR
```

![image32](Active-Directory-Runbook-Images/image32.png)

![image33](Active-Directory-Runbook-Images/image33.png)

33. Navigate to User Configuration > Administrative Templates > Start Menu and Taskbar.

![image34](Active-Directory-Runbook-Images/image34.png)

34. Enable "Remove Run menu from Start Menu."

![image35](Active-Directory-Runbook-Images/image35.png)

35. Open Event Viewer > Windows Logs > Security.

![image36](Active-Directory-Runbook-Images/image36.png)

36. Filter for Event ID 4624 (successful logon).

![image37](Active-Directory-Runbook-Images/image37.png)

37. Open PowerShell and run:
```powershell
Get-WmiObject -Class Win32_Product |
Sort-Object InstallDate -Descending |
Select-Object Name, Version, InstallDate -First 1
```

![image38](Active-Directory-Runbook-Images/image38.png)

38. To check running services, run:
```powershell
Get-Service |
Where-Object {$_.Status -eq "Running"} |
Out-File "running_services.txt"
```

![image39](Active-Directory-Runbook-Images/image39.png)

39. Additional screenshots confirming correct configuration and logon behavior:

![image40](Active-Directory-Runbook-Images/image40.png)
![image41](Active-Directory-Runbook-Images/image41.png)
![image42](Active-Directory-Runbook-Images/image42.png)
![image43](Active-Directory-Runbook-Images/image43.png)
![image44](Active-Directory-Runbook-Images/image44.png)
![image45](Active-Directory-Runbook-Images/image45.png)
![image46](Active-Directory-Runbook-Images/image46.png)
![image47](Active-Directory-Runbook-Images/image47.png)
![image48](Active-Directory-Runbook-Images/image48.png)
![image49](Active-Directory-Runbook-Images/image49.png)
![image50](Active-Directory-Runbook-Images/image50.png)
![image51](Active-Directory-Runbook-Images/image51.png)
![image52](Active-Directory-Runbook-Images/image52.png)
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
