# Splunk-SIEM-Lab
Splunk Enterprise SIEM Lab using Sysmon, Splunk Universal Forwarder and Atomic Red Team

1. Introduction
This lab demonstrates the simulation and detection of various cyber attack techniques using Splunk Enterprise, Sysmon, Atomic Red Team and Splunk Universal Forwarder. The objective of this lab is to emulate real-world attacker behavior, collect security logs through Sysmon, forward the logs to Splunk Enterprise and create detection queries to identify malicious activities.

2. Objectives
The objectives of this lab were:
•	Install and configure Splunk Enterprise.
•	Configure Splunk Universal Forwarder.
•	Install and configure Sysmon.
•	Generate attack telemetry using Atomic Red Team.
•	Collect and analyze logs in Splunk.
•	Detect MITRE ATT&CK techniques using SPL queries.
•	Identify Process Name, Command Line, User and Time information from logs.

3. Lab Environment Setup
3.1 Lab Architecture
The lab consisted of two virtual machines:
Machine	Operating System	Purpose
Splunk Server	Ubuntu Server (v20.04.6)	(SIEM) Log Collection & Analysis
Target Machine	Windows Server 2019	Attack Simulation
<img width="753" height="442" alt="image" src="https://github.com/user-attachments/assets/0ded74e5-9c12-4c76-b5ca-9c60814e244b" />

