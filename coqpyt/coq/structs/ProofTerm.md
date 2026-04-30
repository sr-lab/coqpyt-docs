# `ProofTerm(Term)` [Term](./Term.md)

Term specifically used in a proof file. These terms are used to identify the proofs in the file. 

## Attributes

`steps : List[ProofStep]` [ProofStep](./ProofStep.md)
> The list of all steps taken in defining this term.

`context : List[Term]` [Term](./Term.md)
> The terms and notations used in the definition of this proof term.

`program : Optional[Term]` [Term](./Term.md)
> The last term defined in the context. Used to identify where in the program this term has been defined.

## Operations

```python
__init__(self, term: Term, context: List[Term], steps: List[ProofStep], program: Optional[Term] = None)
```
> Creates a new ProofTerm object
> 
> `term : Term` [Term](./Term.md)
> > Predefined term object to use to set the attributes of the Term class which this class extends.
> 
> `context : List[Term]` [Term](./Term.md)
> > The terms and notations used in the definition of this proof term.
> 
> `steps : List[ProofStep]` [ProofStep](./ProofStep.md)
> > The list of all steps taken in defining this term.
> 
> `program : Optional[Term] = None` [Term](./Term.md)
> > *Optional.* The last term defined in the context. Defaults to None.