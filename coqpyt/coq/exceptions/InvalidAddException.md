# `InvalidAddException(InvalidChangeException)` [InvalidChangeException](./InvalidChangeException.md)

An error created when an addition to a Rocq file leads to error that prevents the file from being successfully evaluated.

## Attributes

`step : str`
> The text representing the step was attempted to be added to the file.


## Operations

```python
__init__(self, step: str)
```
> Creates a new InvalidAddException instance.
> 
> `step : str`
> > The text representing the step was attempted to be added to the file.