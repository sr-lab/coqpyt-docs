# `Term`

Term of a Rocq file. Represents a variable that is defined in a file or library to be used elsewhere in the program.

## Attributes

`step : Step` [Step](./Step.md)
> The step where the term is defined.

`type : TermType` [TermType](./TermType.md)
> The type of the term.

`file_path : str`
> The file where the term is.

`module : List[str]`
> The module where the term is.


## Properties

`text : str`
> The textual representation of the term.

`ast : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> The AST representation of the term.


## Operations

```python
__init__(self, step: Step, type: TermType, file_path: str, module: List[str])
```
> Creates a new Term object.
> 
> `step : Step` [Step](./Step.md)
> > The step where the term is defined.
> 
> `type : TermType` [TermType](./TermType.md)
> > The type of the term.
> 
> `file_path : str`
> > The file where the term is.
> 
> `module : List[str]`
> > The module where the term is.