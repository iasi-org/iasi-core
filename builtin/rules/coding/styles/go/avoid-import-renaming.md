# Avoid Go import renaming

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.avoid-import-renaming |
| Description | Avoids renaming imports unless needed to resolve a collision. |
| Scope | coding/go |
| Level | should-not |
| Tags | coding; go; style; imports; naming |

## Rule

Imports should not be renamed unless necessary to resolve a meaningful name collision or to accommodate an unavoidable generated/external package name.

## Exceptions

Name collisions and established generated-package conventions may justify renaming.

## Rationale

Good package names should normally be usable directly, and unnecessary aliases obscure where identifiers originate.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Prefer `json.Marshal` over aliasing `encoding/json` to another arbitrary local name.
