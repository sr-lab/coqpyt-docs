# `SignatureInformation`

Represents the signature of something callable. A signature can have a label, like a function-name, a doc-comment, and a set of parameters.

## Attributes

`label : str`
> The label of this signature. Will be shown in the UI.

`documentation : str`
> The human-readable doc-comment of this signature. Will be shown in the UI but can be omitted.

`parameters : List[ParameterInformation]` [ParameterInformation](./ParameterInformation.md)
> The parameters of this signature.


## Operations

```python
__init__(self, label: str, documentation: str = "", parameters: List[ParameterInformation] | List[Dict] = [])
```
> Constructs a new SignatureInformation instance.
> 
> `label : str`
> > The label of this signature. 
> 
> `documentation : str = ""`
> > *Optional.* The human-readable doc-comment of this signature. Defaults to "".
> 
> `parameters : List[ParameterInformation] | List[Dict] = []` [ParameterInformation](./ParameterInformation.md)
> > *Optional.* The parameters of this signature. If a list of dictionaries is passed, it will be parsed to a list of parameter informations. Defaults to \[\].