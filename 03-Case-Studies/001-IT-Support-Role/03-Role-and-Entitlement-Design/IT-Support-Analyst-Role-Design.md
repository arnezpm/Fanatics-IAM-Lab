# IT Support Analyst — Role and Entitlement Design

## Role Group
`GG-IT-Support-Analysts` — Global Security Group representing the IT Support Analyst role.

It is a member of the broader functional group `GG-IT-Support`.

## Entitlement Group
`DL-IT-User-Password-Reset` — Domain Local Security Group representing the Reset Password permission.

## Assignment Chain
```text
User account
  → GG-IT-Support-Analysts
  → DL-IT-User-Password-Reset
  → Reset Password on approved standard workforce user objects
```

## Validation Member
Maya Rodriguez  
UPN: `mrodriguez@iamfanatics.com`  
Domain logon: `FANATICS\mrodriguez`

## Entitlement Decisions
| Responsibility | Candidate entitlement | Case 001 |
|---|---|---|
| Reset password | AD Reset Password | Implemented |
| Unlock account | AD Unlock Account | Deferred |
| Basic account lookup | AD User Read | Deferred |
| Workstation support | Endpoint support privilege | Deferred |
| Service Desk tickets | ServiceNow Analyst | Deferred |

## Explicit Exclusions
Domain Admin, DC administration, privileged-account administration, GPO administration, unrestricted server administration, and unrelated group-membership administration.

## Service Desk Boundary
`GG-Service-Desk-Analysts` is not automatically added to `DL-IT-User-Password-Reset`. Related job function does not equal entitlement approval.
