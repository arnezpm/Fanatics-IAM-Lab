# Fanatics IAM Lab

Enterprise-style **Identity & Access Management / Identity Security home lab** focused on building practical experience across Active Directory, Microsoft Entra ID, hybrid identity, identity governance, authentication, privileged access, SSO, automation, and security control assurance.

> **Portfolio disclaimer:** This is a fictional cybersecurity/IAM learning environment created for portfolio demonstration. It is not affiliated with, endorsed by, or representative of Fanatics or any employer. All organizational structures, named stakeholders, business processes, requests, approvals, incidents, and scenarios are fictional or simulated. Technical evidence is generated within a personal home lab. No employer systems, credentials, confidential information, or production data are used.

## Portfolio Objective

This repository is designed to demonstrate IAM work as it occurs in an enterprise environment rather than as a collection of disconnected technical exercises.

Technical implementations are tied to realistic:

- business requirements;
- identity roles and entitlements;
- least-privilege decisions;
- approval and governance processes;
- troubleshooting scenarios;
- positive and negative authorization tests;
- security findings and remediation;
- lifecycle reviews;
- control testing;
- operational runbooks;
- audit/evidence requirements.

The portfolio role is **IAM Analyst within Cybersecurity**. Lab administrator capability is intentionally distinguished from the authority an IAM Analyst would realistically have in production.

## Learning and Validation Methodology

Major IAM capabilities are developed using the following lifecycle:

```text
Learn
  ↓
Implement
  ↓
Repeat
  ↓
Pressure Test
  ↓
Break / Introduce Failure
  ↓
Assess Security & Business Impact
  ↓
Troubleshoot
  ↓
Mitigate / Remediate
  ↓
Prove
  ↓
Harden
  ↓
Map to Security Standards
  ↓
Document
  ↓
Lessons Learned / Post-Implementation Review
```

A capability is not treated as fully covered simply because it was configured successfully.

The goal is to be able to:

- explain why the control exists;
- configure it;
- identify its trust and authorization boundaries;
- test intended and unintended behavior;
- pressure-test assumptions;
- troubleshoot failures using evidence;
- explain the security impact of a failure;
- distinguish mitigation from root-cause remediation;
- prove remediation worked;
- identify preventive hardening opportunities;
- relate the issue to realistic business risk;
- map the concept to applicable security frameworks and certification domains.

## Security and Standards Alignment

Where relevant, cases are analyzed against concepts from:

- **NIST Cybersecurity Framework 2.0**
- **NIST SP 800-53**
- **ISO/IEC 27001 / 27002**
- **Zero Trust**
- **Microsoft SC-300**
- **CompTIA Security+**
- **Microsoft identity security guidance**
- **Okta identity concepts**, as the environment expands

Mappings are included only where they materially apply to the scenario rather than being added as decorative compliance references.

## Technology Roadmap

Current and planned technologies include:

- Active Directory Domain Services
- Microsoft Entra ID
- Hybrid identity and directory synchronization
- MFA and authentication methods
- Self-Service Password Reset
- Conditional Access
- Identity Protection
- Privileged Identity Management
- Access Reviews
- Enterprise Applications
- SAML
- OpenID Connect / OAuth
- SCIM provisioning
- Microsoft Graph
- PowerShell automation
- Service accounts and workload identities
- PKI and certificate lifecycle
- DNS and identity-related network dependencies
- ITSM / ServiceNow-style workflows
- Okta

## Repository Structure

```text
01-Organization/
02-IAM-Governance/
03-Case-Studies/
04-Technical-Implementation/
05-Security/
06-Evidence/
07-Architecture/
08-Operations-and-Runbooks/
09-Integrations/
10-Identity-Data-and-Analytics/
11-Control-Assurance-and-Risk/
```

### Governance

`02-IAM-Governance` contains reusable IAM governance artifacts such as:

- role definitions;
- entitlement definitions;
- role-to-entitlement matrices;
- naming standards;
- access standards;
- approval and decision records;
- segregation-of-duties concepts.

### Case Studies

`03-Case-Studies` contains end-to-end IAM scenarios following the general chain:

```text
Business Trigger
      ↓
Discovery
      ↓
Requirements
      ↓
Role / Entitlement Definition
      ↓
Least-Privilege Analysis
      ↓
Approval
      ↓
Technical Design
      ↓
Implementation
      ↓
Pressure Testing
      ↓
Authorization Testing
      ↓
Finding / Remediation
      ↓
Evidence
      ↓
Closure
      ↓
Lifecycle Review
```

### Evidence and Control Assurance

Technical evidence is distinguished from simulated business artifacts.

When practical, system behavior is generated and tested directly in the lab rather than represented synthetically.

Simulated artifacts may include:

- ITSM tickets;
- business approvals;
- discovery meetings;
- change records;
- incident narratives;
- stakeholder communications.

Technical validation may include:

- authorization results;
- effective permissions;
- ACL inspection;
- sign-in logs;
- PowerShell/Graph output;
- configuration state;
- troubleshooting evidence.

## Case Study 001 — IT Support Analyst Access Standardization

**Case:** `IAM-2026-0047`

The first completed case establishes delegated password-reset access for an IT Support Analyst role using Active Directory RBAC and least privilege.

The initial implementation successfully provided standard-user password resets, but pressure testing identified that the original OU structure caused the delegation to inherit into a privileged identity population.

The case then follows:

```text
Business requirement
    ↓
RBAC design
    ↓
Delegated password reset
    ↓
Positive test
    ↓
Negative authorization test
    ↓
Privileged-scope pressure test
    ↓
Control finding
    ↓
Root-cause analysis
    ↓
Privileged OU separation
    ↓
Retest
    ↓
Hardening
    ↓
Control/framework mapping
```

Final testing demonstrated that the delegated operator could:

- **reset a standard user's password** — allowed;
- **modify that user's group membership** — denied;
- **reset a privileged user's password** — denied.

The case also documents a test-method assurance issue where preliminary `/netonly` testing was rejected because the execution context was not sufficiently reliable to serve as final authorization evidence.

See:

`03-Case-Studies/001-IT-Support-Role/`

## Planned Case Studies

Future scenarios are expected to include:

- Joiner provisioning
- Mover / role-change access
- Leaver remediation
- Access certification
- MFA and SSPR support
- Entra sign-in investigation
- Conditional Access troubleshooting
- Hybrid identity synchronization incidents
- SAML/OIDC SSO troubleshooting
- Risky sign-in response
- PIM and privileged-access workflows
- SaaS application onboarding
- PKI / certificate lifecycle incidents
- Microsoft Graph and PowerShell automation
- Okta identity administration and cross-platform comparison

## Portfolio Philosophy

The objective is not to demonstrate that every implementation was perfect on the first attempt.

Findings, failed assumptions, misconfigurations, excessive access, troubleshooting paths, and design corrections are intentionally preserved when they improve the learning value of a case.

A strong case should be able to answer:

**What was needed?**  
**Why was the control necessary?**  
**What could go wrong?**  
**How was it tested?**  
**What failed?**  
**Why was that failure a security issue?**  
**How was risk mitigated?**  
**What fixed the root cause?**  
**How was the fix proven?**  
**What was hardened afterward?**  
**Which security principles or standards apply?**  
**What would be done differently next time?**

That process is the core of this portfolio.
