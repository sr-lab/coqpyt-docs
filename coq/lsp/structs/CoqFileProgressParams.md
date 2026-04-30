# `CoqFileProgressParams`

Structure holding information on the processing progress of each range in the AST for a given Rocq file.

## Attributes

`textDocument : VersionedTextDocumentIdentifier` [VersionedTextDocumentIdentifier](../../../lsp/structs/VersionedTextDocumentIdentifier.md)
> The text document to which this progress notification applies.

`processing : List[CoqFileProgressProcessingInfo]` [CoqFileProgressProcessingInfo](../structs/CoqFileProgressProcessingInfo.md)
> Array containing the parts of the file which are still being processed. The array should be empty if and only if the server is finished processing.


## Operations

```python
__init__(self, textDocument: VersionedTextDocumentIdentifier, processing: List[CoqFileProgressProcessingInfo])
```
> Creates a new CoqFileProgressParams instance.
> 
> `textDocument : VersionedTextDocumentIdentifier` [VersionedTextDocumentIdentifier](../../../lsp/structs/VersionedTextDocumentIdentifier.md)
> > The text document to which this progress notification applies.
> 
> `processing : List[CoqFileProgressProcessingInfo]` [CoqFileProgressProcessingInfo](../structs/CoqFileProgressProcessingInfo.md)
> > Array containing the parts of the file which are still being processed. 


## Static Operations

```python
parse(coqFileProgressParams: Dict) -> Optional[CoqFileProgressParams]
```
> Converts a dictionary representing a CoqFileProgressParams into a CoqFileProgressParams object.
> 
> `coqFileProgressParams : Dict`
> > Dictionary to parse.
> 
> Returns: `Optional[CoqFileProgressParams]` The created CoqFileProgressParams object if successful.