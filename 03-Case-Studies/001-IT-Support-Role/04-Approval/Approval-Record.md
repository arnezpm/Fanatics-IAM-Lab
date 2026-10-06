# Approval Record — IAM-2026-0047

> **Artifact:** Simulated production approval record. No claim is made that real-world stakeholders approved the home-lab configuration.

## Initial Approval
| Approver/reviewer | Capacity | Decision |
|---|---|---|
| Tyler Mackelroy | Business owner | Approves need for standard-user password reset |
| Derek Orrbuck | Senior IAM reviewer | Approves group-based design subject to boundary testing |
| Matt Maginotta | Director, IAM | Approves IAM implementation within defined scope |
| Paul M. Arnez | IAM Analyst | Recommends design; does not self-approve business need |

## Conditions
- Standard Corporate/Technology users only
- No privileged-user administration
- No Domain Admin requirement
- Positive and negative tests required
- Entitlement subject to review/removal

## Remediation Approval
After inherited reset scope was identified in the nested privileged OU, the simulated production decision was to separate privileged identities into `Fanatics-Privileged-Users`, preserve the standard workforce delegation, and retest.

A production structural OU change is represented as Infrastructure/IAM Engineering owned, with Paul responsible for analysis and validation rather than unrestricted directory architecture.
