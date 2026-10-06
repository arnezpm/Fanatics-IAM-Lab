# Case Study 001 — IT Support Analyst Access Standardization

> **Portfolio disclaimer:** This is a fictional cybersecurity IAM home-lab case. Fanatics, named stakeholders, business processes, approvals, incidents, and organizational relationships are fictional/simulated for learning and portfolio demonstration. Technical lab actions are distinguished from simulated production processes. No employer systems, credentials, or confidential data are used.

## Case Summary

**Case ID:** IAM-2026-0047  
**Portfolio role:** Paul M. Arnez — IAM Analyst, Cybersecurity — Identity & Access Management  
**Business owner:** Tyler Mackelroy — Senior IT Support Manager  
**Primary operator:** Maya Rodriguez — IT Support Analyst (`mrodriguez@iamfanatics.com`)  
**Standard-user target:** Daniel Carter (`dcarter@iamfanatics.com`)  
**Privileged-scope test identity:** Marcus Vale — disabled simulated legacy privileged identity (`mvale@iamfanatics.com`)  
**Systems:** Active Directory Domain Services, ADUC/RSAT, Windows 11 domain member  
**Domain:** `ad.fanatics.local`  
**UPN suffix:** `iamfanatics.com`  
**Status:** Closed — technically remediated, validated, documented, and post-remediation OU cleanup completed.

## Business Problem
IT Support needed a repeatable, least-privilege way to reset standard workforce passwords without broad AD administration.

## Final Authorization Model
```text
Maya Rodriguez
    ↓
GG-IT-Support-Analysts
    ↓
DL-IT-User-Password-Reset
    ↓
Reset Password extended right
    ↓
Standard workforce users under Fanatics-Users
```
Privileged identities are separated under the top-level `Fanatics-Privileged-Users` boundary.

## What This Case Demonstrates
- Requirements-to-entitlement translation
- RBAC and group nesting
- Delegated AD administration
- Positive and negative authorization testing
- Pressure testing beyond the happy path
- ACL inheritance analysis
- Privileged identity boundary design
- Remediation and retesting
- Evidence-quality assurance
- Control/framework mapping
- Lessons learned and lifecycle review

## Key Results
| Test | Expected | Result |
|---|---|---|
| Maya resets Daniel password | Allow | PASS |
| Maya modifies Daniel group membership | Deny | PASS — denied |
| Original nested Privileged OU inherits reset scope | Must not occur | FINDING |
| Maya resets Marcus after OU separation | Deny | PASS — denied |

## Evidence Standard
A preliminary ADUC test launched with `runas /netonly` on the DC was not accepted as authoritative evidence because the local token remained `FANATICS\Administrator` and the context was ambiguous for this control test. Final tests were repeated from `FAN-ITSUP01` with Maya interactively signed in as `FANATICS\mrodriguez`.
