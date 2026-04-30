# `CompletionList`

Represents a collection of completion items to be presented in the editor.

## Attributes

`isIncomplete : bool`
> Whether the list is complete. Further typing should result in recomputing this list.

`items : List[CompletionItem]` [CompletionItem](./CompletionItem.md)
> The completion items.


## Operations
```python
__init__(self, isComplete: bool, items: List[CompletionItem | Dict])
```
> Creates a new CompletionList instance.
> 
> `isComplete : bool`
> > Whether the list is complete.
> 
> `items : List[CompletionItem | Dict]` [CompletionItem](./CompletionItem.md)
> > The completion items. If a dictionary is passed, they will automatically be converted into CompletionItem objects.