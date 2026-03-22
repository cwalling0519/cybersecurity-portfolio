# Windows Hardening Baseline (Standalone Workstation)

## Objective

Harden a standalone Windows 10/11 workstation using a small, practical subset of CIS-style recommendations.  
The goal is to reduce common attack surface (RDP, local accounts, services) and improve logging without breaking normal daily use.

## Scenario

A small business uses Windows 10/11 machines joined to a simple workgroup (no Active Directory).  
They want better security than default settings but do not have a full-time IT or security team.

- Environment: Single Windows 10/11 Pro VM (lab)
- Role: Standard user workstation used for daily productivity
- Constraints: Changes must not disrupt normal office work

## Scope

This lab focuses on:

- Local accounts and password policy
- Remote access and network exposure (RDP, firewall)
- Application control basics (smart defaults, not full whitelisting)
- Logging and audit policy
- Basic hardening of common services and features

It does **not** attempt full CIS coverage—this is a practical baseline.

## Methodology

1. Start from a fresh Windows 10/11 Pro VM snapshot.
2. Review default settings against a small custom hardening checklist inspired by public Windows hardening resources and CIS Benchmarks.[web:163][web:168]
3. Apply changes using local security policy, built-in settings, and a few registry or PowerShell tweaks where needed.[web:155][web:163]
4. Reboot and validate that normal user tasks (browser, Office, line-of-business apps) still work.
5. Document the changes, including before/after notes and key registry / policy paths.

## Key Hardening Areas

- **Accounts & Login**
  - Disable or rename built-in local admin where appropriate.
  - Require non-trivial passwords and lockout on repeated failures.

- **Remote Access**
  - Disable RDP if not required; otherwise restrict it and require NLA.
  - Confirm Windows Firewall is enabled and using sane profiles.

- **Applications & Browser**
  - Tighten SmartScreen and basic exploit protection.
  - Reduce auto-run / auto-play behavior.

- **Logging & Auditing**
  - Enable enhanced audit policies for logon, process creation, and object access.
  - Increase log sizes for Security, System, and Application logs.

## Artifacts

- `checklist.md` – Windows hardening checklist used during the lab.
- `changes.md` – List of specific settings changed (policy paths, registry keys, or GUI steps).
- `screenshots/` – (Optional) Before/after screenshots of key settings and Event Viewer.

## What This Demonstrates

- Ability to interpret Windows hardening guidance and apply a practical subset on a workstation.[web:163][web:168]
- Awareness of the trade-off between security and usability.
- Skill in documenting changes so they can be repeated or rolled back if needed.
