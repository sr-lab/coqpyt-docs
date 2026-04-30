# `FlecheDocument`

Structure containing all elements of the AST of the file and the completion status of the LSP in processing the file. The list of AST elements is used to initialize the steps of CoqFile or ProofFile.

## Attributes

`spans : List[RangedSpan]` [RangedSpan](../structs/RangedSpan.md)
> Array of all AST elements in the document.

`completed : CompletionStatus` [CompletionStatus](../structs/CompletionStatus.md)
> Document's processing status.


## Operations

```python
__init__(self, spans: List[RangedSpan], completed: CompletionStatus)
```
> Creates a new FlecheDocument instance.
> 
> `spans : List[RangedSpan]` [RangedSpan](../structs/RangedSpan.md)
> > Array of all AST elements in the document.
> 
> `completed : CompletionStatus` [CompletionStatus](../structs/CompletionStatus.md)
> > Document's processing status.


## Static Operations

```python
parse(fleche_document: Dict) -> Optional[FlecheDocument]
```
> Converts a dictionary representing a Fleche Document into a FlecheDocument object.
> 
> `fleche_document : Dict`
> > Dictionary to parse.
> 
> Returns: `Optional[FlecheDocument]` The created FlecheDocument object if successful.