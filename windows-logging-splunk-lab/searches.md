System: Windows 11 Pro (VirtualBox VM)
SIEM: Splunk Free (Lab)
Index: windows

These searches show how I investigated Windows Security, System, Application, and PowerShell logs in Splunk, focusing on detections a junior SOC analyst or blue teamer would actually use (failed logons, RDP activity, process creation, and basic threat hunting).

Splunk Searches (SPL) – Windows 11 Lab
1. Environment and health checks
These searches confirm that data is arriving from the Windows 11 VM, fields are parsed correctly, and there are no obvious ingestion gaps.

All events from the lab index:
index=windows

Events by sourcetype (validates inputs.conf):
index=windows
| stats count by sourcetype

Events by host (validates host field in inputs.conf):
index=windows
| stats count by host

Time distribution (look for gaps):
index=windows
| timechart span=5m count

Security vs System vs Application over time:
index=windows sourcetype=WinEventLog:*
| eval logtype=case(
sourcetype="WinEventLog:Security","Security",
sourcetype="WinEventLog:System","System",
sourcetype="WinEventLog:Application","Application",
1=1,"Other"
)
| timechart span=10m count by logtype

2. Windows Security log – authentication and account activity
These searches investigate failed and successful logons, brute force patterns, and privileged logons using common Windows Security Event IDs such as 4625, 4624, 4672, and 4740.

Top Security EventCodes (what’s happening the most):
index=windows sourcetype=WinEventLog:Security
| stats count by EventCode
| sort - count

Failed logons (EventCode 4625) with key context:
index=windows sourcetype=WinEventLog:Security EventCode=4625
| table _time host Account_Name src_ip Logon_Type Failure_Reason

Failed logons aggregated by user (possible brute force against accounts):
index=windows sourcetype=WinEventLog:Security EventCode=4625
| stats count values(host) as hosts values(src_ip) as src_ips by Account_Name
| sort - count

Failed logons aggregated by source IP (possible password spraying from one IP):
index=windows sourcetype=WinEventLog:Security EventCode=4625
| stats count values(Account_Name) as accounts by src_ip
| sort - count

Brute-force style pattern – 5+ failures by same user in 1 minute:
index=windows sourcetype=WinEventLog:Security EventCode=4625
| bin _time span=1m
| stats count values(src_ip) as src_ips by _time Account_Name
| where count >= 5
| sort - _time count

Successful logons (EventCode 4624) – who actually got in:
index=windows sourcetype=WinEventLog:Security EventCode=4624
| table _time host Account_Name src_ip Logon_Type Authentication_Package

Admin-equivalent logons (EventCode 4672 – special privileges assigned):
index=windows sourcetype=WinEventLog:Security EventCode=4672
| table _time host Account_Name Privileges

Account lockouts (EventCode 4740 – potential attack or misconfig):
index=windows sourcetype=WinEventLog:Security EventCode=4740
| table _time host Target_Account_Name Caller_Computer_Name

3. Windows System and Application logs – stability and errors
These searches look at errors and common noise in System and Application logs to spot instability, failing services, or misconfigurations.

Top System EventCodes:
index=windows sourcetype=WinEventLog:System
| stats count by EventCode
| sort - count

System errors over time:
index=windows sourcetype=WinEventLog:System Level=Error
| timechart span=10m count

Top Application EventCodes:
index=windows sourcetype=WinEventLog:Application
| stats count by EventCode
| sort - count

Application errors by source:
index=windows sourcetype=WinEventLog:Application Level=Error
| stats count by SourceName EventCode
| sort - count

4. Process creation and PowerShell – early threat hunting
These searches move toward threat hunting by looking at process creation (EventCode 4688, if enabled) and PowerShell Operational logging, which are typical starting points for detecting execution and abuse on Windows endpoints.

All PowerShell Operational events (Script Block Logging):
index=windows sourcetype=XmlWinEventLog:Microsoft-Windows-PowerShell/Operational

PowerShell events by EventCode:
index=windows sourcetype=XmlWinEventLog:Microsoft-Windows-PowerShell/Operational
| stats count by EventCode
| sort - count

PowerShell with script block text (field names can vary by environment):
index=windows sourcetype=XmlWinEventLog:Microsoft-Windows-PowerShell/Operational
| table _time host EventCode ScriptBlockText

Generic process creation (Security EventCode 4688 – if enabled):
index=windows sourcetype=WinEventLog:Security EventCode=4688
| stats count by New_Process_Name Process_Command_Line
| sort - count

Focus on powershell.exe process creation:
index=windows sourcetype=WinEventLog:Security EventCode=4688 New_Process_Name="*\powershell.exe"
| table _time host Account_Name Process_Command_Line New_Process_Name

Rare processes (possible malware or LOLBins):
index=windows sourcetype=WinEventLog:Security EventCode=4688
| stats count by New_Process_Name
| sort count
| head 20

5. Focused attack scenario – brute force, RDP, and malicious PowerShell
This section ties three related detections together into a simple narrative a hiring manager or interviewer can follow: brute-force attempts (4625), successful RDP logons (4624 Logon_Type 10), and suspicious PowerShell spawned by a user.

5.1 Repeated failed logons (brute force pattern)
index=windows sourcetype=WinEventLog:Security EventCode=4625
| stats count by Account_Name src_ip host
| where count > 5
| sort - count

What it shows: Accounts with more than 5 failed logon attempts from a given source IP/host, which can indicate brute-force or password spraying against a single user or small set of users.

5.2 Successful RDP logons (EventCode 4624, Logon_Type=10)
index=windows sourcetype=WinEventLog:Security EventCode=4624 Logon_Type=10
| stats count by Account_Name src_ip host
| sort - count

What it shows: Users successfully logging in via Remote Desktop (logon type 10), which helps confirm whether an attacker ever turned failed attempts into a real remote session on the target.

5.3 PowerShell spawned by users (Security EventCode 4688)
index=windows sourcetype=WinEventLog:Security EventCode=4688 Image="*\powershell.exe"
| table _time host Account_Name CommandLine
| sort - _time

What it shows: PowerShell executions (by user and command line) following authentication, which is a common way for attackers to run discovery and post-exploitation commands once they land on a system.

6. Log tampering and suspicious gaps
These searches help detect activity where attackers may try to cover their tracks by clearing logs or creating long time gaps in events.

Detect potential log clearing in Windows logs (Security/System):
index=windows sourcetype=WinEventLog:* EventCode IN (1100,1102,104)
| stats count by _time EventCode Message host sourcetype

Look for 30-minute gaps with zero Security events (possible collection issue or tampering):
index=windows sourcetype=WinEventLog:Security
| bin _time span=30m
| stats count by _time
| where count=0

7. Quick “cheat sheet” queries
These are the handful of queries I’d likely use live in an interview or screen share to demonstrate my Splunk skills quickly.

Basic health – events by sourcetype:
index=windows | stats count by sourcetype

Failed logons by user:
index=windows sourcetype=WinEventLog:Security EventCode=4625
| stats count by Account_Name

Possible brute-force (5 failures in 1 minute):
index=windows sourcetype=WinEventLog:Security EventCode=4625
| bin _time span=1m
| stats count by _time Account_Name
| where count >= 5

Successful logons:
index=windows sourcetype=WinEventLog:Security EventCode=4624

System errors over time:
index=windows sourcetype=WinEventLog:System Level=Error
| timechart span=10m count

PowerShell Operational events (if enabled):
index=windows sourcetype=XmlWinEventLog:Microsoft-Windows-PowerShell/Operational
