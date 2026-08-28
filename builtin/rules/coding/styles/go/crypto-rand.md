# Use crypto/rand for secrets

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.crypto-rand |
| Description | Uses cryptographically secure randomness for keys, tokens, and secrets. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; security; randomness |

## Rule

Keys, tokens, credentials, nonces, and other security-sensitive values must use `crypto/rand` rather than `math/rand`.

## Exceptions

None for security-sensitive randomness.

## Rationale

Pseudo-random generators intended for simulation are predictable and unsuitable for secrets.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Use `crypto/rand.Read` for token bytes.
