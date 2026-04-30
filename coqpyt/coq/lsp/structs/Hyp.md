# `Hyp`

Abstraction of a Rocq hypothesis.

## Attributes

`names : List[str]`
> Contains hierarchy of module names of the hypothesis.

`ty : str`
> The type of the hypothesis.

`definition : Optional[str]`
> The body of the hypothesis.


## Operations

```python
__init__(self, names: List[str], ty: str, definition: Optional[str])
```
> Creates a new Hyp object.
> 
> `names : List[str]`
> > The names of the hypothesis.
> 
> `ty : str`
> > The type of the hypothesis.
> 
> `definition : Optional[str]`
> > The body of the hypothesis.