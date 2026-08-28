# Command-line help

## Metadata

| Field | Value |
|---|---|
| ID | coding.cli.help |
| Description | Requires help for anything executable from the command line. |
| Scope | coding; cli |
| Level | must |
| Tags | coding; cli; help; usability |

## Rule

Anything that can be executed from the command line must provide help describing its purpose and usage.

## Exceptions

None.

## Rationale

Command-line functionality must be discoverable without requiring access to external documentation or source code.

## Sources

IASI

## Examples

A command such as:

    iasi create

must provide an accessible help mechanism, for example:

    iasi create --help