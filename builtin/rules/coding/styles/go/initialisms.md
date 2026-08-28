# Go initialisms

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.initialisms |
| Description | Keeps common initialisms consistently capitalized in Go identifiers. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; naming; initialisms |

## Rule

Common initialisms such as `URL`, `HTTP`, `ID`, `API`, and `JSON` must keep consistent capitalization inside identifiers.

## Exceptions

An established external API may require a different spelling.

## Rationale

Consistent initialism casing makes Go identifiers predictable and idiomatic.

## Sources

Go Code Review Comments: https://go.dev/wiki/CodeReviewComments

## Examples

Preferred: `userID`, `HTTPClient`, `parseURL`.

Avoid: `userId`, `HttpClient`, `parseUrl`.
