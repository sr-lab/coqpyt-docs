# `Message`

A structure representing the messages created by the language server when evaluating the steps within a proof.

## Attributes

`level : int`
> The level of severity of this message.

`text : str`
> The text content of the message.

`range : Range` [Range](../../../lsp/structs/Range.md)
> The range in the file for which this message applies.


## Operations

```python
__init__(self, level: int, text: str, range = None)
```
> Creates a new Message object.
> 
> `level`
> > The level of severity of this message.
> 
> `text : str`
> > The text content of the message.
> 
> `range : Range = None`
> > The range in the file for which this message applies.