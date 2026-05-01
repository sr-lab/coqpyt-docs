# `Range`

A structure representing a range of characters in a file. Generally, this is used to represent tokens in a file.

## Attributes

`start : Position` [Position](./Position.md)
> The range's start position.

`end : Position` [Position](./Position.md)
> The range's end position.


## Operations

```python
__init__(self, start: Position | Dict, end: Position | Dict)
```
> Constructs a new Range instance.
> 
> `start : Position | Dict` [Position](./Position.md)
> > The range's start position. If a dictionary is passed, it will be parsed to a Position.
> 
> `end : Position | Dict` [Position](./Position.md)
> > The range's end position. If a dictionary is passed, it will be parsed to a Position.