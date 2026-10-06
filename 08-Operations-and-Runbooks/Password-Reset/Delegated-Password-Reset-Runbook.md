# Runbook — Delegated Standard-User Password Reset

## Preconditions
- Operator is in the approved IT Support Analyst role.
- Request is tied to an approved support process.
- Target is a standard Corporate/Technology user.
- Operator uses approved support tooling/workstation.

## Procedure
1. Validate target identity per support policy.
2. Confirm target is not privileged or a service account.
3. Open ADUC as the operator's normal domain identity.
4. Locate the user.
5. Execute Reset Password.
6. Do not bundle unrelated actions.
7. Record completion in the ticket/change record.
8. Escalate ambiguous scope or unexpected denial.

## Stop / Escalate
Stop if target is privileged, a service account, ownership is unclear, the request includes unrelated privilege changes, or Domain Admin is requested.

## Boundary
Password reset does not authorize group changes, privileged administration, account unlock unless separately delegated, DC administration, GPO, or server administration.
