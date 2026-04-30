# `Location`

Represents a location inside a resource, such as a line inside a text file.

## Attributes

`uri : str`
> The location of the resource file.

`range : Range` [Range](./Range.md)
> The range inside the file.


## Operations

```python
__init__(self, uri: str, range: Range | Dict)
```
> Constructs a new Location instance.
> 
> `uri : str`
> > Resource file.
> 
> `range : Range | Dict` [Range](./Range.md)
> > The range inside the file. If a dictionary is passed, it will be parsed to a Range.