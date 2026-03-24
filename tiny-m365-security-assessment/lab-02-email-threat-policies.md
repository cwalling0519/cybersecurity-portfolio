Tiny M365 Lab 02 – Email Threat Policies
Goal
Strengthen Microsoft 365 email protections by configuring anti‑phishing and anti‑spam policies in the Microsoft Defender portal, and document any technical limitations encountered.

Environment
Tenant: magnoliaridgecybersecurity.onmicrosoft.com

Portal: Microsoft Defender portal at https://security.microsoft.com

Account: Global admin with Security admin rights

Anti-phishing policy – attempted configuration
Signed in to https://security.microsoft.com and confirmed access to the Microsoft Defender home dashboard.

Screenshot: lab02-defender-portal-home.png

Navigated to Email & collaboration → Policies & rules → Threat policies → Anti-phishing and reviewed the existing Office365 AntiPhish Default (Default) policy.

Screenshot: lab02-anti-phishing-policy-list.png

Opened the default anti‑phishing policy and went to the Phishing threshold & protection page to increase protection:

Set Phishing email threshold to 2 – Aggressive.

Left Spoof intelligence On.

Enabled User impersonation protection and added the admin account as a protected user.

Left Domain impersonation protection off for this small lab tenant.

Screenshot: lab02-anti-phishing-threshold-impersonation.png

Attempted to save the updated anti‑phishing policy. The portal repeatedly returned a Client Error indicating the operation could not be completed, even when retrying with minimal changes. This suggests a backend issue in the tenant’s Defender/Exchange policy infrastructure rather than a configuration mistake.

Screenshot: lab02-anti-phishing-client-error.png

Anti-spam policies – attempted configuration
Navigated to Email & collaboration → Policies & rules → Threat policies → Anti-spam and reviewed the default policies:

Anti-spam inbound policy (Default)

Connection filter policy (Default)

Anti-spam outbound policy (Default)
All showed Status: Always on and Priority: Lowest.

Screenshot: lab02-anti-spam-policies-overview.png

Opened Anti-spam inbound policy (Default) and attempted to harden inbound spam handling in the Actions (or Spam/Bulk actions) section by configuring:

High confidence spam → Quarantine message.

Phishing → Quarantine message.

Regular Spam left as Move message to Junk Email folder.
These changes were intended to ensure high‑risk messages are quarantined instead of delivered to user mailboxes.

Screenshot: lab02-anti-spam-inbound-settings.png

When saving the updated inbound spam policy, the portal again displayed a Client Error stating that the operation could not be completed and to try again later. As with the anti‑phishing policy, the error prevented any changes from being applied.

Screenshot: lab02-anti-spam-client-error.png

Findings and observations
Intended changes for this lab were to:

Increase anti‑phishing sensitivity (threshold 2), keep spoof intelligence enabled, and protect the admin account with user impersonation settings.

Quarantine high‑confidence spam and phishing messages instead of sending them to Junk, while leaving normal spam as Junk.

In practice, the tenant’s Defender environment blocked all attempts to create or update email threat policies. Both anti‑phishing and anti‑spam policy changes failed with Client Error messages during save operations, even after confirming valid settings and retrying.

This lab still demonstrates:

How to locate and attempt to configure anti‑phishing and anti‑spam policies in Microsoft Defender.

The specific settings a security analyst would apply to harden a small tenant’s email protections.

How to document platform‑level limitations and errors as part of a security assessment, including capturing evidence screenshots and describing the impact on the organization’s ability to fully enforce best‑practice controls.
