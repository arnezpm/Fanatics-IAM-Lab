# Implementation Record — IAM-2026-0047

## Implemented State
- Maya (`mrodriguez@iamfanatics.com`) is a member of `GG-IT-Support-Analysts`.
- `GG-IT-Support-Analysts` is nested into `GG-IT-Support` and `DL-IT-User-Password-Reset`.
- `DL-IT-User-Password-Reset` has Reset Password on descendant users under `Fanatics-Users`.

## Pressure-Test Setup
Marcus Vale was created as a **disabled simulated legacy privileged identity**. The account was intentionally disabled to reproduce a stale privileged-account condition; its timestamps are not represented as genuine historical age evidence.

## Finding and Remediation
ACL inspection showed the reset ACE inherited into `Fanatics-Users\Privileged`.

A new top-level `Fanatics-Privileged-Users` OU was created and Marcus was moved there, removing him from the standard workforce delegation hierarchy.

## Workstation Validation
`FAN-ITSUP01` was built and joined to `ad.fanatics.local`. RSAT/ADUC was installed and final tests were performed from Maya's genuine interactive domain session.

## Test-Method Correction
Earlier ADUC testing used `runas /netonly` on the DC. `whoami` showed the local token remained `FANATICS\Administrator`. Because that created ambiguity for authorization proof, those reset attempts were excluded from final evidence and repeated correctly from `FAN-ITSUP01`.

## Production-Style Ownership
Paul owns requirements, entitlement analysis, approved administration, troubleshooting, testing, and documentation. Structural OU architecture is represented as Infrastructure/IAM Engineering owned in the fictional production model.
