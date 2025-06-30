# Active Directory Runbook

**New Hire:** Toby Flenderson  
**Role:** Social Media Associate  
**Department:** HR  
**Company:** StackFull Software

The following runbook outlines a series of steps to be executed in order to perform various tasks related to user and group management, file sharing, organizational unit (OU) creation, Group Policy Object (GPO) configuration, and system monitoring. These steps are aimed at setting up and managing a domain environment, ensuring security measures are in place, and enabling efficient user management.


## Step 1: Join the computer to the domain

This step involves joining a computer to the “contoso.com” domain using the provided administrator credentials.
Log in to the computer using the username “administrator” and the password “Pa$$w0rd”.
Open the Control Panel and navigate to System and Security > System.
Click on “Change settings” next to the computer name.
In the System Properties window, click on the “Change” button.
Select the “Domain” option, enter “contoso.com” as the domain name, and click “OK”.
Provide the administrator credentials for the domain when prompted.
Restart the computer for the changes to take effect.

![Step 1](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image1.png?raw=true)
![Step 2](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image2.png?raw=true)
![Step 3](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image3.png?raw=true)
![Step 4](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image4.png?raw=true)
![Step 5](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image5.png?raw=true)
![Step 6](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image6.png?raw=true)

---

## Step 2: Create a user for the new hire

Switching to the server, a new user account is created for the new hire, and a password is set for the account.
Switch to the server machine.
Log in as an administrator with appropriate permissions.
In the search box, type “Active Directory Users and Computers” and go into the program by clicking on the name.
On the left side panel, click on “contoso.com”
Go into the “Users” folder and create User for “Toby Flenderson”
Enter the necessary details for the new hire’s user account, including username and password.
Click “Finish” to create the user account.

![Step 7](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image7.png?raw=true)
![Step 8](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image8.png?raw=true)
![Step 9](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image9.png?raw=true)
![Step 10](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image10.png?raw=true)
![Step 11](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image11.png?raw=true)
![Step 12](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image12.png?raw=true)
![Step 13](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image13.png?raw=true)
![Step 14](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image14.png?raw=true)
![Step 15](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image15.png?raw=true)

---

## Step 3: Create a group with the department name

A group is created with the name of the department, allowing for better organization and management of users.
In the “Computer Management” console, expand “Local Users and Groups” and navigate to “Groups”.
Right-click in the right-hand pane and select “New Group”.
Enter the department name as the group name and click “Create”.
Double-click the newly created group to open its properties.
Click on the “Add” button and enter the username of the new hire.
Click “OK” to add the user to the group.

![Step 16](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image16.png?raw=true)
![Step 17](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image17.png?raw=true)
![Step 18](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image18.png?raw=true)
![Step 19](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image19.png?raw=true)
![Step 20](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image20.png?raw=true)
![Step 21](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image21.png?raw=true)

---

## Step 4: Create a share on the server

A share is created on the server, named after the department, and limited to users belonging to that department. The share has read and write permissions, and a text document called “test.txt” is created within the folder.
1. Open File Explorer on the server machine.
2. Navigate to the desired location where the department share should be created.
3. Right-click on the folder and select “Properties”.
4. In the “Properties” window, go to the “Sharing” tab.
5. Click on the “Share” button and enter the department name as the share name.
6. Configure the share permissions to allow read and write access only to the group created in Step 3.
7. Click “OK” to create the share.
8. Open the newly created share and create a text document called “test.txt”

![Step 22](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image22.png?raw=true)
![Step 23](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image23.png?raw=true)
![Step 24](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image24.png?raw=true)
![Step 25](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image25.png?raw=true)
![Step 26](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image26.png?raw=true)
![Step 27](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image27.png?raw=true)
![Step 28](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image28.png?raw=true)
![Step 29](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image29.png?raw=true)
![Step 30](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image30.png?raw=true)
![Step 31](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image31.png?raw=true)
![Step 32](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image32.png?raw=true)

---

## Step 5: Create an OU with the department name

An Organizational Unit (OU) is created, named after the department, to organize further and manage the user, group, and computer objects.
1. Open the “Active Directory Users and Computers” console on the server machine.
2. Right-click on the domain name and select “New” > “Organizational Unit”.
3. Enter the department name as the OU name and click “OK”.
4. Move the user, group, and computer objects to the newly created OU
5. Create or locate a Group Policy Object (GPO) that contains the desired settings.
6. Right-click on the OU and select “Link an Existing GPO”.
7. Choose the appropriate GPO and click “OK” to link it to the OU.

![Step 33](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image33.png?raw=true)
![Step 34](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image34.png?raw=true)
![Step 35](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image35.png?raw=true)
![Step 36](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image36.png?raw=true)
![Step 37](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image37.png?raw=true)
![Step 38](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image38.png?raw=true)
![Step 39](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image39.png?raw=true)
![Step 40](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image40.png?raw=true)

