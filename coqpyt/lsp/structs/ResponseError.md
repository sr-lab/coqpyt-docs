# `ResponseError(Exception)`

An error object created when the language server returns an error.

## Attributes

`code : int`
> The error code of the error. Error types recognized by CoqPyt can be found in [ErrorCodes](./ErrorCodes.md).

`message : str`
> The message of the error.

`data : Optional`
> Any extra data that the server returns in relation to the error.


## Operations
```python
__init__(self, code: int | ErrorCodes, message: str, data: Optional = None)
```
> Creates a new ResponseError instance.
> 
> `code : int | ErrorCodes` [ErrorCodes](./ErrorCodes.md)
> > The error code of the error. If an ErrorCodes value is passed in, the associated value is used.
> 
> `message : str`
> > The message of the error.
> 
> `data : Optional = None`
> > *Optional.* Any extra data that the server returns in relation to the error. Defaults to None.