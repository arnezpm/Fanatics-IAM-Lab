# Evidence Manifest — IAM-2026-0047

## Actual Lab Validation
| Evidence | Status |
|---|---|
| Maya in `GG-IT-Support-Analysts` | Observed |
| Role group in reset permission group | Observed |
| Reset ACE on `Fanatics-Users` | Observed |
| Reset ACE inherited into original nested Privileged OU | Observed |
| Maya reset Daniel from `FAN-ITSUP01` | Observed |
| Maya group change on Daniel denied | Observed |
| Maya reset Marcus after OU separation denied | Observed |
| Effective Access shows Maya reset denied on Marcus | Observed |
| `/netonly` token remained Administrator | Observed; used to reject preliminary evidence |

## Simulated Business Artifacts
Work item, discovery meeting notes, approval record, production responsibility assignments, and business/security stakeholder narratives are simulated.

## Optional Final Screenshots
1. Delegated ACE on `Fanatics-Users`
2. Inherited ACE on obsolete nested Privileged OU if still present
3. Maya reset success for Daniel
4. Daniel group-change denial
5. Marcus reset denial

Do not recreate/fabricate a system screenshot if the original state no longer exists. A reconstructed demonstration must be clearly labeled.

## Sensitive Data Rule
Never publish passwords, secrets, tokens, private keys, or unrelated personal/host information.
