# `InvalidChangeException(Exception)`

An error created when a change to a Rocq file leads to error that prevents the file from being successfully evaluated.

## Attributes

`diagnostics : List[Diagnostic]` [Diagnostic](../../lsp/structs/Diagnostic.md)
> List of all diagnostics that resulted from the change.

## Properties

`errors : List[Diagnostic]` [Diagnostic](../../lsp/structs/Diagnostic.md)
> Gets all diagnostics that are considered errors, which in this case are all diagnostics with severity 1.


## Operations

```python
__init__(self)
```
> Creates a new InvalidChangeException instance. `diagnostics` gets initialized to an empty list.