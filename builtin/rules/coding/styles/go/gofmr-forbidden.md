# Preserve Go source formatting

## Metadata

| Field | Value |
|---|---|
| ID | coding.styles.go.preserve-formatting |
| Description | Preserve deliberate formatting in Go source code. |
| Scope | coding/go |
| Level | must |
| Tags | coding; go; style; formatting |

## Rule

Do not execute `gofmt`, `go fmt` or any automatic formatter over Go source code owned by the project.

Existing whitespace, indentation and alignment MUST be preserved unless a change is required by the work being performed.

Formatting MAY be changed deliberately when editing code, but MUST NOT be normalized automatically.

## Exceptions

Generated or externally maintained source MAY use the formatting required by its generator or upstream source.

## Rationale

Formatting is part of the intentional representation of the source code.

Alignment and whitespace may be used to expose logical structure and improve human readability. Automatic normalization can remove that information.
