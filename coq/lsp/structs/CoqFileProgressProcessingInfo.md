# `CoqFileProgressProcessingInfo`

Structure containing information about the language servers progress in processing elements in the AST of the file. This structure should only exist on ranges that have not finished parsing successfully yet. The status of the progress is limited to the values defined in the [CoqFileProgressKind](../structs/CoqFileProgressKind.md) enum.

## Attributes

`range : Range` [Range](../../../lsp/structs/Range.md)
> Range for which the processing info was reported.

`kind : Optional[CoqFileProgressKind]` [CoqFileProgressKind](../structs/CoqFileProgressKind.md)
> Kind of progress that was reported.


## Operations

```python
__init__(self, range: Range, kind: Optional[CoqFileProgressKind])
```
> Creates a new CoqFileProgressProcessingInfo instance.
> 
> `range : Range` [Range](../../../lsp/structs/Range.md)
> > Range for which the processing info was reported.
> 
> `kind : Optional[CoqFileProgressKind]` [CoqFileProgressKind](../structs/CoqFileProgressKind.md)
> > Kind of progress that was reported.