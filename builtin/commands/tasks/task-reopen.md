# Reopen task

## Metadata

| Field | Value |
|---|---|
| ID | task.reopen |
| Description | Reopens one or more completed tasks for additional work. |
| Origin | builtin |
| Language | en |
| Applies | |

## Usage

```text
task.reopen(
    selector
)
```

## Parameters

| Name | Required | Default | Description |
|---|---|---|---|
| selector | yes | | Primary parameter. Selects zero, one, or multiple completed tasks. |

The primary parameter may be provided positionally:

```text
task.reopen("001-create-binary")
```

or by name:

```text
task.reopen(
    selector = "001-create-binary"
)
```

Quoted values are literals. Unquoted values are references resolved from the current execution context.

## Purpose

Return completed tasks to `active` when additional work is required.

`reopen` is used to continue, extend, correct, or revise previously closed work.

It differs from `rerun`, which retries a failed execution.

## Selector

A selector identifies zero, one, or multiple tasks.

The canonical model does not prescribe a specific selector syntax.

Adapters may support identifiers, patterns, sets, expressions, queries, filters, or other suitable mechanisms.

If the selector matches no applicable tasks, the command must produce a warning and complete without changing state.

If the selector matches multiple tasks, the complete target set must be resolved before applying changes.


Tasks under `done/<outcome>` are applicable when reopening them is semantically valid.

## Preconditions

For every applicable selected task:

- the task must exist;
- the task must be completed;
- there must be a justified reason to continue, extend, correct, or revise the work.

## Operation

Move every applicable selected task from `done/<outcome>` to `active`.

## Effects

Each selected task becomes active again and may be run further.

The task definition must not be modified solely because it was reopened.

## Outputs

For each affected task:

- task reference;
- previous state and outcome;
- current state: `active`.

## Warnings

If no applicable tasks match the selector, produce a warning and perform no changes.

## Errors

The command must fail when:

- an unquoted reference cannot be resolved;
- a selected applicable task cannot be reopened safely.

## Examples

```text
task.reopen("001-create-binary")
```

```text
task.reopen(
    selector = current_task
)
```

Conceptually:

```text
rerun  = retry failed execution
reopen = continue, extend, correct, or revise closed work
```
