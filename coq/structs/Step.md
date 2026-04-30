# `Step`

Individual step to be executed in a Rocq file. Each step is a single expression that can be found in the AST produced by the language server.

## Attributes

`text : str`
> Untrimmed string of the entire step, including any line breaks within and surrounding it.

`short_text : str`
> Trimmed string of the step.

`ast : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> Expression in the AST where this step is defined.

`diagnostics : List[Diagnostic]` [Diagnostic](../../lsp/structs/Diagnostic.md)
> Any diagnostics created by the language server about this step.


## Operations

```python
__init__(self, text: str, short_text: str, ast: RangedSpan)
```
> Creates a new Step object.
>
> `text : str`
> > Untrimmed string of the entire step, including any line breaks within and surrounding it.
>
> `short_text : str`
> > Trimmed string of the step.
>
> `ast : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> > Expression in the AST where this step is defined.