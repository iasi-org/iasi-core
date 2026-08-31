# Rerun task

## Metadata

| Field | Value |
|---|---|
| ID | task.rerun |
| Description | Runs again one or more tasks whose previous execution failed. |
| Origin | builtin |
| Language | en |
| Applies | |

## Usage

```text
task.rerun(
    selector,
    completion = "auto"
)
```

## Parameters

| Name | Required | Default | Description |
|---|---|---|---|
| selector | yes | | Primary parameter. Selects zero, one, or multiple failed tasks. |
| completion | no | auto | Completion mode: `auto` or `manual`. |

The primary parameter may be provided positionally or by name.

Quoted values are literals. Unquoted values are references resolved from the current execution context.

## Purpose

Retry tasks whose previous execution ended in `done/failed`.

`rerun` represents a new attempt of a failed execution.

It is not the same operation as reopening previously closed work for extension or revision.

## Selector

A selector identifies zero, one, or multiple tasks.

The canonical model does not prescribe a specific selector syntax.

Adapters may support identifiers, patterns, sets, expressions, queries, filters, or other suitable mechanisms.

If the selector matches no applicable tasks, the command must produce a warning and complete without changing state.

If the selector matches multiple tasks, the complete target set must be resolved before applying changes.


Only tasks in `done/failed` are applicable to this command.

## Preconditions

For every applicable selected task:

- the task must exist;
- the task must be in `done/failed`;
- the task must still be executable with the available context.

## Operation

For every applicable selected task:

1. move the task from `done/failed` to `active`;
2. run the task again;
3. apply the same completion semantics defined by `task.run`.

Conceptually:

```text
done/failed
    ↓
rerun
    ↓
active
    ↓
run
    ↓
new outcome
```

## Effects

With `completion = "auto"`, the rerun may finish in a new `done/<outcome>` state.

With `completion = "manual"`, the task remains `active` after execution until explicitly completed.

The new outcome is produced by the new execution.

## Outputs

For each affected task:

- task reference;
- execution result;
- resulting state;
- new outcome when completed.

## Warnings

If no applicable tasks match the selector, produce a warning and perform no changes.

## Errors

Execution failures must be reported.

An unresolved unquoted reference is an error.

## Examples

Automatic rerun:

```text
task.rerun("001-create-binary")
```

Manual rerun:

```text
task.rerun(
    selector = "001-create-binary",
    completion = "manual"
)
```
