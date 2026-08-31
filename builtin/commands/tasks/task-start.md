# Start task

## Metadata

| Field | Value |
|---|---|
| ID | task.start |
| Description | Starts one or more pending tasks. |
| Origin | builtin |
| Language | en |
| Applies | |

## Usage

```text
task.start(
    selector
)
```

## Parameters

| Name | Required | Default | Description |
|---|---|---|---|
| selector | yes | | Primary parameter. Selects zero, one, or multiple pending tasks. |

The primary parameter may be provided positionally:

```text
task.start("001-create-binary")
```

or by name:

```text
task.start(
    selector = "001-create-binary"
)
```

Quoted values are literals. Unquoted values are references resolved from the current execution context.

## Purpose

Start execution of tasks that are currently pending.

## Selector

A selector identifies zero, one, or multiple tasks.

The canonical model does not prescribe a specific selector syntax.

Adapters may support identifiers, patterns, sets, expressions, queries, filters, or other suitable mechanisms.

If the selector matches no applicable tasks, the command must produce a warning and complete without changing state.

If the selector matches multiple tasks, the complete target set must be resolved before applying changes.


Only tasks in the `pending` state are applicable to this command.

## Preconditions

For every applicable selected task:

- the task must exist;
- the task must be in the `pending` state;
- the transition to `active` must be valid.

## Operation

Change every applicable selected task from `pending` to `active`.

## Effects

Each selected task becomes active and available for execution.

The task definition must not be modified solely because of this state transition.

## Outputs

For each affected task:

- task reference;
- previous state: `pending`;
- current state: `active`.

The output may be used as the primary input of a compatible chained command.

## Warnings

If no applicable tasks match the selector, produce a warning and perform no changes.

## Errors

The command must fail when a selected applicable task cannot be transitioned safely.

## Examples

```text
task.start("001-create-binary")
```

```text
task.start(
    selector = "build-*"
)
```

```text
task.start(task_ref)
```
