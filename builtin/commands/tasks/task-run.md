# Run task

## Metadata

| Field | Value |
|---|---|
| ID | task.run |
| Description | Runs one or more active tasks. |
| Origin | builtin |
| Language | en |
| Applies | |

## Usage

```text
task.run(
    selector,
    completion = "auto"
)
```

## Parameters

| Name | Required | Default | Description |
|---|---|---|---|
| selector | yes | | Primary parameter. Selects zero, one, or multiple active tasks. |
| completion | no | auto | Completion mode: `auto` or `manual`. |

The primary parameter may be provided positionally or by name.

All parameters may be provided by name regardless of their textual position:

```text
task.run(
    completion = "manual",
    selector = "001-create-binary"
)
```

Quoted values are literals. Unquoted values are references resolved from the current execution context.

## Purpose

Run the work defined by tasks that are currently active.

A task may be run multiple times while it remains active.

## Selector

A selector identifies zero, one, or multiple tasks.

The canonical model does not prescribe a specific selector syntax.

Adapters may support identifiers, patterns, sets, expressions, queries, filters, or other suitable mechanisms.

If the selector matches no applicable tasks, the command must produce a warning and complete without changing state.

If the selector matches multiple tasks, the complete target set must be resolved before applying changes.


Only tasks in the `active` state are applicable to this command.

## Completion

### auto

`auto` is the default.

When execution determines that a task has finished, it may complete the task automatically and place it under the appropriate `done/<outcome>` state.

If the work remains incomplete, the task remains `active`.

### manual

The task remains `active` after execution.

A separate `task.done` command is required to consolidate the existing execution result and complete the task.

This mode is intended for work that requires manual review, inspection, approval, or another explicit decision before completion.

## Preconditions

For every applicable selected task:

- the task must exist;
- the task must be in the `active` state;
- the executor must have access to the context required by the task.

## Operation

Run the work described by every applicable selected task using the available execution context.

Execution may be repeated as many times as required while a task remains active.

## Effects

Execution may modify project artifacts as required by the task.

With `completion = "manual"`, the task remains `active`.

With `completion = "auto"`, a finished task may transition to `done/<outcome>`.

The outcome is produced by execution. It is not supplied as an input parameter.

## Outputs

For each affected task:

- task reference;
- execution result;
- resulting state;
- outcome when execution completes the task.

The output may be used as the primary input of a compatible chained command.

## Warnings

If no applicable tasks match the selector, produce a warning and perform no changes.

## Errors

Execution failures must be reported.

An unresolved unquoted reference is an error.

An incomplete execution must not be reported as successfully completed.

## Examples

Default automatic completion:

```text
task.run("001-create-binary")
```

Named primary parameter:

```text
task.run(
    selector = "001-create-binary"
)
```

Manual completion:

```text
task.run(
    "001-create-binary",
    completion = "manual"
)
```

Reference from the execution context:

```text
task.run(
    selector = current_task,
    completion = "manual"
)
```
