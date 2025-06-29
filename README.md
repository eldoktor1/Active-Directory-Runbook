**Name of new hire:** Toby Flenderson  
**Role at StackFull Software:** Social Media Associate  
**Department:** HR

---

1. Log in to the computer using the username “administrator” and the password “Pa$$w0rd”.

![image1](Active-Directory-Runbook-Images/image1.png)

2. Open the Control Panel and navigate to System and Security > System.

![image2](Active-Directory-Runbook-Images/image2.png)

3. Click on “Change settings” next to the computer name.

![image3](Active-Directory-Runbook-Images/image3.png)

4. In the System Properties window, click on the “Change” button.

![image4](Active-Directory-Runbook-Images/image4.png)

5. Select the “Domain” option, enter “contoso.com” as the domain name, and click “OK”.

![image5](Active-Directory-Runbook-Images/image5.png)

6. Restart the computer for the changes to take effect.

7. On the server, log in with an account that has administrative privileges.

8. Open Active Directory Users and Computers.

![image6](Active-Directory-Runbook-Images/image6.png)

9. In the left pane, click on the “Users” container.

![image7](Active-Directory-Runbook-Images/image7.png)

10. Right-click on the Users container and select “New” > “User”.

![image8](Active-Directory-Runbook-Images/image8.png)

11. Enter the first name, last name, and full name of the new hire (Toby Flenderson). Enter the user logon name “tflenderson”.

![image9](Active-Directory-Runbook-Images/image9.png)

12. Set the password to “Pa$$w0rd”. Uncheck “User must change password at next logon”. Click Next and then Finish.

![image10](Active-Directory-Runbook-Images/image10.png)

13. Confirm that the user has been created.

![image11](Active-Directory-Runbook-Images/image11.png)

14. Open the Computer Management console on the file server.

![image12](Active-Directory-Runbook-Images/image12.png)

15. In the left pane, expand “System Tools” > “Local Users and Groups” > “Groups”.

![image13](Active-Directory-Runbook-Images/image13.png)

16. Right-click on “Groups” and select “New Group”.

![image14](Active-Directory-Runbook-Images/image14.png)

17. In the New Group dialog box, enter the group name “HR”. Click “Add…” and add “tflenderson” to the group. Click “Create” and then “Close”.

![image15](Active-Directory-Runbook-Images/image15.png)

18. Create a new folder on the file server and name it “HR_Share”.

![image16](Active-Directory-Runbook-Images/image16.png)

19. Right-click on the folder and select “Properties”.

![image17](Active-Directory-Runbook-Images/image17.png)

20. Navigate to the “Sharing” tab and click on “Share”.

![image18](Active-Directory-Runbook-Images/image18.png)

21. In the “Network access” dialog, select “HR” from the drop-down list and click “Add”.

![image19](Active-Directory-Runbook-Images/image19.png)

22. Set the Permission Level for “HR” to “Read/Write” and click “Share”.

![image20](Active-Directory-Runbook-Images/image20.png)

23. Go to the “Security” tab, click “Edit”, remove “Everyone”, and add “HR” with Full Control.

![image21](Active-Directory-Runbook-Images/image21.png)

24. In Active Directory Users and Computers, right-click on the domain and choose “New” > “Organizational Unit”.

![image22](Active-Directory-Runbook-Images/image22.png)

25. Name the OU “HR”.

![image23](Active-Directory-Runbook-Images/image23.png)

26. Move the “tflenderson” user and “HR” group into the “HR” OU.

![image24](Active-Directory-Runbook-Images/image24.png)

![image25](Active-Directory-Runbook-Images/image25.png)

27. Open Group Policy Management. Right-click the “HR” OU and choose “Create a GPO in this domain, and Link it here…”. Name it “HR_GPO”.

![image26](Active-Directory-Runbook-Images/image26.png)

28. Right-click on the newly created GPO and select “Edit”.

![image27](Active-Directory-Runbook-Images/image27.png)

29. In the Group Policy Management Editor, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options. Enable the following policies:
- “Interactive logon: Message title for users attempting to log on”
- “Interactive logon: Message text for users attempting to log on”

![image28](Active-Directory-Runbook-Images/image28.png)

30. Navigate to User Configuration > Administrative Templates > System. Enable “Prevent access to the command prompt” and select “Yes” to disable script processing.

![image29](Active-Directory-Runbook-Images/image29.png)

![image30](Active-Directory-Runbook-Images/image30.png)

31. Navigate to User Configuration > Windows Settings > Scripts (Logon/Logoff). Double-click “Logon”.

![image31](Active-Directory-Runbook-Images/image31.png)

32. Click “Add” and browse to the script location. The script should contain:
```bat
net use H: \\servername\HR
```

![image32](Active-Directory-Runbook-Images/image32.png)

![image33](Active-Directory-Runbook-Images/image33.png)

33. Navigate to User Configuration > Administrative Templates > Start Menu and Taskbar. Enable “Remove Run menu from Start Menu”.

![image34](Active-Directory-Runbook-Images/image34.png)

![image35](Active-Directory-Runbook-Images/image35.png)

34. Open Event Viewer. Go to Windows Logs > Security. Filter the log by Event ID 4624 to confirm successful login.

![image36](Active-Directory-Runbook-Images/image36.png)

![image37](Active-Directory-Runbook-Images/image37.png)

35. Open PowerShell and run the following to find the most recently installed program:
```powershell
Get-WmiObject -Class Win32_Product |
Sort-Object InstallDate -Descending |
Select-Object Name, Version, InstallDate -First 1
```

![image38](Active-Directory-Runbook-Images/image38.png)

36. Run the following command to save a list of running services:
```powershell
Get-Service |
Where-Object {$_.Status -eq "Running"} |
Out-File "running_services.txt"
```

![image39](Active-Directory-Runbook-Images/image39.png)

37. Additional screenshots validating correct policy application and user access:

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
