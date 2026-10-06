# IAM Control Matrix — Case 001

| Control ID | Objective | Test | Result | Alignment |
|---|---|---|---|---|
| IAM-AC-001 | Approved analysts can reset standard-user passwords | Maya resets Daniel | PASS | NIST CSF PR.AA-05; AC-3/AC-6; ISO 5.15/5.18 |
| IAM-AC-002 | Analysts cannot administer privileged identities | Maya reset attempt on Marcus | PASS — denied | PR.AA-05; AC-5/AC-6; ISO 8.2 |
| IAM-AC-003 | Reset role cannot modify unrelated groups | Maya group-change attempt | PASS — denied | AC-3/AC-6; ISO 5.15/8.3 |
| IAM-AC-004 | Entitlement is group-based, not a direct user ACL | Membership/ACL review | PASS | RBAC / governance |
| IAM-AC-005 | Tests use a valid non-admin operator context | Final tests on FAN-ITSUP01 | PASS | Control assurance |
| IAM-AC-006 | Privileged placement avoids standard-user delegation | Inheritance pressure test + retest | PASS after remediation | PR.AA-05; AC-5/AC-6; ISO 8.2 |

IAM-AC-006 initially failed and passed after remediation.
