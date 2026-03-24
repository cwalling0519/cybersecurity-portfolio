# Tiny Microsoft 365 Security Assessment (Mock Client)

Tiny Microsoft 365 security assessment for Magnolia Ridge Cybersecurity, LLC, showing how I review and harden a small client tenant using practical, small‑business‑friendly best practices.

## Objective

Perform a lightweight security assessment of a small Microsoft 365 Business tenant for the mock client **Magnolia Ridge Cybersecurity, LLC**.  
The goal is to find high‑impact misconfigurations and recommend practical fixes across identity, email, data protection, and admin access.

## Scenario

Magnolia Ridge Cybersecurity, LLC is a small security consulting shop that relies on Microsoft 365 for email and collaboration.  
They have never completed a formal internal security review of their own tenant and are concerned about phishing, account compromise, and accidental data exposure.  
Tenant size (lab model): 1–10 users, representing a small client environment.  
Licensing: Microsoft 365 Business (lab configuration based on Business‑class licenses).  
Assumed starting point: defaults mostly unchanged, MFA not consistently enforced, and legacy / basic authentication not fully disabled.

## Scope

This assessment focuses on Microsoft 365 configuration only:

- Identity and MFA  
- Legacy / basic authentication  
- Email and phishing protection (Exchange Online / Defender)  
- Data protection (basic DLP and sharing)  
- Logging and audit  
- Admin roles and privileged access  

Endpoints, on‑prem network equipment, and non‑Microsoft SaaS applications are out of scope.

## Methodology

- Review the Magnolia Ridge tenant against a lightweight small‑business Microsoft 365 security checklist.  
- Capture the current state of key controls (MFA, legacy auth, anti‑phishing, spam filtering, sharing, logging, admin roles).  
- Describe risks for each area in plain language that a small business owner or leadership team can understand.  
- Produce a short written report with prioritized recommendations, separating quick wins from next‑phase improvements.

## Artifacts

- `checklist.md` – Lightweight Microsoft 365 security checklist used during the assessment.  
- `sample-report.pdf` – Mock client report summarizing findings and prioritized recommendations.  
- `tiny-m365-labs/` – Small lab write‑ups (for example, Lab 01 and Lab 02) with step‑by‑step configuration attempts and screenshots.

## What This Demonstrates

- Reviewing a Microsoft 365 tenant using modern, small‑business‑appropriate security best practices.  
- Identifying high‑impact configuration risks and platform limitations with limited time and scope.  
- Communicating findings and next steps in a way that small, non‑technical organizations like Magnolia Ridge’s clients can understand.
