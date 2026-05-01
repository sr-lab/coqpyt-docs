# `Goal`

Abstraction of a Rocq goal.

## Attributes

`hyps : List[Hyp]` [Hyp](../structs/Hyp.md)
> All hypotheses used to support the goal.

`ty : str`
> The type of the goal.


## Operations

```python
__init__(self, hyps: List[Hyp], ty: str)
```
> Creates a new Goal object.
> 
> `hyps : List[Hyp]` [Hyp](../structs/Hyp.md)
> > All hypotheses used to support the goal.
> 
> `ty : str`
> > The type of the goal.


## Static Operations

```python
parse(goal: Dict) -> Optional[Goal]
```
> Converts a dictionary representing a Goal into a Goal object.
> 
> `goal : Dict`
> > Dictionary to parse.
> 
> Returns: `Optional[Goal]` The created Goal object if successful.