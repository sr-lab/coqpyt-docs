# `TextDocumentContentChangeEvent`

An event describing a change to a text document. If range and rangeLength are omitted the new text is considered to be the full content of the document.

## Attributes

`range : Optional[Range]` [Range](./Range.md)
> The range of the document that changed.

`rangeLength : Optional[int]`
> The length of the range that got replaced.

`text : str`
> The new text of the range/document.


## Operations

```python
__init__(self, range: Optional[Range], rangeLength: Optional[int], text: str)
```
> Constructs a new TextDocumentContentChangeEvent instance.
> 
> `range : Optional[Range]` [Range](./Range.md)
> > The range of the document that changed.
> 
> `rangeLength : Optional[int]`
> > The length of the range that got replaced.
> 
> `text : str`
> > The new text of the range/document.