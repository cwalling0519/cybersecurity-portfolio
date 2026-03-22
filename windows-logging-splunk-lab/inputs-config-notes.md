System: Windows 11 Pro (VirtualBox VM)
SIEM: Splunk Free (Lab)

These notes document how Windows events are forwarded into Splunk so the lab is reproducible.

Splunk Server
Index created for Windows logs:
Name: windows
Type: events
Expected sourcetypes:
WinEventLog:Security
WinEventLog:System
WinEventLog:Application
(Optional) XmlWinEventLog:Microsoft-Windows-PowerShell/Operational

Installation
Downloaded Splunk Enterprise (Free license for lab) on a separate VM.
Installed Splunk Enterprise with default settings.
Set admin username and strong password during setup.
Confirmed Splunk Web reachable at:
http://<splunk-server-ip>:8000
​

Index configuration
In Splunk Web:
Settings → Indexes → New Index.
Name: windows
Index Data Type: Events
Leave other settings at defaults for lab.
Save.

Splunk Universal Forwarder on Windows 11 VM
Downloaded Splunk Universal Forwarder for Windows (matching version of Splunk Enterprise).
Ran installer as Administrator.
Chose “Forward data to a Splunk indexer”.
Pointed to Splunk server: <splunk-server-ip>:9997.
Set same admin credentials or forwarder credentials as needed.

Windows Event Log inputs (inputs.conf on forwarder)
On the Windows 11 VM (forwarder):
Default path: C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf

This file controls which Windows logs get sent to Splunk.

Example inputs.conf (lab)

[default]
host = win11-lab
index = windows

[WinEventLog]
index = windows

[WinEventLog://Security]
disabled = 0

[WinEventLog://System]
disabled = 0

[WinEventLog://Application]
disabled = 0

[WinEventLog://Microsoft-Windows-PowerShell/Operational]
disabled = 0
renderXml = 1

Key points:
host is set so events show as coming from win11-lab in Splunk.
index is set to windows so all these logs land in the windows index created earlier.
renderXml = 1 for the PowerShell Operational log so detailed event fields are preserved.

File location notes
If inputs.conf does not exist, create it in:
C:\Program Files\SplunkUniversalForwarder\etc\system\local\

Splunk reads local\inputs.conf on restart.

Splunk forwarding config (outputs.conf on forwarder)
On the Windows 11 VM (forwarder):
Default path: C:\Program Files\SplunkUniversalForwarder\etc\system\local\outputs.conf

This file tells the forwarder where to send data.

Example outputs.conf (single indexer lab)

[tcpout]
defaultGroup = splunk_indexer

[tcpout:splunk_indexer]
server = <splunk-server-ip>:9997

[tcpout-server://<splunk-server-ip>:9997]

Key points:
defaultGroup points to the tcpout stanza splunk_indexer.
server uses the Splunk server IP and receiving port 9997.

Enabling receiving on Splunk server
On Splunk Enterprise (server):
Settings → Forwarding and receiving → Receive data.
Enable receiving on port 9997.

This must match the port specified in outputs.conf on the forwarder.

Service control and restarts
On Windows 11 VM (forwarder):
SplunkForwarder service must be running to send logs.

Typical restart steps after changing inputs.conf / outputs.conf:
Open elevated PowerShell or CMD.
cd "C:\Program Files\SplunkUniversalForwarder\bin"
splunk.exe restart

On Splunk server:
Restart Splunk service after index or input changes if needed:
cd "C:\Program Files\Splunk\bin"
splunk.exe restart

Verification in Splunk Search
In Splunk Web, go to Search & Reporting app.

Basic checks:
index=windows | stats count by sourcetype

You should see:
WinEventLog:Security
WinEventLog:System
WinEventLog:Application
(Optional) XmlWinEventLog:Microsoft-Windows-PowerShell/Operational if that input is enabled.

Host check:
index=windows | stats count by host

You should see host = win11-lab (or whatever you set in inputs.conf).

Event sampling checks
Security log example:
index=windows sourcetype=WinEventLog:Security | stats count by EventCode

System log example:
index=windows sourcetype=WinEventLog:System | stats count by EventCode

Application log example:
index=windows sourcetype=WinEventLog:Application | stats count by EventCode 

PowerShell Operational log example (if enabled):
index=windows sourcetype=XmlWinEventLog:Microsoft-Windows-PowerShell/Operational | stats count by EventCode 

Troubleshooting: no data from Windows 11 VM

Check forwarder service
Confirm SplunkForwarder service is running.
If not, start it from Services.msc or restart using splunk.exe restart.

Verify outputs.conf
Confirm server = <splunk-server-ip>:9997 is correct.
Confirm there is no typo in defaultGroup and tcpout stanza names.

Verify inputs.conf
Confirm disabled = 0 for the logs you expect (Security, System, Application, PowerShell Operational).
Confirm index = windows matches the index name created on the server.

Check network and firewall
From Windows 11 VM, test connectivity to Splunk server on 9997 (for example with Test-NetConnection in PowerShell).
Ensure Windows Firewall or any network firewall allows outbound 9997 to the Splunk server.
​

Check Splunk internal logs on forwarder
On the forwarder, look at:
C:\Program Files\SplunkUniversalForwarder\var\log\splunk\splunkd.log

Search for errors related to TcpOutputProc, connection failures, or license issues.
​

Check Splunk server listener
On Splunk server, confirm receiving on 9997 is enabled.
In Splunk Web, Settings → Forwarding and receiving → Receive data.
Also check:
index=_internal source=metrics.log component=TcpInputProc | stats count by host

This can show if the forwarder is connecting.

Optional filtering and tuning
For a small lab, collecting full Security/System/Application logs is fine.
In a bigger environment, you could add whitelists/blacklists in inputs.conf to filter specific Event IDs or channels to control volume.

Example: whitelist only certain Security EventCodes (concept, not required for this lab):

[WinEventLog://Security]
disabled = 0
whitelist = 4624,4625,4672,4688

This is just an example of tuning; the lab uses full logs for simplicity.

Final quick checklist for this lab
Index windows exists on Splunk server.
Splunk server is listening on port 9997.
Windows 11 VM has Splunk Universal Forwarder installed.
outputs.conf on forwarder points to splunk-server-ip:9997 and defaultGroup is set.
inputs.conf on forwarder has WinEventLog stanzas for Security, System, Application, and optionally PowerShell Operational, all with disabled = 0 and index = windows.
SplunkForwarder service is running.
Search index=windows in Splunk and confirm events are visible from host win11-lab.
