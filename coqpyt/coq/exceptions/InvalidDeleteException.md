# `InvalidDeleteException(InvalidChangeException)` [InvalidChangeException](./InvalidChangeException.md)

An error created when an removal from a Rocq file leads to error that prevents the file from being successfully evaluated.

## Attributes

`step : str`
> The text representing the step was attempted to be removed to the file.


## Operations

```python
__init__(self, step: str)
```
> Creates a new InvalidDeleteException instance.
> 
> `step : str`
> > The text representing the step was attempted to be removed to the file.