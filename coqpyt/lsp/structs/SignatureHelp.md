# `SignatureHelp`

Signature help represents the signature of something callable. There can be multiple signature but only one active and only one active parameter.

## Attributes

`signatures : List[SignatureInformation]` [SignatureInformation](./SignatureInformation.md)
> List of one or more signatures.

`activeSignature : int`
> The index of the focused signature from the `signatures` list.

`activeParameter : int`
> The index of the focused parameter of the active signature.


## Operations

```python
__init__(self, signatures: List[Signatures] | List[Dict], activeSignature: int = 0, activeParameter: int = 0)
```
> Constructs a new SignatureHelp instance.
> 
> `signatures : List[SignatureInformation] | List[Dict]` [SignatureInformation](./SignatureInformation.md)
> > List of one or more signatures. If a list of dictionaries is passed, it will be parsed to a list of Signatures.
> 
> `activeSignature : int = 0`
> > *Optional.* The index of the focused signature from the `signatures` list. Defaults to 0.
> 
> `activeParameter : int = 0`
> > *Optional.* The index of the focused parameter of the active signature. Defaults to 0.