# `Position`

A structure representing a position in a file, indexed by its line and character in that line.

## Attributes

`line : int`
> Line position in a document (zero-based).

`character : int`
> Character offset on a line in a document (zero-based).

`offset : int`
> Character offset from the start of the file. (Unused by CoqPyt)


## Operations

```python
__init__(self, line: int, character: int, offset: int = 0)
```
> Constructs a new Position instance.
> 
> `line : int`
> > Line position in a document (zero-based).
> 
> `character : int`
> > Character offset on a line in a document (zero-based).
> 
> `offset : int = 0`
> > *Optional.* Character offset from the start of the file. Defaults to 0.