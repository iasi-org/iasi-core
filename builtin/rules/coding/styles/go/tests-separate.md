# Separate Go tests from production code

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.tests-separate |
| Description | Keep Go tests separate from production code whenever possible. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; testing; structure |

## Rule

Tests MUST be kept separate from production code whenever possible.

Project tests SHOULD live under a dedicated `tests/` tree that mirrors the logical structure of the production code.

A `_test.go` file MAY be placed next to production code only when testing internal, non-exported behavior requires it and that behavior cannot reasonably be verified through the public or package-level interface.

Tests SHOULD prefer observable behavior over implementation details.

## Examples

Preferred:

```text
go/
├── cmd/
├── internal/
└── tests/
    ├── cli/
    ├── builtin/
    └── commands/
    