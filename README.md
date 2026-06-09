# Splunk-SIEM-Lab
Splunk Enterprise SIEM Lab using Sysmon, Splunk Universal Forwarder and Atomic Red Team

# 1. Introduction
This lab demonstrates the simulation and detection of various cyber attack techniques using Splunk Enterprise, Sysmon, Atomic Red Team and Splunk Universal Forwarder. The objective of this lab is to emulate real-world attacker behavior, collect security logs through Sysmon, forward the logs to Splunk Enterprise and create detection queries to identify malicious activities.

# 2. Objectives
The objectives of this lab were:
- Install and configure Splunk Enterprise.
- Configure Splunk Universal Forwarder.
- Install and configure Sysmon.
- Generate attack telemetry using Atomic Red Team.
- Collect and analyze logs in Splunk.
- Detect MITRE ATT&CK techniques using SPL queries.
- Identify Process Name, Command Line, User and Time information from logs.

# 3. Lab Environment Setup
# 3.1 Lab Architecture

The lab consisted of two virtual machines:
Machine	Operating System	Purpose
Splunk Server	Ubuntu Server (v20.04.6)	(SIEM) Log Collection & Analysis
Target Machine	Windows Server 2019	Attack Simulation
<img width="753" height="442" alt="image" src="https://github.com/user-attachments/assets/0ded74e5-9c12-4c76-b5ca-9c60814e244b" />

# 3.2 Ubuntu Server Configuration:

