# Identity Security / IAM Portfolio

Hands-on Identity Security and IAM portfolio demonstrating **enterprise access administration, authentication, authorization, RBAC, least privilege, troubleshooting, identity governance, and security-control validation**.

**Certification-aligned coverage:** `CompTIA Security+` · `Microsoft SC-300` · `Okta Professional`  
**Portfolio platforms:** `Active Directory` · `Microsoft Entra` · `Hybrid Identity` · `Okta` · `PowerShell` · `Microsoft Graph`

> **Evidence-first portfolio:** Skills listed below link directly to the case-study section where the capability is demonstrated, tested, or troubleshot.

## Skills & Evidence

| Skill / Technology | Demonstrated capability | Evidence |
|---|---|---|
| **Active Directory users, groups & roles** | Managed user identities, security groups, role membership, and nested access groups. | [Case 001 → Identity & Role Administration](03-Case-Studies/001-IT-Support-Role/README.md#evidence-ad-identity-admin) |
| **RBAC** | Translated a business role into a controlled role → entitlement → permission model | [Case 001 → RBAC & Entitlement Design](03-Case-Studies/001-IT-Support-Role/README.md#evidence-rbac) |
| **Password reset / delegated administration** | Implemented scoped password-reset authority without granting broad AD administration | [Case 001 → Delegated Password Reset](03-Case-Studies/001-IT-Support-Role/README.md#evidence-password-reset) |
| **Least privilege** | Defined explicit administrative exclusions and constrained support access to required capabilities | [Case 001 → Least-Privilege Boundary](03-Case-Studies/001-IT-Support-Role/README.md#evidence-least-privilege) |
| **Authorization testing** | Performed positive, negative, and privileged-boundary access tests from a non-admin operator context | [Case 001 → Authorization Testing](03-Case-Studies/001-IT-Support-Role/README.md#evidence-authorization-testing) |
| **ACL inheritance / effective scope** | Identified inherited delegation that unintentionally extended into a privileged identity population | [Case 001 → ACL Inheritance Finding](03-Case-Studies/001-IT-Support-Role/README.md#evidence-acl-inheritance) |
| **Privileged access boundaries** | Separated privileged identities from the standard workforce delegation hierarchy and retested access | [Case 001 → Privileged Identity Remediation](03-Case-Studies/001-IT-Support-Role/README.md#evidence-privileged-boundary) |
| **IAM troubleshooting & evidence assurance** | Rejected an ambiguous authorization test method, rebuilt the test context, and repeated validation correctly | [Case 001 → Troubleshooting & Test Assurance](03-Case-Studies/001-IT-Support-Role/README.md#evidence-troubleshooting) |
| **PowerShell-assisted validation** | Used PowerShell alongside GUI administration to verify Active Directory access-control state | [Case 001 → Technical Validation](03-Case-Studies/001-IT-Support-Role/README.md#evidence-powershell) |

> **Current evidence:** Case 001 provides completed hands-on evidence for the skills above. Microsoft Entra, hybrid identity, authentication, SSO, PIM, PKI, Microsoft Graph, and Okta scenarios are being added through subsequent case studies.

## Case Studies

| Case Study | What it demonstrates | Technology | Core skills |
|---|---|---|---|
| **[001 — IT Support RBAC & Delegated Password Reset](03-Case-Studies/001-IT-Support-Role/README.md)** | Standardized IT Support password-reset access, discovered excessive inherited privileged scope, redesigned the authorization boundary, and validated the remediation | Active Directory, ADUC/RSAT, Windows 11, PowerShell | RBAC, delegated administration, least privilege, ACL inheritance, privileged access, authorization testing |

## Technology Coverage

**Current hands-on evidence:**  
`Active Directory Domain Services` · `ADUC / RSAT` · `Windows 11 Domain Member` · `PowerShell` · `DNS dependencies`

**Portfolio expansion:**  
`Microsoft Entra ID` · `MFA` · `SSPR` · `Conditional Access` · `Identity Protection` · `Hybrid Identity` · `PIM` · `Access Reviews` · `SAML/OIDC` · `SCIM` · `Microsoft Graph` · `PKI` · `Okta`

## Certification & Security Alignment

### Certification-aligned knowledge

`CompTIA Security+` · `Microsoft SC-300` · `Okta Professional`

Case studies connect hands-on technical work to the identity, authentication, authorization, troubleshooting, governance, automation, and security concepts commonly evaluated in these certification domains.

### Security frameworks & principles

`NIST CSF 2.0` · `NIST SP 800-53` · `ISO/IEC 27001/27002` · `Zero Trust`

Framework mappings are used where they materially explain **why a control matters**, what security property is at risk, and how a remediation improves the control environment.

## About This Portfolio

This repository models an evolving fictional enterprise IAM program rather than a collection of isolated configuration exercises.

Each major case begins with a realistic business or security requirement and follows the work through authorization design, implementation, testing, pressure testing, troubleshooting, remediation, evidence, and lifecycle considerations.

The portfolio role is **IAM Analyst within Cybersecurity**. Technical capability demonstrated in the home lab is intentionally distinguished from production authority: business owners approve business need, security and resource owners participate where appropriate, and deeper platform changes may belong to engineering or infrastructure teams.

<details>
<summary><strong>How cases are developed and validated</strong></summary>

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
Map to Security Knowledge & Standards
  ↓
Document
  ↓
Lessons Learned / Post-Implementation Review
```

A capability is not treated as fully covered simply because a feature was configured successfully.

The objective is to understand why the control exists, identify its security boundary, test intended and unintended behavior, diagnose failures using evidence, explain business/security impact, remediate root cause, prove the remediation, and identify preventive improvements.

</details>

<details>
<summary><strong>Repository structure</strong></summary>

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

Reusable artifacts are promoted out of individual cases:

- Roles → Role Catalog
- Entitlements → Entitlement Catalog
- Architecture decisions → ADRs
- Repeated procedures → Runbooks
- Control tests → Control Assurance
- Technical proof → Evidence
- Automation → Technical Implementation

</details>

## Portfolio Roadmap

Planned case-study coverage includes:

| Area | Planned scenarios |
|---|---|
| **Identity lifecycle** | Joiner provisioning, mover access changes, leaver remediation |
| **Authentication** | MFA enrollment/troubleshooting, SSPR, authentication methods |
| **Entra operations** | Sign-in log investigation, Conditional Access troubleshooting, Identity Protection |
| **Hybrid identity** | AD ↔ Entra synchronization and identity troubleshooting |
| **Governance** | Access Reviews, entitlement review, PIM |
| **Application IAM** | Enterprise Applications, SAML/OIDC SSO, application assignment |
| **PKI** | Certificate lifecycle and renewal troubleshooting |
| **Automation** | PowerShell and Microsoft Graph reporting/workflows |
| **Okta** | Authentication, application access, lifecycle, and cross-platform identity comparison |

## Disclaimer

This is a fictional cybersecurity/IAM home-lab portfolio created for learning and professional demonstration.

The lab environment is **not affiliated with, endorsed by, or representative of Fanatics or any employer**. All organizational structures, stakeholders, approvals, incidents, workflows, and business scenarios are fictional or simulated. Technical evidence is generated in a personal lab environment.

No employer systems, production credentials, confidential information, or proprietary data are used.