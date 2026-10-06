# Authorization Test Plan and Results — IAM-2026-0047

## Principles
- Never use Domain Admin to prove delegated authority.
- Test both allowed and denied actions.
- Pressure-test high-risk scope.
- Reject evidence when the execution identity is ambiguous.
- Retest after remediation.

## Results
### T01 — Role Membership Path
Maya → `GG-IT-Support-Analysts`; role group → `GG-IT-Support` and `DL-IT-User-Password-Reset`.  
**Result:** PASS

### T02 — Delegated ACL
`DL-IT-User-Password-Reset` had Allow / Reset Password / Descendant User objects on `Fanatics-Users`.  
**Result:** PASS

### T03 — Positive Authorization
**Operator:** `FANATICS\mrodriguez` on `FAN-ITSUP01`  
**Target:** Daniel Carter (`dcarter@iamfanatics.com`)  
**Action:** Reset password  
**Observed:** Succeeded  
**Result:** PASS

### T04 — Negative Authorization
**Action:** Maya attempted to modify Daniel's group membership.  
**Observed:** Access/permission denied  
**Result:** PASS

### T05 — Pressure Test: Original Privileged Scope
ACL inheritance inspection on the original nested Privileged OU showed the Reset Password ACE inherited from `Fanatics-Users` and applied to descendant user objects.  
**Result:** CONTROL FAIL / FINDING

### T06 — Preliminary `/netonly` Method
The local token remained Administrator, so reset outcomes from that session were not accepted as final authorization evidence.  
**Result:** TEST METHOD REJECTED

### T07 — Post-Remediation Effective Access
For Marcus in `Fanatics-Privileged-Users`, Maya's effective Reset Password access showed denied/unavailable.  
**Result:** PASS

### T08 — Post-Remediation Live Test
Maya attempted to reset Marcus from `FAN-ITSUP01`.  
**Observed:** Access denied  
**Result:** PASS

## Conclusion
The final design permits the intended standard-user password reset and denies unrelated group administration and privileged-user password reset.
