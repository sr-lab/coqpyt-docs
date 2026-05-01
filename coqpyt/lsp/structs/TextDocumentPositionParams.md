# `TextDocumentPositionParams`

A parameter literal used in requests to pass a text document and a position inside that document.

## Attributes

`textDocument : TextDocumentIdentifier` [TextDocumentIdentifier](./TextDocumentIdentifier.md)
> The text document.

`position : Position` [Position](./Position.md)
> The position inside the text document.


## Operations
```python
__init__(self, textDocument: TextDocumentIdentifier, position: Position)
```
> Constructs a new TextDocumentPositionParams instance.
> 
> `textDocument : TextDocumentIdentifier` [TextDocumentIdentifier](./TextDocumentIdentifier.md)
> > The text document.
> 
> `position : Position` [Position](./Position.md)
> > The position inside the text document.