# Business Requirements — IT Support Analyst Password Reset

## BR-001 — Standard Workforce Password Reset
IT Support Analysts require the ability to reset passwords for standard Corporate and Technology workforce users.

## BR-002 — Role-Based Assignment
Access must be assigned through a role/entitlement group model rather than directly to an individual analyst.

## BR-003 — Least Privilege
The entitlement must grant only Reset Password and must not imply group administration, broad user writes, Domain Admin, GPO administration, server administration, or privileged-user administration.

## BR-004 — Independent Authorization Testing
Testing must use a non-administrative operator in a normal support-workstation context.

## BR-005 — Negative Testing
At least one unrelated administrative action must be attempted and denied.

## BR-006 — Privileged Boundary Pressure Test
Privileged identities must remain outside the reset scope.

## BR-007 — Lifecycle Review
Role membership and entitlement scope must be reviewable/removable after role change, termination, requirement changes, or security findings.

## Deferred Requirements
- Account unlock
- Scoped directory read
- Endpoint-management support
- ServiceNow Analyst access
