# Splunk Searches (SPL) – Windows 11 Lab

## 1. Repeated Failed Logons (Event ID 4625)

```spl
index=windows sourcetype=WinEventLog:Security EventCode=4625
| stats count by Account_Name, src_ip, host
| where count > 5
| sort - count
index=windows sourcetype=WinEventLog:Security EventCode=4624 Logon_Type=10
| stats count by Account_Name, src_ip, host
| sort - count
index=windows sourcetype=WinEventLog:Security EventCode=4688
Image="*\\powershell.exe"
| table _time, host, Account_Name, CommandLine
| sort - _time
