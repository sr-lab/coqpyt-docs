# `ProofStep`

Step specifically used in a proof file which contains extra information about the goals of the proof this step may be a part of.

## Attributes

`step : Step` [Step](./Step.md)
> Internal step object to hold the basic step information.

`context : List[Term]` [Term](./Term.md)
> The terms and notations used in this proof step.

`_goals : Union[GoalAnswer, Callable[[Position], GoalAnswer]]` [GoalAnswer](../lsp/structs/GoalAnswer.md) [Position](../../lsp/structs/Position.md)
> The specific goal that this proof step is used for. A function can be passed in as a getter for the goal answer based on the position of the step. 

## Properties

`goals : GoalAnswer` [GoalAnswer](../lsp/structs/GoalAnswer.md)
> The goal that this proof step is used for. If `_goals` is a function, then the position of this step in the file is used as the parameter to get the goal answer at this steps location.

`ast : RangedSpan` [RangedSpan](../lsp/structs/RangedSpan.md)
> Expression in the AST where this step is defined.

`text : str`
> Untrimmed string of the entire step, including any line breaks within and surrounding it.

`diagnostics : List[Diagnostic]` [Diagnostic](../../lsp/structs/Diagnostic.md)
> Any diagnostics created by the language server about this step.


## Operations

```python
__init__(self, step: Step, goals: Union[GoalAnswer, Callable[[Position], GoalAnswer]], context: List[Term])
```
> Creates a new ProofStep object
> 
> `step : Step` [Step](./Step.md)
> > Internal step object to hold the basic step information.
> 
> `goals : Union[GoalAnswer, Callable[[Position], GoalAnswer]]` [GoalAnswer](../lsp/structs/GoalAnswer.md) [Position](../../lsp/structs/Position.md)
> > The specific goal that this proof step is used for. A function can be passed in as a getter for the goal answer based on the position of the step. 
> 
> `context : List[Term]` [Term](./Term.md)
> > The terms and notations used in this proof step.