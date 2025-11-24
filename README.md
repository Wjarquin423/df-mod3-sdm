# df-mod3-sdm
## Secure Data Management (SDM)
List running processes and save to a file:
ps aux > processes.txt
Purpose: This command lists all running processes on the system and redirects the output to a file named processes.txt. This is useful for monitoring system activity and identifying any suspicious processes.
List services and save to a file:
launchctl list > services.txt
Purpose: This command lists all services managed by launchctl on macOS and saves the output to a file named services.txt. It helps in understanding which services are running on the system.
Retrieve the last 50 lines of the system log:
cat /var/log/system.log | tail -n 50 > systemlog.txt
Purpose: This command retrieves the last 50 lines of the system log and saves them to a file named systemlog.txt. It is useful for reviewing recent system events and identifying potential issues.
Search for specific text in a file and save the results:
Get-Content processes.txt | Select-String "powershell" > search_results.txt
Purpose: This command searches the processes.txt file for the keyword "powershell" and saves the matching lines to a file named search_results.txt. This is helpful for filtering specific information from a larger dataset.
Export process information to a CSV file:
ps aux | Export-Csv -Path processes.csv -NoTypeInformation
Purpose: This command exports the list of running processes to a CSV file named processes.csv. The CSV format is useful for further analysis in tools like Excel or other data processing software.
## Managing Permissions
Commands and Their Purpose
Create a folder and file:
mkdir 2-Permissions
cd 2-Permissions
New-Item -Name evidence.txt -ItemType File
Purpose: Creates a folder named 2-Permissions and a file named evidence.txt for testing permissions.
Retrieve and save file permissions:
ls -l evidence.txt > evidence-acl.txt
Purpose: Lists the file permissions of evidence.txt and saves the output to a file named evidence-acl.txt. This is useful for documenting the initial permissions of the file.
Restrict permissions on the file:
chmod 400 evidence.txt
Purpose: Changes the permissions of evidence.txt to read-only for the owner and removes all permissions for the group and others. This ensures the file cannot be modified or executed.
Retrieve and save the updated file permissions:
ls -l evidence.txt > evidence-restricted-acl.txt
Purpose: Lists the updated file permissions of evidence.txt and saves the output to a file named evidence-restricted-acl.txt. This shows the restricted permissions after using chmod.
Explanation
mkdir and New-Item: These commands are used to create directories and files in PowerShell. They are cross-platform and work on macOS, Linux, and Windows.
ls -l: This Unix-based command lists file permissions in a human-readable format. It is the macOS equivalent of Get-Acl on Windows.
chmod: This command is used to modify file permissions on macOS and Linux. It allows you to set specific permissions for the owner, group, and others.
## PowerShell Scripting
### Commands and Their Purpose

1. **Create a backup folder:**
   ```powershell
   mkdir Backup
Purpose: Creates a folder named Backup to store copies of critical files.
Copy files to the backup folder:
Copy-Item -Path ./2-Permissions/* -Destination ./Backup -Recurse
Purpose: Copies all files and subfolders from the 2-Permissions folder to the Backup folder. The -Recurse flag ensures that all contents are copied.
Set permissions for the backup folder:
chmod -R 400 Backup
Purpose: Changes the permissions of the Backup folder and its contents to read-only for the owner, ensuring the files cannot be modified or deleted.
Retrieve and save the ACL for the backup folder:
ls -l Backup > Backup-acl.txt
Purpose: Lists the file permissions of the Backup folder and saves the output to a file named Backup-acl.txt. This documents the permissions for auditing purposes.
