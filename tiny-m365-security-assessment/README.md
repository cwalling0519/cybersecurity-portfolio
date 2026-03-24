Tiny Microsoft 365 Security Assessment (Mock Client)
Tiny Microsoft 365 security assessment for Magnolia Ridge Cybersecurity, LLC, demonstrating how I review and harden a small client tenant using practical, small‑business‑friendly best practices.

Objective
Perform a lightweight security assessment of a small Microsoft 365 Business tenant for a mock client, Magnolia Ridge Cybersecurity, LLC.
The goal is to identify high‑impact misconfigurations and recommend practical fixes around identity, email, data protection, and admin access.

Scenario
Magnolia Ridge Cybersecurity, LLC is a small security consulting shop using Microsoft 365 for email and collaboration.
They have never had a formal internal security review of their own tenant and are concerned about phishing, account compromise, and accidental data exposure.
Tenant size (lab model): 1–10 users.
Licensing: Microsoft 365 Business (lab configuration based on Business‑class licenses).
Existing state (assumed): Defaults mostly unchanged, MFA not consistently enforced, legacy protocols and basic authentication not fully disabled.

Scope
This assessment focuses on Microsoft 365 configuration only:

Identity & MFA

Legacy / basic authentication

Email & phishing protection (Exchange Online / Defender)

Data protection (basic DLP and sharing)

Logging & audit

Admin roles and privileged access

Endpoints, on‑prem network gear, and non‑Microsoft SaaS apps are out of scope.

Methodology
Review the Magnolia Ridge tenant configuration against a lightweight small‑business M365 security checklist.

Capture the current state of key controls (MFA, legacy auth, anti‑phishing, spam filtering, sharing, logging, admin roles).

Assess risks for each area in plain language that would make sense to a small business owner or leadership team.

Produce a short written report with prioritized recommendations (quick wins vs. next‑phase improvements).

Artifacts
checklist.md – Lightweight Microsoft 365 security checklist used during the assessment.

sample-report.pdf – Mock client report summarizing findings and prioritized recommendations.

tiny-m365-labs/ – Small lab write‑ups (for example, Lab 01 and Lab 02) showing step‑by‑step configuration attempts with screenshots.

What This Demonstrates
Reviewing a Microsoft 365 tenant using modern, small‑business‑appropriate security best practices.

Identifying high‑impact configuration risks and platform limitations with limited time and scope.

Communicating findings and next steps in a way that small, non‑technical organizations like Magnolia Ridge’s clients can understand.
