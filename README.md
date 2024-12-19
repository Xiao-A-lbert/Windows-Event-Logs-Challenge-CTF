# Windows Event Logs Challenge CTF

<h2>Description</h2>
In this Windows Event Log task and challenge, I explored windows event logs and filtered through the command line and powershell. I then completed a CTF by filtering for various windows event ids. 

<h2>Languages and Utilities Used</h2>

- <b>Windows cmd</b>
- <b>POwershell</b>
- <b>Event Viewer</b>

<h2>Environments Used </h2>

- <b>Windows 10 Enterprise</b> 

<br />
<br />
Exploring windows event viewer. Looking at the security logs, observing the event id, and looking at the general details provided for the selected logs. 

![1) security 4624 log](https://github.com/user-attachments/assets/9f500ea2-7c49-44d0-bb7a-323d71843763)

<br />
<br />
Scrolling down will show more meta data about the event log. 

![2) scroll down for meta data](https://github.com/user-attachments/assets/8a210274-73ef-4e94-842c-d921510655af)

<br />
<br />  
Click on filter current log to filter. Added 4624 event id. 

![3) filtering current log](https://github.com/user-attachments/assets/3fe27abd-1694-4780-b4df-2ced3c0dee8f)

<br />
<br />
In cmd, I used "wevtutil qe security /c:5 /f:text /rd:true" to query the Windows Security event log and display the 5 most recent events in a human-readable text format145. Here's a breakdown of the command:
wevtutil qe security: Queries events from the Security log,
/c:5 : Limits the output to the 5 most recent events,
/f:text : Formats the output as readable text instead of XML,
/rd:true : Enables event read direction, displaying the newest events first.

![4) cmd event log query](https://github.com/user-attachments/assets/43e1aa36-a369-4d0d-bcb4-e42a06db3de9)

<br />
<br />
In cmd, I used "wevtutil qe security /c:5 /f:text /rd:true /q:"*[System [(EventID=4720)]]" " to query the Windows Security event log for the 5 most recent events with Event ID 4720, which indicates that a user account was created16. Here's a breakdown of the command:
wevtutil qe security: Queries events from the Security log, 
/c:5 : Limits the output to 5 events, 
/f:text : Formats the output as readable text, 
/rd:true : Displays the newest events first, 
/q:"*[System [(EventID=4720)]]": XPath query to filter for Event ID 4720.

![5) cmd query specific event id logs](https://github.com/user-attachments/assets/d64d60ce-b4f0-47aa-a88d-81fc48b7fa9b)

<br />
<br />
In powershell, I used the command "Get-WinEvent -FilterHashtable @{logname= 'Security'; ID=4624;} -MaxEvents 2 | Format-List *" to retrieve the two most recent successful logon events (Event ID 4624) from the Windows Security log and display all available properties for each event in a list format. Here's what this command does:
Queries the Security log for Event ID 4624 (successful logon), 
Limits the output to the 2 most recent events,
Formats the output as a detailed list showing all properties.

![6) powershell filtering event logs](https://github.com/user-attachments/assets/405b2708-da40-40cc-9bcc-d1c473e2d338)

<br />
<br />
Here is the challenge ctf prompt.

![7) challenge prompt](https://github.com/user-attachments/assets/635f6fbd-abea-4d4b-b2ae-aa802be6387e)

<br />
<br />
The hostname for the computer that generated the logs is found on the very first event. 

![8) hostname](https://github.com/user-attachments/assets/fd56e503-ae8d-4167-aa41-97886fd0057c)

<br />
<br />
For the Process ID that cleared the event log, I had to go into xml view to find the "Execution ProcessID" for the event that cleared the security log. 

![9)execution processid](https://github.com/user-attachments/assets/0bb6025f-af21-403a-8d92-b637088e7e4a)

<br />
<br />
Filtering for Event ID 4720 to find accounts created, I listed the created users in chronological order.

![10) filtering for event id 4720 account creation](https://github.com/user-attachments/assets/a3dfe711-704a-44ba-a688-ba4efab8e190)

<br />
<br />
Filtering for Event ID 4725 to find the sysadmin disabled account. 

![11) sysadmin account was disabled](https://github.com/user-attachments/assets/2d7fce75-e89e-42e5-8850-a229a481338f)

<br />
<br />
Filtering for Event ID 4726 to find the backd00r user deleted account. 

![12) account that was deleted](https://github.com/user-attachments/assets/f15d64b3-3390-4e08-9d36-3750dea08673)

<br />
<br />
Filtering for Event ID 4732 and correlating the Security ID to the backd00r user, I listed the security-enabled local groups this user was added to. 

![13) event id 4732 with SID of backd00r](https://github.com/user-attachments/assets/6c9ff868-b9cb-49c4-a060-da61f1960a07)

<br />
<br />
Filtering for Event ID 4732 and correlating the Security ID to the sysadmin user that was added to Backup Operators. 

![13) correlating SID to a previous question, sysadmin was added to backup operator group](https://github.com/user-attachments/assets/3266e5ab-d84e-495a-9b2d-fe3f5b36c894)

<br />
<br />
