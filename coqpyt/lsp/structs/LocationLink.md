# `LocationLink`

Represents a link between a source and a target location.

## Attributes

`originSelectionRange : Range` [Range](./Range.md)
> Span of the origin of this link. Used as the underlined span for mouse interaction. Defaults to the word range at the mouse position.

`targetUri : str`
> The target resource identifier of this link.

`targetRange : Range` [Range](./Range.md)
> The full target range of this link. If the target for example is a symbol then target range is the range enclosing this symbol not including leading/trailing whitespace but everything else like comments. This information is typically used to highlight the range in the editor.

`targetSelectionRange : Range` [Range](./Range.md)
> The range that should be selected and revealed when this link is being followed, e.g the name of a function. Must be contained by the the `targetRange`.


## Operations

```python
__init__(self, originSelectionRange: Range | Dict, targetUri: str, targetRange: Range | Dict, targetSelectionRange: Range | Dict)
```
> Constructs a new LocationLink instance.
> 
> `originSelectionRange : Range | Dict` [Range](./Range.md)
> > Span of the origin of this link. If a dictionary is passed, it will be parsed to a Range.
> 
> `targetUri : str`
> > The target resource identifier of this link.
> 
> `targetRange : Range | Dict` [Range](./Range.md)
> > The full target range of this link. If a dictionary is passed, it will be parsed to a Range.
> 
> `targetSelectionRange : Range | Dict` [Range](./Range.md)
> > The range that should be selected and revealed when this link is being followed. If a dictionary is passed, it will be parsed to a Range.