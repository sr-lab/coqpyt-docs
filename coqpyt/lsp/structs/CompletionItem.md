# `CompletionItem`

Represents a possible entry that could be used to satisfy a completion context.

## Attributes

`label : str`
> The label of this completion item. By default also the text that is inserted when selecting this completion.

`kind : Optional[int]` [CompletionItemKind](./CompletionItemKind.md)
> The kind of this completion item. Based of the kind an icon is chosen by the editor.

`detail : Optional[str]`
> A human-readable string with additional information about this item, like type or symbol information.

`documentation : Optional[str]`
> A human-readable string that represents a doc-comment.

`deprecated : Optional[bool]`
> Indicates if this item is deprecated.

`presented : Optional[bool]`
> Select this item when showing. Note: that only one completion item can be selected and that the tool / client decides which item that is. The rule is that the first item of those that match best is selected.

`sortText : Optional[str]`
> A string that should be used when comparing this item with other items. When `falsy` the label is used.

`filterText : Optional[str]`
> A string that should be used when filtering a set of completion items. When `falsy` the label is used.

`insertText : Optional[str]`
> A string that should be inserted into a document when selecting this completion. When `falsy` the label is used. The `insertText` is subject to interpretation by the client side. Some tools might not take the string literally. For example VS Code when code complete is requested in this example `con<cursor position>` and a completion item with an `insertText` of `console` is provided it will only insert `sole`. Therefore it is recommended to use `textEdit` instead since it avoids additional client side interpretation. 
> *Deprecated.* Use textEdit instead.

`insertTextFormat : Optional[int]` 
> The format of the insert text. The format applies to both the `insertText` property and the `newText` property of a provided `textEdit`. The 2 allowed values are as follows (as defined in the [InsertTextFormat](./InsertTextFormat.md) enum):
> 1. PlainText
> 2. Snippet

`textEdit : Optional[TextEdit | Dict]` [TextEdit](./TextEdit.md)
> An edit which is applied to a document when selecting this completion. When an edit is provided the value of `insertText` is ignored. 
> Note: The range of the edit must be a single line range and it must contain the position at which completion has been requested.

`additionalTextEdits : Optional[List[TextEdit | Dict]]` [TextEdit](./TextEdit.md)
> An optional array of additional text edits that are applied when selecting this completion. Edits must not overlap (including the same insert position) with the main edit nor with themselves. Additional text edits should be used to change text unrelated to the current cursor position (for example adding an import statement at the top of the file if the completion item will insert an unqualified type).

`commitCharacters : Optional[List[str]]`
> An optional set of characters that when pressed while this completion is active will accept it first and then type that character. *Note* that all commit characters should have `length=1` and that superfluous characters will be ignored.

`command : Optional[Command | Dict]` [Command](./Command.md)
> An optional command that is executed *after* inserting this completion. Note: that additional modifications to the current document should be described with the additionalTextEdits-property.

`data : Optional`
> An data entry field that is preserved on a completion item between a completion and a completion resolve request.

`score : float`
> Score of the code completion item.


## Operations

```python
__init__(self, label: str, kind: Optional[int] = None, detail: Optional[int] = None, documentation: Optional[str] = None, deprecated: Optional[bool] = None, presented: Optional[bool] = None, sortText: Optional[str] = None, filterText: Optional[str] = None, insertText: Optional[str] = None, insertTextFormat: Optional[int] = None, textEdit: Optional[TextEdit | Dict] = None, additionalTextEdits: Optional[List[TextEdit | Dict]] = None, commitCharacters: Optional[List[str]] = None, command: Optional[Command | Dict] = None, data: Optional = None, score: float = 0.0)
```
> Constructs a new CompletionItem instance.
> 
> `label : str`
> > The label of this completion item. By default also the text that is inserted when selecting this completion.
> 
> `kind : Optional[int]` [CompletionItemKind](./CompletionItemKind.md)
> > The kind of this completion item. Based of the kind an icon is chosen by the editor.
> 
> `detail : Optional[str]`
> > A human-readable string with additional information about this item, like type or symbol information.
> 
> `documentation : Optional[str]`
> > A human-readable string that represents a doc-comment.
> 
> `deprecated : Optional[bool]`
> > Indicates if this item is deprecated.
> 
> `presented : Optional[bool]`
> > Select this item when showing.
> 
> `sortText : Optional[str]`
> > A string that should be used when comparing this item with other items. When `falsy` the label is used.
> 
> `filterText : Optional[str]`
> > A string that should be used when filtering a set of completion items. When `falsy` the label is used.
> 
> `insertText : Optional[str]`
> > A string that should be inserted into a document when selecting this completion. When `falsy` the label is used.
> 
> `insertTextFormat : Optional[int]` 
> > The format of the insert text. 
> 
> `textEdit : Optional[TextEdit | Dict]` [TextEdit](./TextEdit.md)
> > An edit which is applied to a document when selecting this completion.
> 
> `additionalTextEdits : Optional[List[TextEdit | Dict]]` [TextEdit](./TextEdit.md)
> > An optional array of additional text edits that are applied when selecting this completion. 
> 
> `commitCharacters : Optional[List[str]]`
> > An optional set of characters that when pressed while this completion is active will accept it first and then type that character.
> 
> `command : Optional[Command | Dict]` [Command](./Command.md)
> > An optional command that is executed *after* inserting this completion.
> 
> `data : Optional`
> > An data entry field that is preserved on a completion item between a completion and a completion resolve request.
> 
> `score : float`
> > Score of the code completion item.