# `Result`

Contains information about the result of a diagnostic query, combining the range where the result was found and the message associated with it.

## Attributes

`range : Range` [Range](../../../lsp/structs/Range.md)
> Range for which the result was found in a file.

`message : Message` [Message](../structs/Message.md)
> The diagnostic's message for this result.


## Operations

```python
__init__(self, range: Range, message: Message)
```
> Creates a new Result instance.
> 
> `range : Range` [Range](../../../lsp/structs/Range.md)
> > Range for which the result was found in a file.
> 
> `message : Message` [Message](../structs/Message.md)
> > The diagnostic's message for this result.