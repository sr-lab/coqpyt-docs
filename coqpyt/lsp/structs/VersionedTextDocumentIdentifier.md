# `VersionedTextDocumentIdentifier(TextDocumentIdentifier)` [TextDocumentIdentifer](./TextDocumentIdentifier.md)

An identifier to denote a specific version of a text document.

## Attributes

`version : int`
> The version number of this document. If a versioned text document identifier is sent from the server to the client and the file is not open in the editor (the server has not received an open notification before) the server can send `null` to indicate that the version is known and the content on disk is the truth (as speced with document content ownership). 
> The version number of a document will increase after each change, including undo/redo. The number doesn't need to be consecutive.


## Operations

```python
__init__(self, uri: str, version: int)
```
> Constructs a new TextDocumentIdentifier instance.
> 
> `uri : str`
> > The text document's URI.
> 
> `version : int`
> > The version number of this document.