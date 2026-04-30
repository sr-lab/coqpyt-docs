# `SymbolInformation`

Represents programming constructs like variables, classes, interfaces etc. that appear in a document. Document symbols can be hierarchical and they have two ranges: one that encloses its definition and one that points to its most interesting range, e.g. the range of an identifier.

## Attributes

`name : str`
> The name of this symbol.

`kind : SymbolKind` [SymbolKind](./SymbolKind.md)
> The kind of this symbol.

`containerName : Optional[str]`
> The name of the symbol containing this symbol. This information is for user interface purposes (e.g. to render a qualifier in the user interface if necessary). It can't be used to re-infer a hierarchy for the document symbols.

`deprecated : bool`
> Indicates if this symbol is deprecated.

`detail : Optional`
> More detail for this symbol, e.g the signature of a function.

`range : Optional[Range]`
> The range enclosing this symbol not including leading/trailing whitespace but everything else like comments. This information is typically used to determine if the clients cursor is inside the symbol to reveal it  in the UI.

`selectionRange : Optional[Range]`
> The range that should be selected and revealed when this symbol is being picked, e.g. the name of a function. Must be contained by the `range`.


## Operations

```python
__init__(self, name: str, kind: int, detail = None, range: Range = None, selectionRange: Range = None, location: Location = None, containerName: Optional[str] = None, deprecated: bool = False)
```
> Constructs a new SymbolInformation instance.
> 
> `name : str`
> > The name of this symbol.
> 
> `kind : int`
> > The kind of this symbol. The provided int gets cast to the corresponding value of the SymbolKind enum.
> 
> `detail = None`
> > *Optional.* More detail for this symbol, e.g the signature of a function. Defaults to None.
> 
> `range : Range = None` [Range](./Range.md)
> > *Optional.* The range enclosing this symbol not including leading/trailing whitespace but everything else like comments. Defaults to None.
> 
> `selectionRange : Range = None` [Range](./Range.md)
> > *Optional.* The range that should be selected and revealed when this symbol is being picked, e.g. the name of a function. Must be contained by the `range`. Defaults to None.
> 
> `location : Location = None` [Location](./Location.md)
> > *Optional.* The location of this symbol. Defaults to None.
> 
> `containerName : Optional[str] = None`
> > *Optional.* The name of the symbol containing this symbol. Defaults to None.
> 
> `deprecated : bool = False`
> > *Optional.* Indicates if this symbol is deprecated. Defaults to False.