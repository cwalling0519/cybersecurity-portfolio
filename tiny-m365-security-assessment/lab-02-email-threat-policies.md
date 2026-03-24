Tiny M365 Lab 02 – Email Threat Policies
Goal
Strengthen Microsoft 365 email protections by configuring anti‑phishing and anti‑spam policies in the Microsoft Defender portal, and document any technical limitations encountered.

Environment
Tenant: magnoliaridgecybersecurity.onmicrosoft.com

Portal: Microsoft Defender portal at https://security.microsoft.com
​

Admin account: Global admin with Security admin rights

Attempted anti-phishing policy configuration
Signed in to https://security.microsoft.com and opened Email & collaboration → Policies & rules → Threat policies → Anti-phishing.
​

Took a screenshot of the Anti‑phishing policies list showing built‑in/default policies and my admin context.

Clicked Create policy → Anti-phishing to create a new policy named “Magnolia Ridge – Default Anti-Phishing”.

Scope: Added the tenant domain magnoliaridgecybersecurity.onmicrosoft.com under Include these users, groups, and domains → Domains so the policy would apply to all mailboxes in this lab.

Took a screenshot of the Users, groups, and domains page showing the included domain.

On Phishing threshold & protection:

Set Phishing email threshold to level 2 – Aggressive to increase sensitivity over the default.

Left Spoof intelligence turned On.

Enabled User impersonation protection and added my admin account as a protected user.

Left Domain impersonation off for this tiny lab.

Took a screenshot of this page with the slider, spoof intelligence, and user impersonation settings.

On the Actions page, I attempted to harden message handling:

Set If a message is detected as user impersonation → Quarantine the message.

Left Honor DMARC record policy when the message is detected as spoof enabled.

Ensured If the message is detected as spoof and DMARC policy is p=quarantine → Quarantine the message, and p=reject → Reject the message.
​

Changed If the message is detected as spoof by spoof intelligence → Quarantine the message instead of moving to Junk.

Enabled safety tips such as first contact and user impersonation safety tips where available.

Took a screenshot of the Actions page showing these intended settings.

When attempting to save/finish the new policy, the portal repeatedly returned:

“Client Error – An error occurred when creating the policy. Please review your settings and try again.”

Diagnostic info included Version:1.0.2774.1, Environment:SCUPROD, and backend identifiers.

I confirmed settings were valid and retried several times with minimal changes but received the same error, which aligns with reported issues in some newer tenants where Defender threat policies cannot be created due to backend faults.

Took a screenshot of the error dialog for documentation.

Organizational setup attempt
The portal prompted “Complete organizational setup” while working with threat policies. I chose Yes to try to unblock policy creation.

This opened the organizational / Defender setup wizard intended to complete initial configuration for the tenant.

Took a screenshot of the first page of this setup wizard.

During that setup process, the portal displayed another backend error:

“Client Error – Exception of type 'Microsoft.Exchange.Management.PSDirectInvoke.DirectInvokeCmdletExecutionException' was thrown.”

This indicated the setup could not complete successfully for this tenant at this time.

Took a screenshot of this Client Error from the organizational setup.

After closing the error and refreshing the Defender portal, I confirmed that Anti‑phishing policies still could not be created or edited without hitting the same Client Error message.

Attempted anti-spam policy configuration
Navigated to Email & collaboration → Policies & rules → Threat policies → Anti-spam.
​

Observed three default policies:

Anti-spam inbound policy (Default)

Connection filter policy (Default)

Anti-spam outbound policy (Default)

All showed Status: Always on and Priority: Lowest.

Took a screenshot of this Anti-spam policies overview page.

Opened Anti-spam inbound policy (Default) to adjust spam handling:

Intended changes in the Spam and bulk actions section:

Set High confidence spam → Quarantine the message.

Set any Phishing category (if present) → Quarantine the message.

Leave normal Spam as move to Junk. These follow Microsoft’s recommended stronger baseline for inbound spam and phishing.

Took a screenshot of the settings page showing the intended dropdown changes.

When attempting to save the inbound anti-spam policy, the portal again returned:

“Client Error – An error occurred when updating the policy. Please try it later.”

This matched the same pattern as the anti-phishing policy failures, indicating a broader Defender policy backend issue rather than a configuration mistake.

Took a screenshot of the anti-spam policy editor with the error visible.

Returned to the Anti-spam policies list to confirm:

All default policies remained in their original state (no changes applied).

Took a final screenshot of the list with policies still Always on but unmodified.

Findings and observations
The lab objective was to raise protection by:

Enabling a stricter anti‑phishing policy (threshold 2, spoof intelligence on, user impersonation protection, and quarantine actions).

Tightening inbound anti‑spam handling so high‑confidence spam and phishing are quarantined.

In practice, the Microsoft Defender portal in this tenant would not allow any creation or modification of anti‑phishing or anti‑spam policies. Multiple attempts (including running organizational setup) resulted in consistent Client Error messages tied to backend cmdlet execution in Exchange Online / Defender.

This behavior matches documented issues where new or partially configured tenants experience failures when Defender tries to call underlying Exchange Online cmdlets to create or update threat policies.

Even though final policy changes could not be applied, the lab still demonstrated:

How to navigate to and attempt configuration of Anti‑phishing and Anti‑spam policies in the Microsoft Defender portal.

How to select target domains / users, adjust phishing thresholds, enable spoof and impersonation protection, and choose quarantine vs. junk actions.

How to document platform limitations and errors as part of a security assessment, rather than silently ignoring them.
