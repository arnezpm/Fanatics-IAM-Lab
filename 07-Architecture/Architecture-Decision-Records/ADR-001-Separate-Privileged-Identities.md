# ADR-001 — Separate Privileged Identities from Standard Workforce OU Hierarchy

**Status:** Accepted  
**Case:** IAM-2026-0047

## Context
The parent `Fanatics-Users` reset delegation propagated to the nested Privileged OU.

## Decision
Use a separate top-level `Fanatics-Privileged-Users` OU for privileged human identities.

## Alternatives
1. Duplicate the reset delegation on Corporate and Technology.
2. Block inheritance on the nested Privileged OU.
3. Structural separation — selected.

## Rationale
Structural separation creates a clearer administrative/lifecycle boundary, reduces inheritance complexity, and supports future privileged-access controls.

## Consequences
Standard Corporate/Technology users retain delegated support; privileged users do not inherit the standard-user reset permission.

## Validation
Maya was denied when attempting to reset Marcus after the move.
