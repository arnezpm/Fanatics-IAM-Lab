# Finding F-001 — Password-Reset Delegation Extended into Privileged Identity Scope

**Severity:** Medium in the controlled lab; potentially High in production depending on the privileged identity  
**Status:** Remediated and retested

## Condition
The original nested `Fanatics-Users\Privileged` OU inherited the parent Reset Password delegation.

## Why It Matters
Password reset changes another identity's authenticator. If a support analyst can reset a privileged identity, the role's effective authorization exceeds the business need.

Potential impacts:
- unauthorized control or disruption of a privileged identity;
- account-takeover opportunity;
- weakened separation of duties;
- loss of least-privilege assurance;
- confidentiality, integrity, and availability risk.

## Pressure-Test Scenario
Marcus Vale represented a disabled legacy privileged account. Disabled status does not remove delegated ACLs from the directory object; object placement and permissions still determine who can administer it.

## Immediate Mitigation
- Do not place additional privileged users in the inherited standard-user hierarchy.
- Keep the simulated privileged identity disabled while testing.

## Root-Cause Remediation
Create/use the top-level `Fanatics-Privileged-Users` OU and move privileged identities outside the `Fanatics-Users` inheritance boundary.

## Hardening
1. The obsolete nested `Fanatics-Users\Privileged` OU was verified empty and removed after dependency checks.
2. Document privileged-user placement as an architecture standard.
3. Add privileged-boundary pressure testing to delegated-access changes.
4. Review delegated ACLs after OU redesigns.
5. Periodically recertify IT Support Analyst role membership.

## Retest
Maya's reset attempt against Marcus from `FAN-ITSUP01` was denied.  
**Result:** PASS

## Security / Standards Mapping
### NIST CSF 2.0
**PR.AA-05:** permissions, entitlements, and authorizations are managed/enforced/reviewed and incorporate least privilege and separation of duties.

### NIST SP 800-53 Rev. 5
- AC-2 — Account Management
- AC-3 — Access Enforcement
- AC-5 — Separation of Duties
- AC-6 — Least Privilege

### ISO/IEC 27001:2022 / 27002:2022
Relevant control areas:
- 5.15 — Access control
- 5.18 — Access rights
- 8.2 — Privileged access rights
- 8.3 — Information access restriction

### SC-300
Foundational alignment with effective permissions, authorization, Zero Trust/least privilege, troubleshooting, role assignment, and privileged-access boundaries. The current SC-300 blueprint explicitly expects identity/access administrators to evaluate permissions, troubleshoot access, implement governance, and apply Zero Trust principles.

### CompTIA Security+ SY0-701
Reinforces authentication vs authorization, RBAC, least privilege, privileged-account risk, account management, control testing, mitigation/remediation, and CIA impact analysis.

## Lessons Learned
A technically correct ACE can still be unsafe if the hierarchy makes its effective scope too broad. Disabled/stale accounts remain security-relevant directory objects.

## What We Would Do Differently
Separate privileged identities before implementing standard-user delegation, and include privileged negative testing in the original test plan.
