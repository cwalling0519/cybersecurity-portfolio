# Tiny M365 Security Checklist (Mock Tenant)

Tenant: Contoso Bakery LLC  
Date:  
Assessor:  

Status legend: ✅ Pass | ⚠️ Needs Improvement | ⬜ Not Applicable

## A. Identity & MFA

- [ ] A1 – MFA enforced for all user accounts  
- [ ] A2 – Admin accounts use strong MFA methods (e.g., app‑based)  
- [ ] A3 – No shared admin accounts without MFA  

## B. Legacy Authentication

- [ ] B1 – Legacy/basic auth (POP/IMAP/SMTP AUTH, etc.) blocked where possible  
- [ ] B2 – Any required exceptions documented with compensating controls  

## C. Email & Phishing Protection

- [ ] C1 – Anti‑phishing policy enabled and applied to all users  
- [ ] C2 – Anti‑spam policy configured beyond bare defaults  
- [ ] C3 – Safe Links / Safe Attachments enabled, if licensed  
- [ ] C4 – Automatic forwarding to external domains restricted  

## D. Data Protection & Sharing

- [ ] D1 – Basic DLP policy for sensitive data exists or is explicitly out of scope  
- [ ] D2 – SharePoint/OneDrive external sharing defaults tightened for this business  

## E. Logging & Alerts

- [ ] E1 – Unified audit logging enabled  
- [ ] E2 – Security alerts delivered to a monitored mailbox or distribution list  

## F. Admin Roles & Privileged Access

- [ ] F1 – Global Admin count minimized (ideally 1–2)  
- [ ] F2 – Dedicated admin accounts used instead of daily user accounts  

## G. User Hygiene & Awareness

- [ ] G1 – Password and sign‑in policies follow current guidance  
- [ ] G2 – Basic phishing/MFA guidance provided to users  
