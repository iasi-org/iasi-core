# External inputs must not be overwritten

## Metadata

| Field | Value |
|---|---|
| ID | inputs.externals.no-overwrite |
| Description | Preserves external inputs as immutable evidence of what IASI received. |
| Scope | inputs/externals |
| Level | must-not |
| Tags | inputs; externals; immutability; provenance; traceability |

## Rule

An artifact already incorporated into `inputs/externals/` must not be overwritten, rewritten, normalized, corrected, completed, or otherwise modified by IASI.

Import or copy operations must be create-only with respect to existing external artifacts.

When an outside source changes, the changed material must be incorporated as new evidence rather than replacing the previously retained artifact.

## Exceptions

None for active IASI processing.

Administrative recovery from filesystem corruption or accidental damage is outside normal IASI processing and must preserve or restore the original recorded evidence.

## Rationale

`inputs/externals/` records what IASI actually received from outside the system. Overwriting an existing external artifact would rewrite the historical evidence and could make later material appear to have been available earlier than it really was.

Protecting external artifacts from overwrite turns immutability from a working convention into an enforceable system property and preserves provenance, traceability, reproducibility, and the integrity of the engineering history.

## Sources

- IASI Journey, 2026-08-30, "La frontera también se protege".
- Existing IASI principle that `inputs/externals/` is read-only from the IASI process perspective.

## Examples

Correct:

```text
OUTSIDE requirements-v1.md
        ↓ import
inputs/externals/requirements-v1.md

OUTSIDE later changes
        ↓ import as new evidence
inputs/externals/requirements-v2.md
```

Incorrect:

```text
OUTSIDE requirements-v2.md
        ↓ overwrite
inputs/externals/requirements.md
```

The second case destroys the evidence of what IASI originally received.
