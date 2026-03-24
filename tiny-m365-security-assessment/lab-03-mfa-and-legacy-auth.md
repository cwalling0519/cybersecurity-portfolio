# Tiny M365 Lab 03 – MFA & Legacy Authentication

## Goal

Verify that multi-factor authentication is enforced for the Magnolia Ridge Cybersecurity, LLC tenant
and confirm that legacy/basic authentication is blocked wherever possible.

---

## Environment

- Tenant: `magnoliaridgecybersecurity.onmicrosoft.com`
- Portal: Microsoft 365 admin center (`https://admin.microsoft.com`) and Microsoft Entra admin center (`https://entra.microsoft.com`)
- Account: Global admin with Security admin rights

---

## Step 1 – Review Modern Authentication settings

1. Signed in to `https://admin.microsoft.com` and navigated to **Settings → Org settings → Services → Modern authentication**.
2. The page showed that **Security Defaults are enabled** for the tenant, meaning:
   - Modern authentication to Exchange Online is required for all clients.
   - Basic authentication connections are blocked across all legacy protocols (POP, IMAP, SMTP AUTH, older Outlook clients).
   - Individual protocol toggles are greyed out because Security Defaults enforces these settings at the Azure level tenant-wide.
3. This is the strongest recommended configuration for a small business tenant — no further changes were needed here.
   - Screenshot: `Modern_Auth.png`

---

## Step 2 – Review MFA settings in the admin center

1. Still in **Settings → Org settings → Services**, clicked **Multi-factor authentication**.
2. The page described MFA capabilities but showed no editable controls, confirming that MFA enforcement is handled through Security Defaults and the Entra admin center rather than this page.
3. Clicked **Configure multi-factor authentication** to open the per-user MFA portal in Microsoft Entra.
   - Screenshot: `MFA_Info.png`

---

## Step 3 – Check per-user MFA status

1. In the Microsoft Entra admin center, opened the **Per-user multifactor authentication** page.
2. Confirmed that the admin account **Corey Walling** (`admin@MagnoliaRidgeCybersecurity.onmicrosoft.com`) showed MFA status as **disabled** at the per-user level.
   - Note: This is expected in a Security Defaults tenant — Security Defaults enforces MFA at sign-in separately from per-user MFA settings.
   - Screenshot: `PerUser_MFA.png`

---

## Step 4 – Enforce MFA for the admin account

1. Checked the box next to **Corey Walling** on the per-user MFA page.
2. Clicked **Enable MFA** and confirmed the prompt.
3. Immediately after enabling, clicked **Enforce MFA** to move the account to enforced status.
4. Confirmed the admin account status changed from **disabled** to **enforced**.
   - Screenshot: `PerUser_Enforced.png`

---

## Step 5 – Confirm 2FA enrollment prompt

1. Opened a private/incognito browser window and signed in to `https://portal.office.com` as the Magnolia Ridge admin.
2. Confirmed that the sign-in process now requires MFA completion before granting access, validating that the enforced setting took effect.
   - Screenshot: `2FA.png`

---

## Findings and observations

- Security Defaults were already enabled in the Magnolia Ridge tenant, blocking basic/legacy authentication
  across all protocols tenant-wide. This is the recommended baseline configuration for small businesses
  that do not have Microsoft Entra ID P1/P2 licensing for Conditional Access.
- Per-user MFA was initially set to **disabled** for the admin account, which is a gap even when Security
  Defaults are on — Security Defaults enforces MFA at sign-in but marking accounts as **enforced** at the
  per-user level adds an additional explicit layer.
- After enforcing per-user MFA on the admin account, the next sign-in prompted for MFA enrollment,
  confirming the change took effect immediately.
- For a real Magnolia Ridge client engagement, the recommendation would be:
  - Keep Security Defaults enabled (or move to Conditional Access if licensing allows).
  - Enforce per-user MFA for all admin accounts at minimum.
  - Enforce per-user MFA for all standard users in addition to Security Defaults.
  - Verify no accounts are excluded from MFA requirements.

---

## Screenshots captured

- `Modern_Auth.png` – Modern authentication page showing Security Defaults are enabled and basic auth is blocked.
- `MFA_Info.png` – Multi-factor authentication Services page with link to configure per-user MFA.
- `PerUser_MFA.png` – Per-user MFA portal showing admin account status as disabled before changes.
- `PerUser_Enforced.png` – Per-user MFA portal showing admin account status as enforced after changes.
- `2FA.png` – Sign-in prompt confirming MFA is now required for the admin account.
