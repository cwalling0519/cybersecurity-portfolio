# Tiny M365 Lab 01 – MFA and External Forwarding Baseline

Tenant: Magnolia Ridge Cybersecurity (Microsoft 365 E5 trial)  
Admin account: Global administrator with MFA enforced during signup  

## 1. Lab Goal

Establish a minimal but realistic security baseline in a new Microsoft 365 tenant:

- Ensure administrator accounts are protected with MFA and legacy auth is blocked via Security defaults.
- Prevent users from automatically forwarding mail to external recipients using an Exchange Online mail flow rule.

## 2. Environment Setup

- Created a new Microsoft 365 E5 trial tenant for **Magnolia Ridge Cybersecurity**.
- During signup, Microsoft required MFA registration for the first admin account.
- Verified that the admin can sign in to:
  - Microsoft 365 admin center (https://admin.microsoft.com).
  - Entra admin center (https://entra.microsoft.com).
  - Exchange admin center.

Screenshots captured:
- `lab01-admin-center-home.png` – Microsoft 365 admin center home page for the tenant.

## 3. Verify Security Defaults (MFA / Legacy Auth Baseline)

Steps:

1. Opened **Entra admin center** as the tenant admin.
2. Navigated to:  
   Microsoft Entra ID → **Properties** → **Manage security defaults**.
3. Confirmed the banner: **“Your organization is protected by security defaults”** and that security defaults are enabled.

Result:

- Security defaults enforce MFA for admins and block most legacy authentication protocols for the tenant.

Screenshots captured:

- `lab01-entra-overview.png` – Entra ID Overview showing the Magnolia Ridge Cybersecurity tenant and primary domain.
- `lab01-security-defaults.png` – Security defaults panel showing that the organization is protected by security defaults.

## 4. Block Automatic External Email Forwarding

Objective: Stop users from automatically forwarding company mail to external addresses.

Steps:

1. Opened **Exchange admin center** from the Microsoft 365 admin center (Admin centers → Exchange).
2. In Exchange admin center, went to **Mail flow → Rules**.
3. Created a new rule named **“Block external auto-forwarding”**:
   - Condition 1: Recipient is **outside the organization**.
   - Condition 2: Message matches automatic forwarding / forwarding-related criteria (configured using available message property or header options in this tenant).
   - Action: **Block the message** by rejecting it with an explanation:  
     `Automatic external forwarding is disabled for security.`
   - Mode: **Enforce**.
4. Saved the rule and confirmed it appears enabled in the Mail flow rules list.

Screenshots captured:

- `lab01-mailflow-rules-before.png` – Mail flow → Rules view before creating the rule.
- `lab01-mailflow-rule-edit.png` – Rule edit screen showing the two conditions and the reject-with-explanation action.
- `lab01-mailflow-rules-after.png` – Rules list with `Block external auto-forwarding` enabled.

## 5. Takeaways / Client Style Notes

For a small client like **Magnolia Ridge Cybersecurity**, this tiny lab demonstrates:

- Administrator accounts are protected using MFA and legacy protocols are not allowed by default (via Security defaults).
- Data exfiltration risk from automatic mailbox forwarding to personal email is reduced by a tenant-wide mail flow rule.
- The exact configuration is documented with screenshots so the baseline can be reviewed, repeated, or extended in future assessments.
