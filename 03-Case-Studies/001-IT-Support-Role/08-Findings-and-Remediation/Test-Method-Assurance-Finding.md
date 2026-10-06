# Finding F-002 — Authorization Test Used an Ambiguous Execution Context

## Condition
The first test launched ADUC on the DC with `runas /netonly`; the local process token remained `FANATICS\Administrator`.

## Risk
A control test is only meaningful when the identity exercising the control is known with sufficient confidence. Ambiguous execution context can create a false conclusion about whether delegation works.

## Decision
Do not use the preliminary reset outcomes as final evidence.

## Remediation
Build/use `FAN-ITSUP01`, sign in interactively as Maya, and repeat all material positive/negative tests.

## Control Improvement
Future authorization tests should:
1. use the real delegated identity;
2. use a workstation appropriate to the role;
3. verify the active identity;
4. avoid Domain Admin context unless explicitly required;
5. separate configuration inspection from functional authorization proof.

## Lesson
Evidence provenance and test identity are part of security-control assurance.
