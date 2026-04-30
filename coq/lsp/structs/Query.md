# `Query`

An object representing a keyword query of all diagnostics, along with any results that were found throughout files.

## Attributes

`query : str`
> The keyword string used to search the list of diagnostics with.

`results : List[Result]` [Result](../structs/Result.md)
> All the diagnostics messages that match the query string.


## Operations

```python
__init__(self, query: str, results: List[Result])
```
> Creates a new Query instance.
> 
> `query : str`
> > The keyword string used to search the list of diagnostics with.
> 
> `results : List[Result]` [Result](../structs/Result.md)
> > All the diagnostics messages that match the query string.