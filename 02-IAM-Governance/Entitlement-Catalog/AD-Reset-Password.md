# Entitlement Catalog Entry — AD Reset Password

**Entitlement ID:** ENT-AD-RESET-PASSWORD  
**Permission group:** `DL-IT-User-Password-Reset`  
**Platform:** Active Directory Domain Services

## Purpose
Allow approved support roles to reset passwords for standard workforce users.

## Permission
Active Directory Reset Password extended right on descendant standard-user objects within the approved OU boundary.

## Approved Role
`GG-IT-Support-Analysts`

## Not Included
Unlock Account, group changes, broad user-property writes, privileged-user administration, or domain administration.

## Scope
Corporate + Technology users under `Fanatics-Users`; privileged identities excluded.

## Review Triggers
Role change, OU redesign, privileged-boundary change, periodic access review, or security finding.
