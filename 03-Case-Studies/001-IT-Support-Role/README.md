# Case Study 001 — IT Support RBAC & Delegated Password Reset

**Case:** `IAM-2026-0047`  
**Status:** Closed — remediated, validated, documented, and hardened

> **Outcome:** Designed a least-privilege password-reset model for IT Support, identified that inherited Active Directory delegation unintentionally extended into a privileged identity population, redesigned the authorization boundary, and proved the remediation through positive and negative authorization testing.

**Technology:** `Active Directory DS` · `ADUC / RSAT` · `Windows 11` · `PowerShell`

**Skills demonstrated:**  
[Active Directory Administration](#evidence-ad-identity-admin) ·
[RBAC](#evidence-rbac) ·
[Password Reset](#evidence-password-reset) ·
[Least Privilege](#evidence-least-privilege) ·
[Authorization Testing](#evidence-authorization-testing) ·
[ACL Inheritance](#evidence-acl-inheritance) ·
[Privileged Access](#evidence-privileged-boundary) ·
[Troubleshooting](#evidence-troubleshooting) ·
[PowerShell](#evidence-powershell)

## Evidence Map

| Skill | What this case proves | Jump to evidence |
|---|---|---|
| **AD users, groups & roles** | Identity objects, role membership, group nesting, and delegated administration | [View ↓](#evidence-ad-identity-admin) |
| **RBAC** | Business responsibility translated into role, entitlement, permission group, and ACL | [View ↓](#evidence-rbac) |
| **Password reset** | Standard-user password reset succeeds without Domain Admin | [View ↓](#evidence-password-reset) |
| **Least privilege** | Unneeded administrative capabilities remain excluded | [View ↓](#evidence-least-privilege) |
| **Authorization testing** | Positive, negative, and privileged-scope tests validate the boundary | [View ↓](#evidence-authorization-testing) |
| **ACL inheritance** | Pressure testing identifies unintended inherited permission scope | [View ↓](#evidence-acl-inheritance) |
| **Privileged access** | Privileged identities are isolated from standard support delegation | [View ↓](#evidence-privileged-boundary) |
| **Troubleshooting** | Ambiguous test evidence is rejected and testing is rebuilt correctly | [View ↓](#evidence-troubleshooting) |
| **PowerShell** | Command-line verification supplements GUI-based IAM administration | [View ↓](#evidence-powershell) |

## My Role & Responsibility Boundary

**Portfolio role:** Paul M. Arnez — IAM Analyst, Cybersecurity — Identity & Access Management

**My responsibility in the scenario:** requirements analysis, translating business responsibilities into entitlements, least-privilege analysis, access-model design, approved IAM administration, authorization testing, troubleshooting, evidence collection, and documentation.

**Not represented as my unilateral authority:** business approval, unrestricted Domain Admin activity, privileged-access approval, or ownership of every infrastructure/architecture change.

Business requirements are owned by the appropriate business stakeholder; senior IAM, security, infrastructure, or engineering stakeholders review or implement deeper changes where appropriate.

## Business Problem

IT Support needed a repeatable method to reset passwords for standard workforce users.

The existing requirement did **not** justify broad Active Directory administration. The IAM design therefore needed to provide the required support capability while preventing unrelated directory administration and privileged-account access.

The approved first entitlement was:

> **Reset passwords for standard Corporate and Technology workforce identities.**

Account unlock, broad directory writes, group administration, Domain Admin, GPO administration, unrestricted server administration, and privileged-account administration were intentionally outside the scope of this case.

---

<a name="evidence-ad-identity-admin"></a>

## Active Directory Identity & Role Administration

The operator used for the case was **Maya Rodriguez**, an IT Support Analyst:

`mrodriguez@iamfanatics.com`

Maya was assigned to:

`GG-IT-Support-Analysts`

The role group participates in a broader functional hierarchy while remaining distinct from other support roles.

The case also uses separate identity populations for:

- standard Corporate workforce users;
- Technology users;
- privileged identities.

This separation becomes important when delegated authorization scope is evaluated later in the case.

**Detailed evidence:**  
[Role & Entitlement Design](03-Role-and-Entitlement-Design/IT-Support-Analyst-Role-Design.md)

---

<a name="evidence-rbac"></a>

## RBAC & Entitlement Design

The business requirement was not assigned directly to Maya's user object.

Instead, the design separated **identity**, **business role**, **technical entitlement**, and **permission**:

```text
Maya Rodriguez
    ↓
GG-IT-Support-Analysts
    ↓
DL-IT-User-Password-Reset
    ↓
Reset Password extended right
    ↓
Approved standard workforce identities
```

This makes the entitlement reusable, reviewable, and removable without assigning an ACL directly to an individual.

The broader IT Support function does not automatically receive every possible support entitlement. For example, `GG-Service-Desk-Analysts` was intentionally **not** given password-reset permission simply because it is another support-oriented role.

**Detailed evidence:**  
[Role Design](03-Role-and-Entitlement-Design/IT-Support-Analyst-Role-Design.md)  
[Role Catalog](../../02-IAM-Governance/Role-Catalog/IT-Support-Analyst.md)  
[Entitlement Catalog](../../02-IAM-Governance/Entitlement-Catalog/AD-Reset-Password.md)  
[Role-to-Entitlement Matrix](../../02-IAM-Governance/Role-Entitlement-Matrix/IT-Support-Analyst.md)

---

<a name="evidence-password-reset"></a>

## Delegated Password Reset

The permission group:

`DL-IT-User-Password-Reset`

received the Active Directory **Reset Password** extended right for descendant user objects within the standard workforce authorization boundary.

The design intentionally avoided broad user-property permissions and did not require Maya to become a Domain Admin.

Final functional validation was performed from the domain-joined support workstation:

`FAN-ITSUP01`

with Maya interactively signed in as:

`FANATICS\mrodriguez`

Maya successfully reset the password of the standard-user test identity, **Daniel Carter** (`dcarter@iamfanatics.com`).

**Result:** PASS — approved password-reset capability worked.

**Detailed evidence:**  
[Authorization Test Plan & Results](07-Testing/Authorization-Test-Plan-and-Results.md)  
[Technical Design](05-Technical-Design/AD-Delegated-Password-Reset-Design.md)

---

<a name="evidence-least-privilege"></a>

## Least-Privilege Boundary

Password-reset authority was treated as a discrete entitlement rather than an administrator role.

Explicitly excluded capabilities included:

- Domain Admin;
- Domain Controller administration;
- GPO administration;
- unrestricted server administration;
- privileged-account administration;
- group-membership administration;
- broad user-property modification.

A negative authorization test verified the boundary.

Maya attempted to modify Daniel Carter's group membership.

**Result:** PASS — access denied.

The denial was as important as the successful password reset because it demonstrated that the role could perform its required function without unrelated directory-administration authority.

**Detailed evidence:**  
[Business Requirements](02-Discovery-and-Requirements/Business-Requirements.md)  
[Authorization Test Results](07-Testing/Authorization-Test-Plan-and-Results.md)

---

<a name="evidence-authorization-testing"></a>

## Authorization Testing

The case used multiple test classes instead of relying on a single successful action.

| Test | Expected | Result |
|---|---|---|
| Maya resets Daniel's standard-user password | Allow | **PASS** |
| Maya modifies Daniel's group membership | Deny | **PASS — denied** |
| Privileged identity inherits the original reset scope | Must not occur | **FINDING** |
| Maya resets Marcus after remediation | Deny | **PASS — denied** |

The testing strategy therefore evaluated:

**Can the operator perform the required task?**

and:

**Can the operator perform something that should be prohibited?**

The case then went further by pressure-testing a higher-risk privileged identity population.

**Detailed evidence:**  
[Authorization Test Plan & Results](07-Testing/Authorization-Test-Plan-and-Results.md)

---

<a name="evidence-acl-inheritance"></a>

## Pressure Test — ACL Inheritance Finding

The original directory structure contained:

```text
Fanatics-Users
├── Corporate
├── Technology
└── Privileged
```

Password-reset delegation was applied at `Fanatics-Users` and inherited by descendant user objects.

That meant the nested `Privileged` OU also inherited the IT Support password-reset permission.

A disabled simulated legacy privileged identity, **Marcus Vale** (`mvale@iamfanatics.com`), was used to test the boundary.

The pressure test demonstrated an important distinction:

> A technically correct ACL can still produce an incorrect authorization model when the directory hierarchy causes the permission to apply to the wrong population.

**Finding:** The technical scope exceeded the approved business scope.

**Detailed evidence:**  
[Finding F-001 — Privileged OU Scope](08-Findings-and-Remediation/Privileged-OU-Scope-Finding.md)

---

<a name="evidence-privileged-boundary"></a>

## Privileged Identity Remediation

The excessive scope was not solved by simply accepting the inherited permission or treating the disabled account as harmless.

The privileged identity population was structurally separated into:

`Fanatics-Privileged-Users`

Marcus was moved outside the standard `Fanatics-Users` inheritance boundary.

The obsolete nested `Fanatics-Users\Privileged` OU was later verified empty and removed as a post-remediation hardening action.

After the change, Maya attempted to reset Marcus's password from `FAN-ITSUP01`.

**Result:** PASS — Access Denied.

The remediation preserved the valid standard-user support capability while removing the unintended privileged-user scope.

**Detailed evidence:**  
[Privileged Scope Finding & Remediation](08-Findings-and-Remediation/Privileged-OU-Scope-Finding.md)  
[ADR-001 — Separate Privileged Identities](../../07-Architecture/Architecture-Decision-Records/ADR-001-Separate-Privileged-Identities.md)

---

<a name="evidence-troubleshooting"></a>

## Troubleshooting & Test Assurance

An earlier authorization test attempted to run ADUC on the domain controller using `runas /netonly`.

The local process token remained:

`FANATICS\Administrator`

Because that context was not sufficiently clean for proving Maya's delegated authority, the resulting password-reset attempts were **not accepted as final authorization evidence**.

Instead of forcing a conclusion from ambiguous evidence, the test method was changed.

A domain-joined Windows 11 workstation was built and Maya signed into it interactively using her normal identity.

The authorization tests were then repeated from that environment.

This produced trustworthy positive and negative results.

**Control-assurance lesson:** security testing is not only about whether an action succeeds. The identity, execution context, and provenance of the evidence matter.

**Detailed evidence:**  
[Finding F-002 — Test Method Assurance](08-Findings-and-Remediation/Test-Method-Assurance-Finding.md)

---

<a name="evidence-powershell"></a>

## PowerShell-Assisted Technical Validation

The lab uses a **GUI-first, PowerShell-second** learning model.

Active Directory delegation and group relationships were first understood through administrative tooling, then command-line verification was used to validate ACL and directory state.

PowerShell therefore supported control verification rather than replacing understanding of the underlying Active Directory authorization model.

**Detailed evidence:**  
[Technical Design](05-Technical-Design/AD-Delegated-Password-Reset-Design.md)  
[Implementation Record](06-Implementation/Implementation-Record.md)

---

## Security Impact

The inherited privileged password-reset scope created risk because password reset changes the credential associated with an identity.

If an IT Support operator can reset a privileged identity, an otherwise limited support role may gain a path to control or disrupt a more powerful account.

The issue therefore affected:

| Security property | Relevance |
|---|---|
| **Confidentiality** | Privileged account control could expose protected information |
| **Integrity** | Unauthorized personnel could alter privileged credential state |
| **Availability** | Improper password changes could disrupt authorized administrative access |
| **Authorization** | Effective permission exceeded the approved business boundary |
| **Accountability** | Excessive scope weakens defensible administrative responsibility |

## Certification & Security Mapping

**Certification-aligned knowledge:**  
`Security+` · `SC-300` · `Okta / cross-platform IAM concepts`

**Security frameworks & principles:**  
`Least Privilege` · `Separation of Duties` · `Zero Trust` · `NIST CSF 2.0` · `NIST SP 800-53` · `ISO/IEC 27001/27002`

Case 001 particularly reinforces access enforcement, least privilege, separation of duties, effective permissions, privileged-access boundaries, account administration, mitigation/remediation, and control validation.

The Active Directory implementation itself is not presented as completion of an Entra-specific SC-300 objective. Instead, it establishes the authorization and governance reasoning that will be applied to subsequent Microsoft Entra cases.

## Results

The final authorization model demonstrated that:

| Required behavior | Outcome |
|---|---|
| IT Support Analyst can reset a standard user's password | **PASS** |
| IT Support Analyst cannot modify unrelated group memberships | **PASS** |
| IT Support Analyst cannot reset a privileged identity | **PASS** |
| Privileged identities remain outside standard support delegation | **PASS** |
| Authorization testing uses a valid non-admin operator context | **PASS** |

## Control Improvement

The case resulted in more than a one-time technical correction.

The lab now carries forward the following control expectations:

- privileged identities remain structurally separated from standard workforce delegation;
- delegated-access changes require positive and negative authorization tests;
- high-risk populations should be pressure-tested;
- ambiguous authorization evidence should be rejected and retested correctly;
- OU changes require review of delegated ACL scope;
- role membership and sensitive entitlements require lifecycle review.

## Lessons Learned / Post-Implementation Review

The initial password-reset permission was technically functional, but the surrounding directory structure made its effective scope too broad.

The primary lesson was:

> **Permission design cannot be evaluated independently from object placement, inheritance, and effective authorization scope.**

If this environment were being designed from scratch, privileged identities would be structurally separated before standard-user delegation was implemented.

The original test plan would also include a privileged-scope negative test from the beginning rather than treating the standard-user positive test as sufficient.

A second lesson was that questionable evidence should not be rationalized. When the `/netonly` execution context made the authorization result ambiguous, the correct response was to improve the test environment and repeat the test.

## Case Artifacts

| Artifact | Purpose |
|---|---|
| [IAM-2026-0047](01-Work-Item/IAM-2026-0047.md) | Simulated ITSM work item |
| [Discovery Notes](02-Discovery-and-Requirements/Discovery-Meeting-Notes.md) | Business/stakeholder discovery |
| [Business Requirements](02-Discovery-and-Requirements/Business-Requirements.md) | Approved capability and exclusions |
| [Role Design](03-Role-and-Entitlement-Design/IT-Support-Analyst-Role-Design.md) | RBAC model |
| [Approval Record](04-Approval/Approval-Record.md) | Simulated production approval |
| [Technical Design](05-Technical-Design/AD-Delegated-Password-Reset-Design.md) | AD permission architecture |
| [Implementation Record](06-Implementation/Implementation-Record.md) | Technical implementation |
| [Authorization Testing](07-Testing/Authorization-Test-Plan-and-Results.md) | Positive/negative/pressure tests |
| [Privileged Scope Finding](08-Findings-and-Remediation/Privileged-OU-Scope-Finding.md) | Security finding and remediation |
| [Test Assurance Finding](08-Findings-and-Remediation/Test-Method-Assurance-Finding.md) | Evidence/test-method correction |
| [Closure & Lifecycle](09-Closure-and-Lifecycle/Closure-and-Lifecycle-Review.md) | Closure and ongoing governance |
| [Interview Story](09-Closure-and-Lifecycle/Interview-Story.md) | Concise scenario explanation |

## Portfolio Disclaimer

This case study is part of a fictional cybersecurity/IAM home lab.

All named stakeholders, business processes, approvals, organizational relationships, incidents, and work items are fictional or simulated for learning and portfolio demonstration.

Technical lab actions are distinguished from simulated production processes. No employer systems, credentials, confidential information, or production data are used.