# `RangedSpan`

Structure holding information about a vernacular expression in the AST of the file. For more information about the format of the vernacular expression, check out the [docs](https://rocq-prover.org/doc/v8.20/api/coq-core/Vernacexpr/index.html). The OCaml types have been parsed into Python dictionaries. The base type that `span` represents is `vernac_control`, located at the bottom of the linked doc page. 

*Note:* This doc page is for the 8.20 version of Rocq, prior to its rebranding as Rocq. Documentation for the 9.x version of Rocq is still incomplete, with the `Vernacexpr` module having no documentation. For the most accurate information, use the Rocq source code for [vernacexpr](https://github.com/rocq-prover/rocq/blob/master/vernac/vernacexpr.mli)).

## Attributes

`range : Range` [Range](../../../lsp/structs/Range.md)
> Range in the file where this span is located.

`span : Any`
> Vernacular expression describing this specific span in the AST. 


## Operations

```python
__init__(self, range: Range, span: any)
```
> Creates a new RangedSpan instance.
> 
> `range : Range` [Range](../../../lsp/structs/Range.md)
> > Range in the file where this span is located.
> 
> `span : Any`
> > Vernacular expression describing this specific span in the AST. 