# Windows 11 Logging & Detection Lab with Splunk

## Objective

Collect and analyze Windows 11 logs in Splunk to detect basic attack behaviors.  
The goal is to forward key events from a hardened Windows 11 Pro workstation into Splunk Free and build a few simple detections using SPL.

## Lab Scenario

A small organization wants better visibility into what is happening on its Windows endpoints  
(failed logons, RDP attempts, suspicious PowerShell), but has no existing SIEM.

- Endpoint: Windows 11 Pro VM in VirtualBox (already hardened in my other lab)
- SIEM: Splunk Free running on a separate VM or host
- Focus: Log collection, search, and simple detection—not enterprise-scale architecture

## Scope

This lab focuses on:

- Configuring Windows 11 logging to send Security and PowerShell events to Splunk
- Using Splunk searches (SPL) to find:
  - Repeated failed logons / potential brute-force attempts
  - Interactive logons over RDP
  - PowerShell executions
- Writing and saving a few basic alerts / dashboards

It does not try to model a full SOC or complex correlation rules.

## Environment

- Windows 11 Pro (VirtualBox VM) as the monitored endpoint
- Splunk Free installation (Linux or Windows VM)
- Winlogbeat / Splunk Universal Forwarder / or another supported method to send Windows events into Splunk

## Methodology

1. Install and configure Splunk Free on a lab VM.
2. Install and configure a Windows event forwarder (e.g., Splunk Universal Forwarder) on the Windows 11 VM.
3. Verify that Security and PowerShell logs are arriving in Splunk.
4. Generate test activity:
   - Failed logon attempts
   - RDP connections
   - PowerShell commands
5. Build SPL searches to identify these behaviors.
6. Save searches as reports/alerts and (optionally) simple dashboards.

## Example Detections (Planned)

- **Failed logon bursts** – multiple 4625 events against the same account within a short time window.
- **RDP logons** – 4624 events where the logon type indicates a remote interactive session.
- **PowerShell activity** – events from PowerShell operational logs or process creation logs referencing `powershell.exe`.

## Artifacts

- `inputs-config-notes.md` – Notes on how Windows events are forwarded into Splunk.
- `searches.md` – SPL queries used for detection and investigation.
- `screenshots/` – (Optional) Splunk search, alert, and dashboard screenshots.

## What This Lab Demonstrates

- Ability to forward Windows 11 security logs into a SIEM (Splunk).
- Basic skill with SPL for searching and detection.
- Understanding of how endpoint hardening, logging, and monitoring fit together.
