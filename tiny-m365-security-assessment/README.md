# Tiny Microsoft 365 Security Assessment (Mock Client)

## Objective

Perform a lightweight security assessment of a 10‑user Microsoft 365 Business tenant for a mock small business (Contoso Bakery LLC).  
The goal is to identify high‑impact misconfigurations and recommend practical fixes around identity, email, data protection, and admin access.

## Scenario

Contoso Bakery LLC is a small local business using Microsoft 365 for email and collaboration.  
They have never had a formal security review and are worried about phishing, account compromise, and data leaks.

- Tenant size: ~10 users  
- Licensing: Microsoft 365 Business Standard  
- Existing state (assumed): Defaults mostly unchanged, MFA not enforced for all users, legacy protocols still allowed  

## Scope

This assessment focuses on Microsoft 365 configuration only:

- Identity & MFA  
- Legacy / basic authentication  
- Email & phishing protection (Exchange Online / Defender)  
- Data protection (basic DLP and sharing)  
- Logging & audit  
- Admin roles and privileged access  

Endpoints, on‑prem network gear, and non‑Microsoft SaaS apps are out of scope.

## Methodology

1. Review tenant configuration against a lightweight small‑business M365 security checklist.  
2. Capture the current state of key controls (MFA, legacy auth, anti‑phishing, sharing, logging, admin roles).  
3. Assess risks for each area in plain language relevant to a small business.  
4. Produce a short written report with prioritized recommendations (quick wins vs. next‑phase work).

## Artifacts

- `checklist.md` – Lightweight Microsoft 365 security checklist used during the assessment.  
- `sample-report.pdf` – Mock client report summarizing findings and prioritized recommendations.  

## What This Demonstrates

- Reviewing a Microsoft 365 tenant using modern small‑business security best practices.  
- Identifying high‑impact configuration risks with limited time and scope.  
- Communicating findings and next steps in a way small, non‑technical businesses can understand.