1. Download Splunk Enterprse from https://www.splunk.com/en_us/download/splunk-enterprise.html
<img width="749" height="726" alt="image" src="https://github.com/user-attachments/assets/61f750a0-d9ad-49e2-9f50-68ab37e9be2a" />
<br>
<br>
2. Now open a Terminal and run  sudo apt update && sudo apt upgrade -y  and enter your root password
<br>
<br>
<img width="304" height="356" alt="image" src="https://github.com/user-attachments/assets/3c59acc5-9649-420f-af42-fdf4b01358b5" />
<img width="773" height="311" alt="image" src="https://github.com/user-attachments/assets/794987d5-d000-4fd9-a749-ba15429bbfe8" />
<br>
<br>
3. Now open a new Terminal in Downloads directory and run -->
<br>
<b>sudo su</b>
<br>
<b>dpkg -i splunk*.deb</b>
<br>
<b>/opt/splunk/bin/splunk start --run-as-root</b>
<br>
<br>
<img width="691" height="446" alt="image" src="https://github.com/user-attachments/assets/950905f8-68bc-4373-95ce-1b951420bd93" />
<img width="684" height="358" alt="image" src="https://github.com/user-attachments/assets/e69d19ad-ed22-439e-b7f2-74f330a40bff" />
<br>
<br>
4. Write a username and password for login Splunk server
<br>
<br>
<img width="771" height="350" alt="image" src="https://github.com/user-attachments/assets/1d7dc66f-6080-421b-82ff-44a287078328" />
<br>
<br>
5. Now copy this link <b>(http://ubun2004:8000)</b> and go to a </b>latest version browser</b>. Paste this link and enter the created username and password.
<br>
<br>
<img width="705" height="458" alt="image" src="https://github.com/user-attachments/assets/a1a9bece-9936-495a-8894-2c16aa45bd71" />
<img width="719" height="378" alt="image" src="https://github.com/user-attachments/assets/ffe0bb82-5bfd-455e-bbcc-9380e317d617" />
<br>
<br>
6. Now click <b>Settings > Forwarding and receiving</b> and configure receiving (port: 9997).
<br>
<br>
<img width="691" height="256" alt="image" src="https://github.com/user-attachments/assets/045f1b34-5a4c-40d7-9a27-d99e28291205" />
<img width="647" height="311" alt="image" src="https://github.com/user-attachments/assets/117da9b2-fa81-486d-884c-27800e430567" />
<img width="655" height="129" alt="image" src="https://github.com/user-attachments/assets/83b4112b-9bde-4c82-83b0-ec5ca287e2ae" />
<img width="624" height="172" alt="image" src="https://github.com/user-attachments/assets/d22165f7-64ad-4223-9234-efcc441399dd" />
<img width="764" height="175" alt="image" src="https://github.com/user-attachments/assets/47c08c9f-6d14-407e-ac2f-1ade8eb5a602" />
<br>
<br>
7. Create an <b>index in splunk (wineventlog)</b>
<br>
<br>
Run--> <b>/opt/splunk/bin/splunk add index wineventlog</b>
<br>
Check created index--> <b>/opt/splunk/bin/splunk list index</b>
<br>
<br>
Now restart the splunk server--> <b>/opt/splunk/bin/splunk restart --run-as-root</b>
<br>
<br>
<img width="782" height="236" alt="image" src="https://github.com/user-attachments/assets/7440e40f-ac9d-4edd-b9ce-2ec965cde447" />
<img width="791" height="244" alt="image" src="https://github.com/user-attachments/assets/288599ec-c350-40f7-bd0c-2e9a728a7783" />
<br>
<br>
8. Download <b>Splunk Add-on for Microsoft Windows</b> from: https://splunkbase.splunk.com/ and install it following instruction-->
<br>
<br>
<img width="795" height="272" alt="image" src="https://github.com/user-attachments/assets/29bcb1e1-1018-44d9-af6c-45b348ac1140" />
<img width="705" height="376" alt="image" src="https://github.com/user-attachments/assets/ff55eebb-7681-4f5a-a907-14157e1c1eb7" />
<img width="742" height="273" alt="image" src="https://github.com/user-attachments/assets/d12d9131-0b12-49f5-9942-3c5f2d2fca5e" />
<img width="637" height="308" alt="image" src="https://github.com/user-attachments/assets/387ff5b5-b94d-4d96-8dca-481a13ab8d42" />
<img width="627" height="270" alt="image" src="https://github.com/user-attachments/assets/6f6013bf-73a8-47a6-911b-6145d380f892" />
<img width="641" height="316" alt="image" src="https://github.com/user-attachments/assets/be41c6b1-7836-4703-9bbb-2963ff74b0a7" />
<img width="611" height="290" alt="image" src="https://github.com/user-attachments/assets/4c62ef6d-4460-48b7-9245-34bdb66c668a" />

# 3.3 Windows Server Configuration

1. Download and Install Splunk forwarder form: https://www.splunk.com/en_us/download/universal-forwarder.html
<br>
<img width="490" height="379" alt="image" src="https://github.com/user-attachments/assets/c3a6f6f3-7efc-49da-9f6f-a47fba36b094" />
<img width="485" height="381" alt="image" src="https://github.com/user-attachments/assets/4651ec57-cd3c-4b6e-9bbe-42070d01cbcf" />
<br>
<br>
2. Enter a username and password for forwarder
<br>
<br>
<img width="513" height="400" alt="image" src="https://github.com/user-attachments/assets/2b51f293-551b-4644-a8be-352e6bfcc5af" />
<img width="479" height="372" alt="image" src="https://github.com/user-attachments/assets/dfbae0c3-8270-43da-b910-43316a98ccaa" />
<img width="481" height="377" alt="image" src="https://github.com/user-attachments/assets/71277774-6248-4d45-87fd-7826db1b9cc7" />
<img width="629" height="494" alt="image" src="https://github.com/user-attachments/assets/3cfdbb0b-7620-4104-a40a-15b0b2f0a9c1" />
<br>
<br>
3. Enter Splunk server IP (Ubuntu server IP)

Check Ubuntu server IP:
<br>
<br>
<img width="542" height="287" alt="image" src="https://github.com/user-attachments/assets/b140d2cc-e5d3-4394-8f9b-b02fd90d9004" />
<img width="470" height="368" alt="image" src="https://github.com/user-attachments/assets/d96e86cc-ab87-4100-be1e-8a42798742f4" />
<img width="458" height="359" alt="image" src="https://github.com/user-attachments/assets/9bb54218-467c-449c-ac56-c04587c37001" />
<img width="435" height="343" alt="image" src="https://github.com/user-attachments/assets/81b59ea0-378b-4a50-bfa5-e8d9bd4a2fe9" />
<br>
<br>
4. Now go to <b>Local Disk (C:) > Program Files > SplunkUniversalForwarder > etc > system > local</b> and Create an <b>inputs.conf</b> file
<br>
<br>
<img width="496" height="369" alt="image" src="https://github.com/user-attachments/assets/5264c68d-57df-4504-a679-2c9cb72be016" />
<img width="659" height="225" alt="image" src="https://github.com/user-attachments/assets/294694fa-82f2-40b1-ab88-fb6bbba47bf9" />
<br>
<br>
5. Open <b>inputs.conf</b> file and edit as image instruction and save-->
<br>
<br>
<img width="670" height="400" alt="image" src="https://github.com/user-attachments/assets/52762817-5ca6-4cbd-b75c-b0630d475446" />
<br>
<br>
6. Check “SplunkForwarder status running” in <b>services</b>-->
<br>
<br>
<img width="735" height="467" alt="image" src="https://github.com/user-attachments/assets/f1a47534-e1b0-4ca1-a228-aa0aa785523e" />
<br>
<br>
7. Now download <b>Sysmon</b> and setup from: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
<br>
<br>
<img width="668" height="328" alt="image" src="https://github.com/user-attachments/assets/f042f6d9-8189-4902-b314-cbd49b8fc49d" />
<br>
<br>
8. Download <b>sysmonconfig.xml</b> from: https://github.com/swiftonsecurity/sysmon-config
<br>
<br>
<img width="732" height="282" alt="image" src="https://github.com/user-attachments/assets/18e49de7-e60a-4aaf-86b2-1699970e25d8" />
<br>
<br>
9. Now go to downloads folder, then extract <b>Sysmon Zip</b> file, then copy <b>Sysmon64.exe</b> and paste downloads folder and follow the steps:
<br>
<br>
<img width="670" height="323" alt="image" src="https://github.com/user-attachments/assets/9af37d74-bd38-4803-9408-117c40e7515b" />
<br>
<br>
10. Now open cmd run as administrator and install <b>Sysmon64</b> -->
<br>
<br>
<img width="558" height="342" alt="image" src="https://github.com/user-attachments/assets/78fb3789-a693-414f-be95-7c5bb77bc25a" />
<img width="803" height="311" alt="image" src="https://github.com/user-attachments/assets/76cb4190-91f9-4501-9ec5-f2d516cbc8c2" />
<br>
<br>
11. Now check Sysmon successful installation. Go to <b>Event Viewer</b> -->
<br>
<br>
<img width="351" height="372" alt="image" src="https://github.com/user-attachments/assets/e019f61b-4d30-43f9-8e90-372048fb9ed5" />
<img width="277" height="516" alt="image" src="https://github.com/user-attachments/assets/d88c8d98-f382-426c-b477-abb8d3d61b84" />
<br>
<br>
Sysmon installed successfully and store event 
<br>
<img width="672" height="489" alt="image" src="https://github.com/user-attachments/assets/7de8a1c6-645e-49e4-9080-b4c9103dbc6b" />

# 3.4 Atomic Red Team Setup

1. Now open Powershell run as administrator and run the following command-->

<b>Set-ExecutionPolicy Bypass -Scope Process</b>
<br>
<b>IEX (IWR ‘https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1’ -UseBasicParsing)</b>
<br>
<br>
<img width="813" height="207" alt="image" src="https://github.com/user-attachments/assets/32d18ebe-4c81-4a96-9ffe-6d7d58f66378" />
<br>
<br>
2. Go to <b>Local Disk (C:) > AtomicRedTeam</b> folder. If there not found <b>“atomics”</b> folder following the next instruction (3 to 5), otherwise skip.
<br>
<br>
<img width="719" height="240" alt="image" src="https://github.com/user-attachments/assets/afe46d99-dcce-4418-8270-623fdb73be6b" />
<br>
<br>
3. Open virus & threat protection and turn off protection-->
<br>
<br>
<img width="396" height="412" alt="image" src="https://github.com/user-attachments/assets/d72bd35b-3df5-4624-9a68-36f93abd6448" />
<img width="469" height="363" alt="image" src="https://github.com/user-attachments/assets/816d685f-0a2c-4320-91b9-6075dbd4a528" />
<img width="292" height="421" alt="image" src="https://github.com/user-attachments/assets/746c5045-db88-4a5d-94d1-9c59a5a463d7" />
<img width="415" height="367" alt="image" src="https://github.com/user-attachments/assets/5eae1fe5-f404-4757-9e33-ad137495ae88" />
<br>
<br>
4. Now download atomic-red-team zip file from: https://github.com/redcanaryco/atomic-red-team and extract the zip file.
<br>
<br>
<img width="545" height="373" alt="image" src="https://github.com/user-attachments/assets/8caa1a7e-39c4-473e-af90-df6542d2ca86" />
<img width="547" height="254" alt="image" src="https://github.com/user-attachments/assets/72e5bbb3-fadf-4a90-b423-b2a0c92cc858" />
<br>
<br>
5. Go to <b>atomic-red-team-master</b> folder and copy <b>“atomics”</b> folder and paste it in <b>“Local Disk (C:) > AtomicRedTeam”</b> folder-->
<br>
<br>
<img width="673" height="291" alt="image" src="https://github.com/user-attachments/assets/37257ec7-353a-452e-bb07-5f88bbfa841e" />
<img width="522" height="426" alt="image" src="https://github.com/user-attachments/assets/ac45a0e5-8052-417e-877d-9a6d649382ce" />
<img width="502" height="158" alt="image" src="https://github.com/user-attachments/assets/d63a5db4-efbe-48ba-a844-e9f13c8c8996" />
<br>
<br>
6. Now install atomic red team-->
<br>
	<b>Install-AtomicRedTeam</b>
    <br>
    <b>Install-Module –Name Invoke-AtomicRedTeam -Force</b>
    <br>
	<b>Import-Module Invoke-AtomicRedTeam</b>
<br>
<br>
<img width="975" height="58" alt="image" src="https://github.com/user-attachments/assets/42396510-d605-4528-a0b7-a1b0a37e3746" />
<img width="894" height="51" alt="image" src="https://github.com/user-attachments/assets/5a7ed2d5-878e-436f-a8c2-0aa89cc27dc9" />

# 4. Attack Simulation and Detection

**Attack 1: T1053.005 (Persistence) | Scheduled Task**
<br>
A malicious scheduled task was created using Atomic Red Team. 
<br>
<br>
<img width="804" height="364" alt="image" src="https://github.com/user-attachments/assets/a85717fd-b0a8-444e-a19a-17e82b0bd7f2" />
<br>
<br>
**Detection and Query:**
<br>
<br>
index=wineventlog source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1
<br>
| search schtasks.exe
<br>
| table _time Image CommandLine ParentImage User
<br>
<br>
<img width="745" height="370" alt="image" src="https://github.com/user-attachments/assets/cd1087e8-ad46-4ef4-8148-6f2952ce6705" />
<br>
<br>
Sysmon Event ID: 1 (Process Creation)
<br>
Event ID 1 records process creation activities. It was the most useful event because it captured the execution of <b>schtasks.exe</b> along with the full command line, allowing identification of the malicious scheduled task creation.
<br>
<br>
**Attack 2: T1218.005 (Defense Evasion) | MSHTA**
<br>
A malicious HTA file was executed using mshta.exe.
<br>
<br>
<img width="609" height="168" alt="image" src="https://github.com/user-attachments/assets/681764d8-d6d6-4f6c-b036-a37ca86f94f9" />
<br>
<br>
**Detection and Query:**
<br>
<br>
index=wineventlog source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1
<br>
| search mshta.exe
<br>
| table _time Image CommandLine ParentImage User
<br>
<br>
<img width="757" height="323" alt="image" src="https://github.com/user-attachments/assets/8b963774-74c4-4ca4-a94b-0d2116d7ec8d" />
<br>
<br>
Sysmon Event ID: 1 (Process Creation)
<br>
Event ID 1 captured the execution of mshta.exe and its associated command-line arguments. This made it possible to identify the use of MSHTA for executing a malicious HTA file.
<br>
<br>
**Attack 3: T1003.001 (Credential Access) | LSASS Dumping**
<br>
The attack attempted to access the LSASS process memory.
<br>
<br>
<img width="637" height="245" alt="image" src="https://github.com/user-attachments/assets/7fa8e065-755f-418e-a6e4-6588e13d2c7c" />
<br>
<br>
**Detection and Query:**
<br>
<br>
index=wineventlog source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1
<br>
| search procdump.exe OR lsass.exe
<br>
| table _time Image CommandLine ParentImage User
<br>
<br>
<img width="975" height="432" alt="image" src="https://github.com/user-attachments/assets/7ac4b49c-5bc5-4f71-aaac-fe33e1311f4c" />
<br>
<br>
Sysmon Event ID: 1 (Process Creation)
<br>
Event ID 1 was the most useful event for detecting the LSASS Dumping attack because it recorded the creation of the process responsible for dumping the LSASS memory. The command line showed the execution of the dump operation and the creation of the file lsass_dump.dmp, which provided strong evidence of a credential dumping attempt.
<br>
<br>
**Attack 4: T1059.001 (Execution) | PowerShell Download**
<br>
PowerShell was used to download and execute a script.
<br>
<br>
<img width="705" height="248" alt="image" src="https://github.com/user-attachments/assets/c57839a2-0714-423d-91f8-4a9b2af04d34" />
<br>
<br>
**Detection and Query:**
<br>
<br>
index=wineventlog source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=1
<br>
| search "DownloadString" OR "Invoke-WebRequest" OR "IEX"
<br>
| table _time Image CommandLine ParentImage User
<br>
<br>
<img width="975" height="422" alt="image" src="https://github.com/user-attachments/assets/6e308f85-6af5-49d5-8540-14ba36a38b68" />
<br>
<br>
Sysmon Event ID: 1 (Process Creation)
<br>
Event ID 1 captured the execution of PowerShell and displayed the command line containing download-related commands such as Invoke-WebRequest, helping identify malicious script execution.
<br>
<br>
**Attack 5: T1112 (Defense Evasion) | Registry Modification**
<br>
Registry keys were modified to alter system behavior.
<br>
<br>
<img width="690" height="336" alt="image" src="https://github.com/user-attachments/assets/4f103993-3563-4a81-8ffe-1b96415a5640" />
<br>
<br>
**Detection and Query:**
<br>
<br>
index=wineventlog source="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventCode=13
<br>
| table _time TargetObject Details User
<br>
<br>
<img width="975" height="429" alt="image" src="https://github.com/user-attachments/assets/e5646762-83c4-4f01-8ae0-2bb72f6b1e90" />
<br>
<br>
Sysmon Event ID: 13 (Registry Value Set)
<br>
Event ID 13 records registry value modifications. It was the most useful event because it directly captured changes made to registry keys associated with Windows Defender configuration.

# 5. Splunk Dashboard

A dashboard was created to monitor Sysmon activity and attack indicators.
<br>
1.	Go to splunk home page and click “Created by you”, then click “create a dashboard”
<br>
<img width="635" height="307" alt="image" src="https://github.com/user-attachments/assets/f087e141-56ce-4eb8-80d5-afb26a1bd7e6" />
<img width="731" height="278" alt="image" src="https://github.com/user-attachments/assets/c013f239-2b30-4e9c-82c6-b5b4c5a3ad5c" />
<br>
<br>
2.	Write a title of the Dashboard. Then Scroll down and select a Dashboard type and click create.
<br>
<br>
<img width="501" height="397" alt="image" src="https://github.com/user-attachments/assets/46eacb9b-b855-4ae5-b133-cfa3eea5069d" />
<img width="603" height="481" alt="image" src="https://github.com/user-attachments/assets/e093b818-6080-4e4e-b37f-66de4f40d3ae" />
<br>
<br>
3.	Now click Add Panel > New > Single Value and following
<br>
<br>
<img width="679" height="300" alt="image" src="https://github.com/user-attachments/assets/bc9524b4-3920-41fe-bc8c-2850be3ddb96" />
<br>
<br>
This query show <b>Total Sysmon Events</b>
<br>
<img width="481" height="385" alt="image" src="https://github.com/user-attachments/assets/ae281170-6a7d-411c-a2c2-3f633360ae69" />
<br>
<br>
4.	Same step again….
<br>
<br>
This query show <b>Recent process creation events</b>
<br>
<img width="584" height="335" alt="image" src="https://github.com/user-attachments/assets/51cb341d-41ca-4a13-9b93-0915c7f77013" />
<br>
<br>
This query show <b>Sysmon Event Distribution</b>
<br>
<img width="697" height="336" alt="image" src="https://github.com/user-attachments/assets/f4b01e4c-c9c4-45e6-be28-b3e9d42baa69" />
<br>
<br>
This query show <b>Registry Modification Events</b>
<br>
<img width="706" height="362" alt="image" src="https://github.com/user-attachments/assets/5ac0c773-8fa2-4def-9720-0ada03489641" />
<br>
<br>
This query show <b>LSASS Access Attempts</b>
<img width="689" height="385" alt="image" src="https://github.com/user-attachments/assets/71e232b4-2b2b-4def-9c50-f6562e3ce895" />
<br>
<br>
This query show <b>Powershell Activity Events</b>
<br>
<img width="685" height="412" alt="image" src="https://github.com/user-attachments/assets/7b07e410-ed30-45ae-906f-bdd58ae90bc6" />
<br>
<br>
See the Output:
<br>
<img width="675" height="178" alt="image" src="https://github.com/user-attachments/assets/4fcb42cd-a65d-4fca-8a0b-f950976c7c41" />
<img width="795" height="301" alt="image" src="https://github.com/user-attachments/assets/354d80f4-80a9-486f-b80f-a55ea2f932a7" />
<img width="797" height="307" alt="image" src="https://github.com/user-attachments/assets/e7f0411a-3c32-4b34-b530-c7823f58952c" />
<br>
<br>
5.	Click Save
<br>
<br>
<img width="651" height="173" alt="image" src="https://github.com/user-attachments/assets/753e20ea-cc6d-439f-8968-d1719672c446" />
<br>
<br>
6.	Now go to <b>home page, click Dashboard > Choose a home dashboard</b>
<br>
<br>
<img width="823" height="362" alt="image" src="https://github.com/user-attachments/assets/9e8f65f3-d95f-46d8-bfa2-f28f3accb386" />
<br>
<br>
7.	Select created Dashboard and click Save
<br>
<br>
<img width="797" height="302" alt="image" src="https://github.com/user-attachments/assets/fdcc55e1-a981-4615-a3e0-ac416163c7da" />
<br>
<br>
Dashboard Result Show:
<br>
<img width="753" height="293" alt="image" src="https://github.com/user-attachments/assets/4c8ecd1a-66a8-40a5-8ab6-1bb357b3038b" />

# 7. Challenges and Solutions

- Challenge 1: Sysmon Fields Not Appearing in Splunk

Initially, Sysmon fields such as EventCode, Image, and CommandLine were not displayed correctly in Splunk. This issue was resolved by enabling XML rendering <b>(renderXml=true)</b> in the Splunk Universal Forwarder configuration and installing the Splunk Add-on for Microsoft Windows.

- Challenge 2: Event Detection Queries Returning No Results

Some detection queries returned no results because Sysmon events were stored under the <b>XmlWinEventLog:Microsoft-Windows-Sysmon/Operational</b> source instead of the standard Windows Event Log source. Updating the search queries to use the correct source resolved the issue.

- Challenge 3: Splunk Dashboard Creation Error

While creating the Splunk dashboard, the error <b>e.toReversed is not a function</b> occurred. The issue was caused by using an outdated Firefox browser version. Updating the browser or using a modern browser resolved the problem.

# 8. Conclusion
This lab demonstrated the deployment of a SOC monitoring environment using Splunk, Sysmon, and Atomic Red Team. Five MITRE ATT&CK techniques were successfully executed and detected using Sysmon event logs. The exercise provided practical experience in attack detection, log analysis and security monitoring.










