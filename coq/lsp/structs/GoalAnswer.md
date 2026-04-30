# `GoalAnswer`

Structure representing the GoalAnswer of the coq-lsp. Goal answer contains specific information about a sentence in a proof, such as any errors.

## Attributes

`textDocument : VersionedTextDocumentIdentifier` [VersionedTextDocumentIdentifier](../../../lsp/structs/VersionedTextDocumentIdentifier.md)
> The URI and version of the file for which this goal is associated with.

`position : Position` [Position](../../../lsp/structs/Position.md)
> The position in the file where the start of the goal sentence is located.

`message : List[Message]` [Message](../structs/Message.md)
> A collection of all messages for the sentence at the position.

`goals : Optional[GoalConfig]` [GoalConfig](../structs/GoalConfig.md)
> All goals that this proof is attempting to meet.

`error : Any`
> The highest priority error for the current sentence.

`program : List`
> Information about the current scope and obligations of the program.

`range : Optional[Range]` [Range](../../../lsp/structs/Range.md)
> The range for which this sentence applies in the file.


## Operations

```python
__init__(self, textDocument: VersionedTextDocumentIdentifier, position: Position, messages: List[Message], goals: Optional[GoalConfig] = None, error: Any = None, program: List = [], range: Range = None)
```
> Creates a new GoalAnswer object.
> 
> `textDocument : VersionedTextDocumentIdentifier` [VersionedTextDocumentIdentifier](../../../lsp/structs/VersionedTextDocumentIdentifier.md)
> > The URI and version of the file for which this goal is associated with.
> 
> `position : Position` [Position](../../../lsp/structs/Position.md)
> > The position in the file where the start of the goal sentence is located.
> 
> `message : List[Message]` [Message](../structs/Message.md)
> > A collection of all messages for the sentence at the position.
> 
> `goals : Optional[GoalConfig] = None` [GoalConfig](../structs/GoalConfig.md)
> > *Optional.* All goals that this proof is attempting to meet. Defaults to None.
> 
> `error : Any = None`
> > *Optional.* The highest priority error for the current sentence. Defaults to None.
> 
> `program : List = []`
> > *Optional.* Information about the current scope and obligations of the program. Defaults to an empty array.
> 
> `range : Range = None` [Range](../../../lsp/structs/Range.md)
> > *Optional.* The range for which this sentence applies in the file. Defaults to None.


## Static Operations

```python
parse(goal_answer: Dict) -> Optional[GoalAnswer]
```
> Converts a dictionary representing goal answer into a GoalAnswer object.
> 
> `goal : Dict`
> > Dictionary to parse.
> 
> Returns: `Optional[GoalAnswer]` The created GoalAnswer object if successful.