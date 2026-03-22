# Microsoft 365 Security Baseline Assessment  
**Client:** Contoso Bakery LLC (Mock)  
**Tenant Size:** ~10 users  
**Date:**  
**Assessor:**  

---

## 1. Executive Summary

Contoso Bakery LLC uses Microsoft 365 Business Standard for email and collaboration.  
This lightweight assessment reviews key security controls for identity, email, data protection, logging, and admin access.

Overall, the tenant is currently rated **Fair**. There are several quick configuration changes that can significantly reduce the risk of account compromise and data leakage.

**Top 3 Risks**

1. MFA is not enforced for all users.  
2. Legacy authentication (older protocols) is still allowed.  
3. Global Admin accounts are more numerous and less isolated than necessary.

**Top 3 Recommended Actions**

1. Enforce MFA for all accounts and require strong methods for admins.  
2. Block legacy authentication protocols and document any true exceptions.  
3. Reduce the number of Global Admins and use dedicated admin accounts.

---

## 2. Scope and Methodology

**In Scope**

- Identity & MFA  
- Legacy / basic authentication  
- Email & phishing protection  
- Data protection and sharing  
- Logging & alerts  
- Admin roles and privileged access  

**Method**

- Reviewed settings in Microsoft 365 Admin Center, Entra ID, and Defender portals.  
- Compared configuration against a small‑business‑focused M365 security checklist.  
- Documented current state, risks, and recommended changes.

---

## 3. Findings and Recommendations

### 3.1 Identity & MFA

**Current State (Mock)**  
- MFA is optional; only some users have enabled it.  
- Admins use MFA but rely on weaker methods.

**Risks**  
- Password‑only or weakly protected accounts are vulnerable to phishing and credential stuffing.

**Recommendations**  
- Enforce MFA for all users.  
- Require app‑based MFA (or stronger) for admin accounts.

---

### 3.2 Legacy Authentication

**Current State (Mock)**  
- Legacy protocols (POP/IMAP/SMTP AUTH) are allowed for all users.

**Risks**  
- Attackers can bypass modern auth protections and target weaker legacy endpoints.

**Recommendations**  
- Disable legacy authentication globally.  
- Document any accounts that truly require it and apply compensating controls.

---

### 3.3 Email & Phishing Protection

**Current State (Mock)**  
- Anti‑phishing/anti‑spam policies are mostly at default settings.  
- Automatic forwarding to external domains is allowed.

**Recommendations**  
- Enable and tune anti‑phishing policies for all users.  
- Restrict automatic forwarding to external domains.

---

### 3.4 Data Protection & Sharing

**Current State (Mock)**  
- No basic DLP policy is configured.  
- External sharing is more permissive than required.

**Recommendations**  
- Implement a simple DLP policy for obvious sensitive data types.  
- Tighten SharePoint/OneDrive external sharing defaults.

---

### 3.5 Logging & Admin Roles

**Current State (Mock)**  
- Unified audit logging is enabled.  
- Three Global Admins exist and are used for daily email.

**Recommendations**  
- Designate 1–2 dedicated Global Admin accounts for administration only.  
- Create a documented emergency access account if appropriate.

---

## 4. Prioritized Action Plan

**Immediate (0–2 weeks)**  
- Enforce MFA for all users.  
- Disable legacy authentication.  
- Reduce and isolate Global Admin accounts.

**Next (1–3 months)**  
- Tune anti‑phishing and anti‑spam policies.  
- Implement a basic DLP policy and adjust external sharing defaults.

**Future (3–6 months)**  
- Expand Conditional Access policies and monitoring as licensing allows.
