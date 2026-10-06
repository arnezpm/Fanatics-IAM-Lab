# Technical Design — AD Delegated Password Reset

## Objective
Allow approved IT Support Analysts to reset standard workforce passwords without broad directory administration.

## Group Model
- `GG-IT-Support` — broad functional group
- `GG-IT-Support-Analysts` — role group
- `GG-Service-Desk-Analysts` — separate role group
- `DL-IT-User-Password-Reset` — permission group

## Delegation
The Delegate Control wizard was used on `Fanatics-Users` with:
- User objects
- Reset Password only
- Applies to descendant user objects

Verified ACL characteristics at the delegation point:
- Identity: `FANATICS\DL-IT-User-Password-Reset`
- Type: Allow
- Right: Reset Password / ExtendedRight
- Inherited from: None

## Original Structural Risk
```text
Fanatics-Users
├── Corporate
├── Technology
└── Privileged
```
The nested `Privileged` OU inherited the same reset delegation, making the technical scope broader than the business-approved scope.

## Remediated Boundary
```text
ad.fanatics.local
├── Fanatics-Users
│   ├── Corporate
│   └── Technology
├── Fanatics-Privileged-Users
├── Fanatics-Groups
├── Fanatics-Computers
└── Fanatics-ServiceAccounts
```
The obsolete nested `Fanatics-Users\Privileged` OU was verified empty and removed after the privileged identity boundary was validated.

## Decision Rationale
Structural separation was preferred over duplicated delegations or inheritance blocking because it produces a clearer security/lifecycle boundary and is easier to reason about.

## Operator Workstation
Final testing used `FAN-ITSUP01`, a Windows 11 Pro domain member with RSAT. Maya signed in interactively as `FANATICS\mrodriguez`; no interactive DC logon was required.
