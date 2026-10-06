# Interview Story — Case 001

## Situation
IT Support needed consistent standard-user password reset without broad AD administration.

## Responsibility
Paul translated the business requirement into a role/entitlement model, documented least-privilege boundaries, coordinated the change, and owned testing/evidence.

## Investigation
The role path and ACL were verified. Positive testing worked and an unrelated group-change test was denied. Pressure testing then showed the nested privileged OU inherited the same reset scope. An initial `/netonly` test method was also rejected because its execution context was ambiguous.

## Decision
Use structural separation for privileged identities and repeat testing from a genuine support-operator workstation.

## Action
- Created `Fanatics-Privileged-Users`.
- Moved the simulated legacy privileged identity outside the standard-user hierarchy.
- Used `FAN-ITSUP01` for final Maya testing.
- Repeated positive and negative authorization tests.

## Result
Maya could reset Daniel, could not change his groups, and could not reset Marcus after remediation.

## Control Improvement
Added privileged-boundary pressure tests, clarified OU placement standards, and established a stronger authorization-evidence method.

## Lessons Learned
The scope hierarchy can invalidate an otherwise correct ACL. If designing from scratch, privileged identities would be separated first and privileged negative tests would be included in the original test plan.
