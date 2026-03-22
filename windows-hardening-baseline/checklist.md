# Windows 11 Pro Hardening Checklist (VirtualBox Lab)

System: Windows 11 Pro (VirtualBox VM)  
Date:  
Assessor:  

Status legend: ✅ Done | ⚠️ Review | ⬜ Not Applied

---

## A. Local Accounts & Sign‑in

- [ ] A1 – Built‑in **Administrator** account disabled or renamed
- [ ] A2 – All local accounts have strong, unique passwords
- [ ] A3 – Password policy set (min length ≥ 12, password history, max age as desired)
- [ ] A4 – Account lockout policy set (lock after X failed attempts, reasonable duration)
- [ ] A5 – Fast user switching disabled if not needed

---

## B. Remote Access & Network

- [ ] B1 – Remote Desktop **disabled** if not required
- [ ] B2 – If RDP is required, NLA enforced and only specific users allowed
- [ ] B3 – Windows Defender Firewall **On** for Domain/Private/Public profiles
- [ ] B4 – Unneeded inbound firewall rules removed/disabled
- [ ] B5 – File and printer sharing disabled if not needed

---

## C. Applications, Browser & Execution

- [ ] C1 – AutoRun/AutoPlay disabled for removable media
- [ ] C2 – Microsoft Defender SmartScreen enabled for apps and browsers
- [ ] C3 – Microsoft Defender Antivirus real‑time protection enabled and up to date
- [ ] C4 – Basic exploit protection enabled (system defaults applied)
- [ ] C5 – Unneeded startup apps reviewed and disabled

---

## D. Logging & Auditing

- [ ] D1 – Advanced audit policy enabled for logon events
- [ ] D2 – Advanced audit policy enabled for process creation (4688 with command line)
- [ ] D3 – Security log size increased (e.g., ≥ 256 MB)
- [ ] D4 – System and Application log sizes increased
- [ ] D5 – Time sync confirmed (correct time and NTP source)

---

## E. Services & Features

- [ ] E1 – Remote Assistance and similar remote‑help features disabled if not needed
- [ ] E2 – Legacy protocols/features (e.g., SMBv1) disabled if not required
- [ ] E3 – Unneeded optional Windows features removed
- [ ] E4 – Any third‑party remote‑access tools reviewed/removed if not required

---

## F. Validation

- [ ] F1 – User can still browse web, use Office/productivity apps, and access needed resources
- [ ] F2 – Event Viewer shows expected logon and process‑creation events
- [ ] F3 – All changes recorded in `changes.md`
