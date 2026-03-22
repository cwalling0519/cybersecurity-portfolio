# Windows Hardening Baseline Checklist (Standalone Workstation)

System: Windows 10/11 Pro (Lab VM)  
Date:  
Assessor:  

Status legend: ✅ Done | ⚠️ Review | ⬜ Not Applied

## A. Local Accounts & Authentication

- [ ] A1 – Built-in local Administrator account disabled or renamed
- [ ] A2 – All local accounts use strong, unique passwords
- [ ] A3 – Account lockout policy configured (lockout after several failed attempts)
- [ ] A4 – Password policy configured (minimum length, history, max age as appropriate)

## B. Remote Access & Network

- [ ] B1 – Remote Desktop disabled if not required
- [ ] B2 – If RDP is required, NLA enforced and only specific users/groups allowed
- [ ] B3 – Windows Defender Firewall enabled on all profiles (Domain/Private/Public)
- [ ] B4 – Unused inbound rules reviewed and disabled

## C. Applications & Execution

- [ ] C1 – AutoRun/AutoPlay disabled for removable media
- [ ] C2 – SmartScreen enabled for apps and browsers
- [ ] C3 – Basic exploit protection settings enabled (DEP, ASLR defaults)

## D. Logging & Auditing

- [ ] D1 – Audit policy enabled for logon events and account logon
- [ ] D2 – Audit policy enabled for process creation (event ID 4688 with command line if possible)
- [ ] D3 – Security, System, and Application log sizes increased from defaults
- [ ] D4 – Time synchronization verified (NTP) so logs have accurate timestamps

## E. Services & Features

- [ ] E1 – Unneeded sharing services (e.g., SMB shares) reviewed and disabled where possible
- [ ] E2 – Remote Assistance and other remote-help features disabled if not needed
- [ ] E3 – Optional / legacy features (e.g., SMBv1) disabled if not required

## F. Hardening Validation

- [ ] F1 – User can still perform normal tasks (browser, Office, basic apps)
- [ ] F2 – Event Viewer shows expected audit events (logon, process creation)
- [ ] F3 – Documented changes saved to `changes.md`
