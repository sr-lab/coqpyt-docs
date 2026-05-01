# `CompletionStatus`

Status of a documents completion in processing. Considers the document as a whole, instead of the progress of a specific line.

## Attributes

`status : str`
> Status of the document. One of "Yes", "Stopped", or "Failed". "Yes" if the document has been fully checked.

`range : Range` [Range](../../../lsp/structs/Range.md)
> Location of the last seen lexical token in the file. Used for finding where the document has left off.


## Operations

```python
__init__(self, status: str, range: Range)
```
> Creates a new CompletionStatus instance.
> 
> `status : str`
> > Status of the document.
> 
> `range : Range` [Range](../../../lsp/structs/Range.md)
> > The last seen lexical token in the file.