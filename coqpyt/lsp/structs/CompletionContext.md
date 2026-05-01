# `CompletionContext`

Contains additional information about the context in which a completion request is triggered.

## Attributes

`triggerKind : int`
> How the completion was triggered. The 3 allowed values as defined in [CompletionTriggerKind](./CompletionTriggerKind.md) are as follows:
> 1. Invoked
> 2. TriggerCharacter
> 3. TriggerForIncompleteCompletions

`triggerCharacter : Optional[str]`
> The trigger character (a single character) that has trigger code complete. Is undefined if `triggerKind` is not TriggerCharacter.


## Operations

```python
__init__(self, triggerKind: int, triggerCharacter: Optional[str] = None)
```
> Constructs a new CompletionContext instance.
> 
> `triggerKind : int`
> > How the completion was triggered.
> 
> `triggerCharacter : Optional[str] = None`
> > The trigger character (a single character) that has trigger code complete.