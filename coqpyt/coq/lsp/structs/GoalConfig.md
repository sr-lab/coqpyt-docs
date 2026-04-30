# `GoalConfig`

Structure representing the GoalConfig of the coq-lsp. This is the main object for goals information.

## Attributes

`goals : List[Goal]` [Goal](../structs/Goal.md)
> The current list of foreground goals.

`stack : List[Tuple[List[Goal], List[Goal]]]` [Goal](../structs/Goal.md)
> A list of focused goals, where each element represents a focus position.

`shelf : List[Goal]` [Goal](../structs/Goal.md)
> List of goals hiding from tactics.

`given_up : List[Goal]` [Goal](../structs/Goal.md)
> List of admitted goals.

`bullet : Any`
> Type of bullet used in structuring the proof.


## Operations

```python
__init__(self, goals: List[Goal], stack: List[Tuple[List[Goal], List[Goal]]], shelf: List[Goal], given_up: List[Goal], bullet: Any = None)
```
> Creates a new GoalConfig object.
> 
> `goals : List[Goal]` [Goal](../structs/Goal.md)
> > The current list of foreground goals.
> 
> `stack : List[Tuple[List[Goal], List[Goal]]]` [Goal](../structs/Goal.md)
> > A list of focused goals, where each element represents a focus position.
> 
> `shelf : List[Goal]` [Goal](../structs/Goal.md)
> > List of goals hiding from tactics.
> 
> `given_up : List[Goal]` [Goal](../structs/Goal.md)
> > List of admitted goals.
> 
> `bullet : Any = None` [Goal](../structs/Goal.md)
> > *Optional.* Type of bullet used in structuring the proof. Defaults to None.


## Static Operations

```python
parse(goal_config: Dict) -> Optional[GoalConfig]
```
> Converts a dictionary representing goal config into a GoalConfig object.
> 
> `goal : Dict`
> > Dictionary to parse.
> 
> Returns: `Optional[GoalConfig]` The created GoalConfig object if successful.