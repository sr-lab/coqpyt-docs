# `ParameterInformation`

Represents a parameter of a callable-signature. A parameter can have a label and a doc-comment.

## Attributes

`label : str`
> The label of this parameter. Will be shown in the UI.

`documentation : str`
> The human-readable doc-comment of this parameter. Will be shown in the UI but can be omitted.


## Operations

```python
__init__(self, label: str, documentation: str = "")
```
> Constructs a new ParameterInformation instance.
> 
> `label : str`
> > The label of this parameter.
> 
> `documentation : str = ""`
> > *Optional.* The human-readable doc-comment of this parameter. Defaults to "".