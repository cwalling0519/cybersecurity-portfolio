# Windows 11 Pro Hardening Changes (VirtualBox Lab)

System: Windows 11 Pro (VirtualBox VM)  
Date:  
Assessor:  

This file records the specific settings changed during the hardening lab so the configuration can be repeated or rolled back.

---

## 1. Local Accounts & Authentication

- Disabled/renamed built-in Administrator account:  
  - Path / Tool: `Computer Management -> Local Users and Groups -> Users`  
  - Change:

- Password and lockout policy:  
  - Path / Tool: `secpol.msc -> Account Policies`  
  - Changes:

---

## 2. Remote Access & Network

- Remote Desktop settings:  
  - Path / Tool: `Settings -> System -> Remote Desktop`  
  - Change:

- Firewall rules adjusted:  
  - Path / Tool: `wf.msc`  
  - Changes:

---

## 3. Applications & Execution

- AutoRun/AutoPlay:  
  - Path / Tool: `Control Panel -> AutoPlay` or `gpedit.msc`  
  - Change:

- SmartScreen / Exploit protection:  
  - Path / Tool: Windows Security -> App & browser control  
  - Changes:

---

## 4. Logging & Auditing

- Audit policy:  
  - Path / Tool: `secpol.msc -> Advanced Audit Policy Configuration`  
  - Changes:

- Log sizes:  
  - Path / Tool: Event Viewer -> Log Properties  
  - Changes:

---

## 5. Services & Features

- Disabled services/features:  
  - Path / Tool: `services.msc` or `Optional features`  
  - Changes:

---

## 6. Validation Notes

- Normal user tasks tested:  
- Any issues encountered / mitigations:
