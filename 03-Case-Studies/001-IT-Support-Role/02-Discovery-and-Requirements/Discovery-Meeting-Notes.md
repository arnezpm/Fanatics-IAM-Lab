# Discovery Meeting Notes — IT Support Analyst Access Standardization

> **Artifact:** Simulated business meeting record  
> **Case:** IAM-2026-0047

## Participants
| Participant | Role | Contribution |
|---|---|---|
| Tyler Mackelroy | Senior IT Support Manager | Business/role owner; defines analyst responsibilities |
| Paul M. Arnez | IAM Analyst | Requirements discovery; entitlement translation; testing/documentation |
| Derek Orrbuck | Senior IAM Analyst | Technical challenge and least-privilege review |
| Matt Maginotta | Director, IAM | IAM oversight and approval |
| Aleksander Cifin | Identity / IAM Engineer | Consulted for engineering-level changes |
| Suraj Rakhsashana | Principal Security Engineer | Consulted for privileged-boundary/security concerns |

## Responsibilities Identified
- Reset standard employee passwords
- Unlock standard employee accounts
- Basic account lookup/read
- Support employee workstations
- Work Service Desk tickets

## Phase-1 Decision
Only **Reset Password** is implemented in Case 001. Adjacent capabilities are deliberately separated because each has a different technical right and risk profile.

## Population Decision
Password reset applies to standard **Corporate and Technology** users. It does not include privileged identities.

## Review Requirements
Derek required both positive and negative authorization testing. The team also required a pressure test against a higher-risk identity population and prohibited using Domain Admin as proof that delegation worked.

## Design Direction
- Global role group for IT Support Analysts
- Domain Local permission group for the reset entitlement
- Reset Password extended right only
- No automatic entitlement for Service Desk Analysts without explicit business justification
