# Tiny Microsoft 365 Security Assessment (Mock Client)

Tiny Microsoft 365 security assessment for the mock client **Magnolia Ridge Cybersecurity, LLC**, showing how I review and harden a small tenant using practical, small‑business‑friendly best practices.

---

## Objective

Perform a lightweight security assessment of a small Microsoft 365 Business tenant for **Magnolia Ridge Cybersecurity, LLC**.  
The goal is to identify high‑impact misconfigurations and recommend practical fixes across identity, email, data protection, and admin access.

---

## Scenario

Magnolia Ridge Cybersecurity, LLC is a small security consulting shop that relies on Microsoft 365 for email and collaboration.  
They have never completed a formal internal security review of their own tenant and are concerned about phishing, account compromise, and accidental data exposure.

- Tenant size (lab model): 1–10 users, representing a small client environment.  
- Licensing: Microsoft 365 Business (lab configuration based on Business‑class licenses).  
- Assumed starting point: defaults mostly unchanged, MFA not consistently enforced, and legacy/basic authentication not fully disabled.

---

## Scope

This assessment focuses on Microsoft 365 configuration only:

- Identity and MFA  
- Legacy/basic authentication  
- Email and phishing protection (Exchange Online / Defender)  
- Data protection (basic DLP and sharing)  
- Logging and audit  
- Admin roles and privileged access  

Endpoints, on‑prem network equipment, and non‑Microsoft SaaS applications are out of scope.

---

## Methodology

- Review the Magnolia Ridge tenant against a lightweight small‑business Microsoft 365 security checklist.  
- Capture the current state of key controls (MFA, legacy auth, anti‑phishing, spam filtering, sharing, logging, admin roles).  
- Describe risks for each area in plain language that a small business owner or leadership team can understand.  
- Produce a short written report with prioritized recommendations, separating quick wins from next‑phase improvements.

---

## Tools and Portals Used

- Microsoft 365 admin center  
- Entra ID (Azure AD) portal  
- Exchange admin center  
- Microsoft Defender portal (where applicable)  
- Built‑in security and compliance features available in Business‑class licenses

---

## Artifacts

- `checklist.md` – Lightweight Microsoft 365 security checklist used during the assessment.  
- `sample-report.md` – Mock client report summarizing findings and prioritized recommendations.  
- `lab-01-mfa-and-forwarding-baseline.md` – Lab write‑up covering MFA and email forwarding baseline, with step‑by‑step configuration and screenshots.  
- `lab-02-email-threat-policies.md` – Lab write‑up covering email threat policies (anti‑phishing, anti‑spam, and related controls), with notes and screenshots.

Screenshots used in the labs are stored under the `images/` directory.

---

## What This Demonstrates

- Reviewing a Microsoft 365 tenant using modern, small‑business‑appropriate security best practices.  
- Identifying high‑impact configuration risks and platform limitations with limited time and scope.  
- Communicating findings and next steps in a way that small, non‑technical organizations (like Magnolia Ridge’s clients) can understand.  
- Documenting work clearly through checklists, lab notes, and client‑style reporting suitable for an entry‑level cloud/security role.
