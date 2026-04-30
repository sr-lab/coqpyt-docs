# `DiagnosticRelatedInformation

A structure representing extra information that is related to the diagnostic that references this object. These are generally for things that are related to the diagnostic but are in different locations in the file.

## Attributes

`location : Location` [Location](./Location.md)
> The location of this related diagnostic information.

`message : str`
> The message of this related diagnostic information.


## Operations
```python 
__init__(self, location: Location, message: str)
```
> Constructs a new Diagnostic instance.
> 
> `location : Location` [Location](./Location.md)
> > The location of this related diagnostic information.
> 
> `message : str`
> > The message of this related diagnostic information.
