# Windows 11 Pro Hardening Baseline (VirtualBox Lab)

## Objective

Harden a Windows 11 Pro workstation running in VirtualBox using a small, practical subset of hardening controls.  
The goal is to reduce common attack surface (RDP, local accounts, services) and improve logging without breaking normal daily use.

## Lab Scenario

A small business uses Windows 11 Pro machines in a simple workgroup (no Active Directory).  
They want better security than the default install but do not have a full‑time IT or security team.

- Environment: Single Windows 11 Pro VM in VirtualBox (lab)
- Role: Standard user workstation used for daily productivity
- Constraints: Changes must not disrupt normal office work (browser, Office, line‑of‑business apps)

## Scope

This lab focuses on:

- Local accounts and password / lockout policy  
- Remote access and network exposure (especially RDP and firewall)  
- Application and execution controls (SmartScreen, AutoRun, basic exploit protection)  
- Logging and audit policy  
- Basic hardening of common services and legacy features  

This is a **practical baseline**, not a full implementation of every CIS Benchmark setting.

## Methodology

1. Start from a fresh Windows 11 Pro VM snapshot in VirtualBox.  
2. Review default settings against a custom hardening checklist in this repo (`checklist.md`).  
3. Apply changes using:
   - Local Security Policy (`secpol.msc`)
   - Local Group Policy (`gpedit.msc`) where needed
   - Windows Security app and built‑in settings
4. Record each change and its path in `changes.md` so the configuration is repeatable.  
5. Reboot and verify that normal user activities still work as expected.  

## Key Hardening Areas

### 1. Local Accounts & Authentication

- Disable or rename the built‑in local Administrator account where appropriate.  
- Enforce stronger password and lockout policies for local accounts.  

### 2. Remote Access & Network

- Disable Remote Desktop if it is not required for this workstation.  
- If RDP is needed, require Network Level Authentication (NLA) and restrict who can connect.  
- Ensure Windows Defender Firewall is enabled on all profiles and remove unnecessary inbound rules.  

### 3. Applications & Execution

- Disable AutoRun / AutoPlay for removable media.  
- Enable Microsoft Defender SmartScreen for apps and browsers.  
- Turn on sensible exploit protection defaults for common applications and the OS.  

### 4. Logging & Auditing

- Enable advanced audit policies for logon events and process creation.  
- Increase the size of Security, System, and Application logs so important events are retained longer.  
- Verify time synchronization so log timestamps are accurate.  

### 5. Services & Features

- Review and disable unneeded services and optional Windows features (for example, legacy protocols like SMBv1 if not required).  
- Turn off remote‑help features such as Remote Assistance when not needed.  

## Artifacts in This Folder

- `checklist.md` – Step‑by‑step Windows 11 hardening checklist used during the lab.  
- `changes.md` – Detailed record of each setting changed, with paths and notes.  
- `sample-screenshots/` (optional) – Before/after screenshots of key settings and Event Viewer views.  

## What This Lab Demonstrates

- Ability to interpret Windows hardening guidance and apply a realistic baseline on Windows 11 Pro.  
- Awareness of usability vs. security trade‑offs on end‑user systems.  
- Clear documentation of changes so another engineer (or future you) can reproduce or audit the configuration.