---

## Step 6: Edit the GPO and apply specific rules

The Group Policy Object (GPO) attached to the created OU is edited to enforce certain rules:
Display a message during computer startup, prohibiting unauthorized program installations.
Restrict user access to the Command Prompt (CMD).
Add a login script to map the previously created share for the user.
Disable the Run command from the start menu.
Display a message during computer startup, prohibiting unauthorized program installations:
1. Open the Group Policy Management Console on your Windows Server.
2. Create a new Group Policy Object (GPO) or select an existing one.
3. Right-click on the selected GPO and choose “Edit”.
4. In the Group Policy Management Editor, navigate to "Computer Configuration" > "Policies" > "Windows 
    Settings" > "Security Settings" > "Local Policies" > "Security Options."
5. Look for the policy setting named "User Account Control: Run all administrators in Admin Approval Mode" 
    and double-click on it.
6. Set the policy to "Enabled" and click "OK."
7. Close the Group Policy Management Editor.
8. Apply the GPO to the relevant Organizational Units (OU) or Active Directory group.
Restrict user access to the Command Prompt (CMD):
1. Open the Group Policy Management Console.
2. Create a new GPO or select an existing one.
3. Right-click on the selected GPO and choose "Edit."
4. In the Group Policy Management Editor, navigate to "User Configuration" > "Policies" > "Administrative 
    Templates" > "System."
5. Find the policy setting called "Prevent access to the command prompt" and double-click on it.
6. Set the policy to "Enabled" and click "OK."
7. Close the Group Policy Management Editor.
8. Apply the GPO to the relevant OUs or Active Directory group.
Add a login script to map the previously created share for the user:
1. Open the Group Policy Management Console.
2. Create a new GPO or select an existing one.
3. Right-click on the selected GPO and choose "Edit."
4. In the Group Policy Management Editor, navigate to "User Configuration" > "Policies" > "Windows Settings" 
    > "Scripts (Logon/Logoff)."
5. Double-click on "Logon" to open the logon script configuration.
6. Click on "Show Files" to open the logon scripts folder.
7. Copy your login script (usually a .bat file) into this folder.
8. Go back to the Group Policy Management Editor, click "Add," and browse for your login script file.
9. Click "OK" to close the dialog boxes.
10. Close the Group Policy Management Editor.
11. Apply the GPO to the relevant OUs or Active Directory group.

Disable the Run command from the Start menu:
Open the Group Policy Management Console.
Create a new GPO or select an existing one.
Right-click on the selected GPO and choose "Edit."
In the Group Policy Management Editor, navigate to "User Configuration" > "Policies" > "Administrative Templates" > "Start Menu and Taskbar."
Locate the policy setting called "Remove Run menu from Start Menu" and double-click on it.
Set the policy to "Enabled" and click "OK."
Close the Group Policy Management Editor.
Apply the GPO to the relevant OUs or Active Directory group.

![Step 41](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image41.png?raw=true)
![Step 42](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image42.png?raw=true)
![Step 43](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image43.png?raw=true)
![Step 44](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image44.png?raw=true)
![Step 45](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image45.png?raw=true)
![Step 46](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image46.png?raw=true)
![Step 47](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image47.png?raw=true)
![Step 48](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image48.png?raw=true)
![Step 49](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image49.png?raw=true)
![Step 50](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image50.png?raw=true)
![Step 51](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image51.png?raw=true)
![Step 52](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image52.png?raw=true)
![Step 53](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image53.png?raw=true)
![Step 54](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image54.png?raw=true)
![Step 55](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image55.png?raw=true)
![Step 56](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image56.png?raw=true)

---

## Step 7: Check the Event Viewer for the last successful login

Using the domain administrator account, the Event Viewer on the server machine is checked to determine the timestamp of the last successful login by the specified user.


![Step 57](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image57.png?raw=true)
![Step 58](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image58.png?raw=true)
![Step 59](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image59.png?raw=true)

---

## Step 8: Use PowerShell to check the latest installed program

A PowerShell command is executed to retrieve information about the most recent program installation on the computer.
![Step 60](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image60.png?raw=true)
![Step 61](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image61.png?raw=true)

---

## Step 9: Write a PowerShell script to list running services

A PowerShell script is created to gather a list of all running services on the computer, and the output is saved to a file named “running_services.txt”.
By following these steps, the runbook aims to facilitate the setup and management of a domain environment, enforce security measures, monitor system activity, and streamline user and group management within the specified department.

![Step 61](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image61.png?raw=true)
![Step 62](https://github.com/eldoktor1/Active-Directory-Runbook/blob/main/Active-Directory-Runbook-Images/image62.png?raw=true)
---

## Summary

By following these steps, the runbook aims to facilitate the setup and management of a domain environment, enforce security measures, monitor system activity, and streamline user and group management within the specified department.

---
