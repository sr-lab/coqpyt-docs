# `TextEdit`

A textual edit applicable to a text document.

## Attributes

`range : Range | Dict` [Range](./Range.md)
> The range of the text document to be manipulated. To insert text into a document create a range where start === end.

`newText : str`
> The string to be inserted. For delete operations use an empty string.


## Operations

```python
__init__(self, range: Range | Dict, newText: str)
```
> Constructs a new TextEdit instance.
> 
> `range : Range | Dict` [Range](./Range.md)
> > The range of the text document to be manipulated.
> 
> `newText : str`
> > The string to be inserted.